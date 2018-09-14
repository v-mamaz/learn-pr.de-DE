Ihr Team hat sich entschieden, die Möglichkeiten von Azure Event Hubs zu nutzen, um das steigende Transaktionsvolumen in Ihrem System zu bewältigen und zu verarbeiten.

Ein Event Hub ist eine Azure-Ressource. Daher ist Ihr erster Schritt das Erstellen eines neuen Hubs in Azure, den Sie entsprechend den spezifischen Anforderungen Ihrer Anwendungen konfigurieren.

## <a name="what-is-an-azure-event-hub"></a>Was ist ein Azure Event Hub?

Azure Event Hubs ist ein cloudbasierter Dienst zur Ereignisverarbeitung, der pro Sekunde Millionen von Ereignissen empfangen und verarbeiten kann. Event Hubs fungiert als Zugang zu einer Ereignispipeline, in der eingehende Daten empfangen und gespeichert werden, bis Verarbeitungsressourcen verfügbar sind.

Eine Entität, die Daten an die Event Hubs sendet, wird als *Herausgeber* und eine Entität, die Daten von den Event Hubs liest, als *Consumer* oder *Abonnent* bezeichnet. Azure Event Hubs befindet sich zwischen diesen beiden Entitäten, um die Produktion (durch den Herausgeber) und den Verbrauch (durch den Abonnenten) eines Ereignisdatenstroms aufzuteilen. Diese Entkopplung hilft, Szenarien zu bewältigen, in denen die Rate der Ereignisproduktion viel höher ist als der Verbrauch.

![Herausgeber senden mehrere Ereignisse an einen einzelnen Event Hub und stellen die Daten Abonnenten zur Verfügung](../media-draft/2-event-hub-overview.png "Übersicht über Event Hubs")

### <a name="events"></a>Ereignisse

Ein **Ereignis** ist ein kleines Paket, das eine Benachrichtigung zu einer Änderung enthält und nicht die Details darüber, was sich genau geändert hat. Sie können eine Consumeranwendung nicht so konfigurieren, dass sie irgendeine Art von Abfrage auslöst, um die Details zu ermitteln, aber dies ist keine Voraussetzung, und Event Hubs kümmert sich nicht darum. Ereignisse können einzeln oder in Batches veröffentlicht werden, aber eine einzelne Veröffentlichung (ob einzeln oder als Batch) darf 256 KB nicht überschreiten.

Im Gegensatz dazu enthält die **Nachricht** beim Message Queuing (in Azure Service Bus) Daten und das Ereignis. Der Herausgeber der Nachricht erwartet, dass der Consumer die Nachricht auf eine bestimmte Weise verarbeitet.

### <a name="publishers-and-subscribers"></a>Herausgeber und Abonnenten

Ereignisherausgeber sind alle Anwendungen oder Geräte, die Ereignisdaten über HTTPS oder Advanced Message Queuing Protocol (AQMP) 1.0 senden können. 

Für Herausgeber, die Daten häufig senden, bietet AMQP eine bessere Leistung. Es weist jedoch einen höheren anfänglichen Sitzungsaufwand auf, da zunächst ein persistentes bidirektionales Socket und Transport Level Security (TLS) oder SSL/TLS eingerichtet werden müssen. 

Für ein Veröffentlichen mit häufigerer Unterbrechung ist HTTPS die bessere Option. Obwohl HTTPS für jede Anforderung zusätzlichen SSL-Aufwand mit sich bringt, fällt kein Aufwand für die Sitzungsinitialisierung an.

> [!NOTE] 
> Bestehende Kafka-basierte Anwendungen, die Apache Kafka 1.0 und neuere Clientversionen verwenden, können auch als Event Hubs-Herausgeber fungieren.

Ereignisabonnenten sind Anwendungen, die eine von zwei unterstützten programmgesteuerten Methoden verwenden, um Ereignisse von einem Event Hub zu empfangen und zu verarbeiten.

- **EventHubReceiver**: Eine einfache Methode, die eingeschränkte Optionen für die Verwaltung bereitstellt.
- **EventProcessorHost**: Eine effiziente Methode, die wir später in diesem Modul verwenden.

### <a name="consumer-groups"></a>Consumergruppen

