Ihr Unternehmen hat sich für Azure Cosmos DB entschieden, um die Anforderungen seines wachsenden Kundenstamms und Produktangebots zu erfüllen. Sie wurden mit der Erstellung der Datenbank beauftragt.

Der erste Schritt ist das Erstellen eines Azure Cosmos DB-Kontos.

## <a name="what-is-an-azure-cosmos-db-account"></a>Was ist ein Azure Cosmos DB-Konto?

Ein Azure Cosmos DB-Konto ist eine Azure-Ressource, die als organisatorische Entität für Ihre Datenbanken fungiert. Es verknüpft zu Abrechnungszwecken Ihre Nutzung mit Ihrem Azure-Abonnement.

Jedes Azure Cosmos DB-Konto ist mit einem der verschiedenen Datenmodelle verbunden, die Azure Cosmos DB unterstützt, und Sie können so viele Konten erstellen, wie Sie brauchen. 

Die SQL-API ist das bevorzugte Datenmodell, wenn Sie eine neue Anwendung erstellen. Wenn Sie mit Graphen oder Tabellen arbeiten oder Ihre MongoDB- oder Cassandra-Daten zu Azure migrieren, erstellen Sie zusätzliche Konten, und wählen Sie entsprechende Datenmodelle aus.

Wählen Sie beim Anlegen eines Kontos eine für Sie aussagekräftige ID, anhand derer Sie Ihr Konto identifizieren. Erstellen Sie außerdem das Konto in der Azure-Region, die Ihren Benutzern am nächsten ist, um die Wartezeit zwischen dem Rechenzentrum und Ihren Benutzern zu minimieren.

Sie können bei der Erstellung eines Kontos optional virtuelle Netzwerke und Georedundanz einrichten, was aber auch nachträglich erfolgen kann. In diesem Modul werden wir diese Einstellungen nicht aktivieren.

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="creating-an-azure-cosmos-db-account-in-the-portal"></a>Erstellen eines Azure Cosmos DB-Kontos im Portal

1. Melden Sie sich am [Azure-Portal für die Sandbox](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) mit dem gleichen Konto an, über das Sie die Sandbox aktiviert haben.

    > [!IMPORTANT]
    > Melden Sie sich am Azure-Portal über den Link oben an, um sicherzustellen, dass Sie mit der Sandbox verbunden sind, die Zugriff auf ein Concierge-Abonnement ermöglicht.

1. Klicken Sie auf **Ressource erstellen** > **Datenbanken** > **Azure Cosmos DB**.
   
   ![Der Bereich „Datenbanken“ im Azure-Portal](../media/2-create-nosql-db-databases-json-tutorial.png)

1. Geben Sie auf der Seite **Azure Cosmos DB-Konto erstellen** die Einstellungen für das neue Azure Cosmos DB-Konto einschließlich des Standorts ein.

    [!INCLUDE[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]
 
    Einstellung|Wert|Beschreibung
    ---|---|---
    Abonnement|*Concierge-Abonnement*|Wählen Sie das Concierge-Abonnement aus. Wenn das Concierge-Abonnement nicht aufgelistet wird, haben Sie mehrere Mandanten in Ihrem Abonnement aktiviert und müssen die Mandanten wechseln. Hierzu melden Sie sich erneut über den folgenden Link beim Portal an: [Azure-Portal für Sandbox](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true).
    Ressourcengruppe|Vorhandene verwenden<br><br>**<rgn>[Name der Sandbox-Ressourcengruppe]</rgn>**|Hier erstellen Sie eine neue Ressourcengruppe oder wählen eine vorhandene Ressourcengruppe Ihres Abonnements aus. 
    Kontoname|*Ein eindeutiger Name*|Geben Sie einen eindeutigen Namen ein, der das Azure Cosmos DB-Konto identifiziert. Da *documents.azure.com* an die ID angefügt wird, die Sie bereitstellen, um Ihren URI zu erstellen, sollten Sie eine eindeutige, aber identifizierbare ID verwenden.<br><br>Die ID darf nur Kleinbuchstaben, Zahlen und einen Bindestrich (-) enthalten, und sie muss zwischen 3 und 50 Zeichen lang sein.
    API|SQL|Die API bestimmt den Typ des zu erstellenden Kontos. Azure Cosmos DB stellt fünf APIs bereit, die Sie für Ihre Anwendung auswählen können: SQL (Dokumentdatenbank), Gremlin (Diagrammdatenbank), MongoDB (Dokumentdatenbank), Azure Table und Cassandra. Für jede ist derzeit ein separates Konto erforderlich. <br><br>Wählen Sie **SQL** aus, da Sie in diesem Modul eine Dokumentdatenbank erstellen, die mit SQL-Syntax abgefragt werden kann und für die SQL-API zugänglich ist.|
    Standort|*Auswählen der Region, die Ihnen am nächsten liegt, aus der Liste oben*|Wählen Sie den Standort aus, an dem die Datenbank gespeichert werden soll.
    Georedundanz| Deaktivieren | Durch diese Einstellung wird eine replizierte Version Ihrer Datenbank in einer zweiten (zugeordneten) Region erstellt. Lassen Sie diese Option jetzt deaktiviert, da die Datenbank später repliziert werden kann.
    Multimaster | Deaktivieren | Durch diese Einstellung können Sie in mehreren Regionen gleichzeitig schreiben. Diese Einstellung kann nur bei der Kontoerstellung konfiguriert werden. Lassen Sie diese Option jetzt für diese Einheit deaktiviert.
    Virtuelles Netzwerk|Nicht ausfüllen|Lassen Sie das Feld für virtuelle Netzwerke vorerst leer. Dies kann später konfiguriert werden.

1. Klicken Sie auf **Überprüfen + erstellen**.

    ![Die Seite „Neues Konto“ für Azure Cosmos DB](../media/2-azure-cosmos-db-create-new-account.png)

1. Nach Überprüfung der Einstellungen klicken Sie auf **Erstellen**, um das Konto zu erstellen. 

1. Die Kontoerstellung dauert einige Minuten. Warten Sie, bis das Portal die Benachrichtigung anzeigt, dass die Bereitstellung erfolgreich war, und klicken Sie auf die Benachrichtigung. 

    ![Benachrichtigung](../media/2-azure-cosmos-db-notification.png)

1. Klicken Sie im Benachrichtigungsfenster auf **Zu Ressource wechseln**.

    ![Zu Ressource wechseln](../media/2-azure-cosmos-db-go-to-resource.png)

    Im Portal wird **Glückwunsch! Ihr Azure Cosmos DB-Konto wurde erstellt** angezeigt.

    ![Der Bereich „Benachrichtigungen“ im Azure-Portal](../media/2-azure-cosmos-db-account-created.png)

## <a name="summary"></a>Zusammenfassung

Sie haben ein Azure Cosmos DB-Konto erstellt, was der erste Schritt zur Erstellung einer Azure Cosmos DB-Datenbank ist. Sie haben die entsprechenden Einstellungen für Ihre Datentypen ausgewählt und den Speicherort des Kontos festgelegt, um die Wartezeit für Ihre Benutzer zu minimieren.
