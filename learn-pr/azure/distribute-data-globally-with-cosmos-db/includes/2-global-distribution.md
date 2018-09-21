Ihren Kunden den schnellsten Zugang zu den Produkten auf Ihrer Bekleidungswebsite zu bieten, ist für Ihre Kunden und den Erfolg Ihres Unternehmens ausschlaggebend. Verkürzen Sie die Wege, die Daten zu den Benutzern zurücklegen müssen, um mehr Inhalte schneller bereitzustellen. Wenn Ihre Daten in Azure Cosmos DB gespeichert sind, ist die Replikation der Websitedaten in mehrere Regionen auf der ganzen Welt ein Kinderspiel. 

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

In dieser Einheit lernen Sie die Vorteile der globalen Verteilung und eines nativen Multimaster-Datenbankdiensts kennen und replizieren Ihr Konto anschließend in drei weitere Regionen.

## <a name="global-distribution-basics"></a>Grundlagen der globalen Verteilung

Die globale Verteilung ermöglicht es Ihnen, Daten aus einer Region in mehrere Azure-Regionen zu replizieren. Sie können jederzeit Regionen hinzufügen oder entfernen, in denen Ihre Datenbank repliziert ist. Dabei stellt Azure Cosmos DB sicher, dass Ihre Daten, wenn Sie eine zusätzliche Region hinzufügen, innerhalb von 30 Minuten für Vorgänge verfügbar sind, vorausgesetzt, Ihre Daten sind nicht größer als 100 TB.

Es gibt zwei gängige Szenarios für die Replikation von Daten in zwei oder mehr Regionen:

1. Bereitstellen von Datenzugriff mit geringer Latenz für Endbenutzer, unabhängig davon, wo sie sich befinden
2. Hinzufügen von regionaler Resilienz für Geschäftskontinuität und Notfallwiederherstellung (Business Continuity & Disaster Recovery, BCDR)

Um Kunden den Zugriff mit geringer Latenz zu ermöglichen, wird empfohlen, die Daten in Regionen zu replizieren, die dem Standort Ihrer Benutzer am nächsten liegen. Der Onlineshop Ihres Bekleidungsunternehmen hat Kunden in Los Angeles, New York und Tokio. Sehen Sie sich die Seite mit den [Azure-Regionen](https://azure.microsoft.com/global-infrastructure/regions/) an, und legen Sie die Regionen fest, die diesen Kundengruppen am nächsten liegen, da Sie Benutzer an diese Orte replizieren werden.

Als BCDR-Lösung empfiehlt es sich, die Regionen basierend auf den Regionspaaren hinzuzufügen, die im Artikel [Geschäftskontinuität und Notfallwiederherstellung: Azure-Regionspaare](https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/) beschrieben werden.

Wenn eine Datenbank repliziert wird, werden auch der Durchsatz und der Speicher gleichermaßen repliziert. Wenn also Ihre ursprüngliche Datenbank einen Speicherplatz von 10 GB und einen Durchsatz von 1.000 RU/s hätte und Sie diese in drei weitere Regionen repliziert hätten, würde jede Region über 10 GB an Daten und einen Durchsatz von 1.000 RU/s verfügen. Da der Speicher und der Durchsatz in jede Region repliziert werden, sind die Kosten für die Replikation in eine andere Region die gleichen wie für die ursprüngliche Region. Folglich fallen bei der Replikation in drei zusätzliche Regionen insgesamt etwa die vierfachen Kosten der ursprünglichen, nicht replizierten Datenbank an.

## <a name="creating-an-azure-cosmos-db-account-in-the-portal"></a>Erstellen eines Azure Cosmos DB-Kontos im Portal

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) mit demselben Konto an, das Sie zum Aktivieren der Sandbox verwendet haben.

    > [!IMPORTANT]
    > Melden Sie sich beim Azure-Portal und der Sandbox mit demselben Konto an.
    > 
    > Melden Sie sich beim Azure-Portal über den obigen Link an, um sicherzustellen, dass Sie mit der Sandbox verbunden sind, die Zugriff auf ein Concierge-Abonnement ermöglicht.

1. Klicken Sie auf **Ressource erstellen** > **Datenbanken** > **Azure Cosmos DB**.
   
   ![Der Bereich „Datenbanken“ im Azure-Portal](../media/2-global-distribution/2-create-nosql-db-databases-json-tutorial.png)