Eine Event Hub-**Consumergruppe** stellt eine spezifische Ansicht eines Event Hub-Datenstroms dar. Durch die Verwendung separater Consumergruppen können mehrere Abonnentenanwendungen einen Ereignisdatenstrom unabhängig und ohne Auswirkungen auf andere Anwendungen verarbeiten. Allerdings ist die Verwendung mehrerer Consumergruppen keine Voraussetzung, und für viele Anwendungen ist die einzelne Standardconsumergruppe ausreichend.

### <a name="pricing"></a>Preise

Für Azure Event Hubs gibt es drei Tarife: Basic, Standard und Dedicated. Die Tarife unterscheiden sich hinsichtlich der unterstützten Verbindungen, der Anzahl verfügbarer Consumergruppen und des Durchsatzes. Wenn Sie mit der Azure CLI einen Event Hubs-Namespace erstellen und keinen Tarif angeben, wird **Standard** (20 Consumergruppen, 1000 vermittelte Verbindungen) zugewiesen.

## <a name="creating-and-configuring-a-new-azure-event-hubs"></a>Erstellen und Konfigurieren eines neuen Azure Event Hubs

Es gibt zwei unverzichtbare Schritte beim Erstellen und Konfigurieren eines neuen Azure Event Hubs. Der erste Schritt ist das Definieren eines Event Hubs-**Namespace**. Der zweite Schritt ist das Erstellen eines Event Hubs in diesem Namespace.

### <a name="defining-an-event-hubs-namespace"></a>Definieren eines Event Hubs-Namespace

Ein Event Hubs-Namespace ist eine Containerentität für die Verwaltung eines oder mehrerer Event Hubs. 

Das Erstellen einen Event Hubs-Namespace umfasst in der Regel Folgendes:

1. Definieren von Einstellungen auf Namespace-Ebene. Bestimmte Einstellungen wie Namespacekapazität (die mit **Durchsatzeinheiten** konfiguriert wird), Tarif und Leistungsmetriken werden auf Namespace-Ebene definiert. Diese gelten für alle Event Hubs innerhalb dieses Namespace. Wenn Sie diese Einstellungen nicht festlegen, wird ein Standardwert verwendet: *1* für Kapazität und *Standard* für Tarif.

    Sie können die Durchsatzeinheit nicht ändern, nachdem Sie sie festgelegt haben. Sie müssen Ihre Konfiguration mit Ihrem verfügbaren Azure-Budget abstimmen. Sie können für unterschiedliche Durchsatzanforderungen verschiedene Event Hubs konfigurieren. Wenn Sie beispielsweise eine Vertriebsdatenanwendung betreiben und zwei Event Hubs planen (einen für die Telemetrieerfassung von Vertriebsdaten in Echtzeit mit hohem Durchsatz und einen für die gelegentliche Sammlung von Ereignisprotokollen), wäre es sinnvoll, für jeden Hub einen eigenen Namespace zu verwenden. Auf diese Weise müssen Sie nur eine hohe Durchsatzkapazität für den Telemetrie-Event Hub konfigurieren (und bezahlen).

1. Auswählen eines eindeutigen Namens für den Namespace. Auf den Namespace kann über diese URL zugegriffen werden: *_Namespace_.servicebus.windows.net*

1. Definieren der folgenden optionalen Eigenschaften:

    - Aktivieren Sie Kafka. Diese Option ermöglicht Kafka-Anwendungen das Veröffentlichen von Ereignissen für den Event Hub.
    - Richten Sie diesen Namespace zonenredundant ein. Zonenredundanz ermöglicht die Replikation von Daten in separaten Rechenzentren mit eigener unabhängiger Energieversorgung, Netzwerk- und Kühlinfrastruktur.
    - Aktivieren Sie „Automatische Vergrößerung“ und „Maximale Durchsatzeinheiten für die automatische Vergrößerung“. „Automatische Vergrößerung“ bietet eine Option für automatisches Hochskalieren, bei der die Anzahl von Durchsatzeinheiten bis zu einem Maximalwert erhöht wird. Dies ist nützlich, um in Situationen, in denen ein- oder ausgehende Datenraten die aktuell festgelegte Anzahl von Durchsatzeinheiten überschreiten, eine Drosselung zu vermeiden.

### <a name="azure-cli-commands-for-creating-an-event-hubs-namespace"></a>Azure CLI-Befehle zum Erstellen eines Event Hubs-Namespace

Führen Sie die folgenden Befehle aus, um einen neuen Event Hub-Namespace zu erstellen:

1. In Azure ist eine Ressourcengruppe ein Container, der zusammengehörige Azure-Ressourcen enthält, um die Verwaltung zu vereinfachen. Erstellen Sie bei Bedarf eine neue Ressourcengruppe für Ihren Event Hub.

    ```azurecli
    az group create --name <resource group name> --location <location>
    ```

1. Erstellen Sie den Event Hubs-Namespace unter Angabe derselben Ressourcengruppe und desselben Speicherorts wie im vorherigen Schritt.

    ```azurecli
    az eventhubs namespace create --name <Event Hubs namespace name> --resource-group <resource group name> -l <location>
    ```

1. Für alle Event Hubs im gleichen Event Hubs-Namespace gelten zur Verbindungsherstellung dieselben Anmeldeinformationen. Sie benötigen diese Anmeldeinformationen, wenn Sie Anwendungen zum Senden und Empfangen von Nachrichten über den Event Hub konfigurieren. Verwenden Sie den folgenden Befehl, um die Verbindungszeichenfolge für Ihren Event Hubs-Namespace zurückzugeben, wobei Sie die gleiche Ressourcengruppe und den gleichen Event Hubs-Namespacenamen wie zuvor verwenden.

    ```azurecli
    az eventhubs namespace authorization-rule keys list --resource-group <resource group name> --namespace-name <EventHub namespace name> --name RootManageSharedAccessKey
    ```

### <a name="configuring-a-new-event-hub"></a>Konfigurieren eines neuen Event Hubs

Nachdem der Event Hubs-Namespace erstellt wurde, können Sie einen Event Hub erstellen. Beim Erstellen eines neuen Event Hubs sind mehrere Pflichtparameter zu beachten.

Dabei handelt es sich um die folgenden:

- **Event Hub-Name**: Der Event Hub-Name, muss innerhalb Ihres Abonnements eindeutig sein und folgende Eigenschaften aufweisen:
  - 1 bis 50 Zeichen
  - Nur Buchstaben, Ziffern, Punkte, Bindestriche und Unterstriche
  - Mit einem Buchstaben oder einer Ziffer beginnen und enden
- **Anzahl der Partitionen**: Die Anzahl, der in einem Event Hub erforderlichen Partitionen (2 bis 32). Dies sollte in direktem Zusammenhang mit der erwarteten Anzahl gleichzeitiger Verbraucher stehen. Dieser Wert kann nach der Erstellung des Event Hubs nicht mehr geändert werden. Die Partition trennt den Nachrichtendatenstrom ab, sodass Consumer- oder Empfängeranwendungen nur eine bestimmte Teilmenge des Datenstroms lesen müssen. Falls nicht definiert, lautet der Standardwert *4*.
- **Nachrichtenaufbewahrung**: Die Anzahl von Tagen (1 bis 7), die Nachrichten verfügbar bleiben, wenn der Datenstrom aus beliebigem Grund erneut wiedergegeben werden muss. Falls nicht definiert, lautet der Standardwert *7*.

Sie können auch optional einen Event Hub konfigurieren, um Daten zu einem Azure Blob Storage- oder Azure Data Lake Store-Konto zu streamen.

### <a name="azure-cli-commands-for-creating-an-event-hub"></a>Azure CLI-Befehle zum Erstellen eines Event Hubs

Führen Sie die folgenden Befehle aus, um einen neuen Event Hub zu erstellen:

1. Erstellen Sie den Event Hub unter Verwendung derselben Ressourcengruppe und desselben Speicherorts wie beim Erstellen des Namespace.

    ```azurecli
    az eventhubs eventhub create --name <event hub name> --resource-group <Resource Group name> --namespace-name <Event Hubs namespace name>
    ```

1. Zeigen Sie die Details Ihres Event Hubs im Namespace unter Verwendung der gleichen Ressourcengruppe und des gleichen Namens für Event Hub und Namespace wie zuvor an.

    ```azurecli
    az eventhubs eventhub show --resource-group <Resource Group name> --namespace-name <Event Hubs namespace name> --name <event hub name>

## Summary

To deploy Azure Event Hubs, you must configure an Event Hubs namespace and then configure the event hub itself. In the next section, you will go through the detailed configuration steps to create a new namespace and event hub.