1. Geben Sie auf der Seite **Azure Cosmos DB-Konto erstellen** die Einstellungen für das neue Azure Cosmos DB-Konto einschließlich des Standorts ein.

    <!-- Resource selection --> [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]
     
    Einstellung|Wert|Beschreibung
    ---|---|---
    ID|*Ein eindeutiger Name*|Geben Sie einen eindeutigen Namen ein, der das Azure Cosmos DB-Konto identifiziert. Da *documents.azure.com* an die ID angefügt wird, die Sie bereitstellen, um Ihren URI zu erstellen, sollten Sie eine eindeutige, aber identifizierbare ID verwenden.<br><br>Die ID darf nur Kleinbuchstaben, Zahlen und einen Bindestrich (-) enthalten, und sie muss zwischen 3 und 50 Zeichen lang sein.
    API|SQL|Die API bestimmt den Typ des zu erstellenden Kontos. Azure Cosmos DB stellt fünf APIs bereit, die Sie für Ihre Anwendung auswählen können: SQL (Dokumentdatenbank), Gremlin (Diagrammdatenbank), MongoDB (Dokumentdatenbank), Azure Table und Cassandra. Für jede ist derzeit ein separates Konto erforderlich. <br><br>Wählen Sie **SQL** aus, da Sie in diesem Modul eine Dokumentdatenbank erstellen, die mit SQL-Syntax abgefragt werden kann und für die SQL-API zugänglich ist.|
    Abonnement|*Concierge-Abonnement*|Wählen Sie Ihr Concierge-Abonnement aus. Ist das Concierge-Abonnement nicht aufgelistet, haben Sie mehrere Mandanten in Ihrem Abonnement aktiviert und müssen die Mandanten wechseln. Hierzu melden Sie sich erneut über den folgenden Link beim Portal an: [Azure-Portal für Sandbox](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true).
    Ressourcengruppe|Vorhandene verwenden<br><br><rgn>[Sandbox-Ressourcengruppenname]</rgn>|Klicken Sie auf **Vorhandene verwenden**, und geben Sie dann <rgn>[Sandbox-Ressourcengruppenname]</rgn> ein.
    Standort|*Auswählen der am nächsten gelegenen Region*|Wählen Sie aus der obigen Liste der Regionen die Region aus, die Ihnen am nächsten liegt.
    Georedundanz| Deaktivieren | Durch diese Einstellung wird eine replizierte Version Ihrer Datenbank in einer zweiten (zugeordneten) Region erstellt. Lassen Sie diese Einstellung vorerst deaktiviert, da Sie die Datenbank später replizieren werden.
    Multimaster | Aktivieren | Durch diese Einstellung können Sie in mehreren Regionen gleichzeitig schreiben. Diese Einstellung kann nur bei der Kontoerstellung konfiguriert werden.
    Virtuelles Netzwerk|Nicht ausfüllen|Lassen Sie das Feld für virtuelle Netzwerke vorerst leer. Dies kann später konfiguriert werden.

1. Klicken Sie auf **Überprüfen + erstellen**.

    ![Die Seite „Neues Konto“ für Azure Cosmos DB](../media/2-global-distribution/2-azure-cosmos-db-create-new-account.png)

1. Nach Überprüfung der Einstellungen klicken Sie auf **Erstellen**, um das Konto zu erstellen.

1. Die Kontoerstellung dauert einige Minuten. Warten Sie, bis das Portal die Benachrichtigung anzeigt, dass die Bereitstellung erfolgreich war, und klicken Sie auf die Benachrichtigung.

    ![Benachrichtigung](../media/2-global-distribution/2-azure-cosmos-db-notification.png)

1. Klicken Sie im Benachrichtigungsfenster auf **Zu Ressource wechseln**.

    ![Zu Ressource wechseln](../media/2-global-distribution/2-azure-cosmos-db-go-to-resource.png)

    Im Portal wird **Glückwunsch! Ihr Azure Cosmos DB-Konto wurde erstellt** angezeigt.

    ![Der Bereich „Benachrichtigungen“ im Azure-Portal](../media/2-global-distribution/2-azure-cosmos-db-account-created.png)

## <a name="replicate-data-in-multiple-regions"></a>Replizieren von Daten in mehrere Regionen

Als Nächstes replizieren Sie Ihre Datenbank in Regionen, die Ihren Benutzern in Los Angeles, New York und Tokio am nächsten sind.

1. Klicken Sie auf der Kontoseite im Menü auf **Daten global replizieren**.
1. Wählen Sie auf der Seite **Daten global replizieren** die Regionen „USA, Westen 2“, „USA, Osten“ und „Japan, Osten“ aus, und klicken Sie dann auf **Speichern**.

    Wenn Sie die Karte im Azure-Portal nicht sehen, minimieren Sie die Menüs auf der linken Seite der Anzeige, um sie anzuzeigen.
  
    Auf der Seite wird die Meldung **Wird aktualisiert** angezeigt, während die Daten in die neuen Regionen geschrieben werden. Die Daten werden innerhalb von 30 Minuten in den neuen Regionen verfügbar sein.
   
    ![Hinzufügen von Regionen per Klick auf die Regionen auf der Karte](../media/2-global-distribution/2-global-replication.gif)
 
## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie Ihre Datenbank in die Regionen der Welt repliziert, in denen sich die meisten Ihrer Benutzer befinden, um ihnen einen Zugriff mit geringer Latenz auf die Daten Ihrer Website zu ermöglichen.
