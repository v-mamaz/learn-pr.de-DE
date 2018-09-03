Ihr Unternehmen hat sich für Azure Cosmos DB entschieden, um die Anforderungen seines wachsenden Kundenstamms und Produktangebots zu erfüllen. Sie wurden mit der Erstellung der Datenbank beauftragt.

Der erste Schritt ist das Erstellen eines Azure Cosmos DB-Kontos. 

## <a name="what-is-an-azure-cosmos-db-account"></a>Was ist ein Azure Cosmos DB-Konto?

Ein Azure Cosmos DB-Konto ist eine Azure-Ressource, die als organisatorische Entität für Ihre Datenbanken fungiert. Es verknüpft zu Abrechnungszwecken Ihre Nutzung mit Ihrem Azure-Abonnement.

Jedes Azure Cosmos DB-Konto ist mit einem der verschiedenen Datenmodelle verbunden, die Azure Cosmos DB unterstützt, und Sie können so viele Konten erstellen, wie Sie brauchen. 

Die SQL-API ist das bevorzugte Datenmodell, wenn Sie eine neue Anwendung erstellen. Wenn Sie mit Graphen oder Tabellen arbeiten oder Ihre MongoDB- oder Cassandra-Daten zu Azure migrieren, erstellen Sie zusätzliche Konten, und wählen Sie entsprechende Datenmodelle aus.

Wählen Sie beim Anlegen eines Kontos eine für Sie aussagekräftige ID, anhand derer Sie Ihr Konto identifizieren. Erstellen Sie außerdem das Konto in der Azure-Region, die Ihren Benutzern am nächsten ist, um die Wartezeit zwischen dem Rechenzentrum und Ihren Benutzern zu minimieren.

Sie können bei der Erstellung eines Kontos optional virtuelle Netzwerke und Georedundanz einrichten, was aber auch nachträglich erfolgen kann. In diesem Modul werden wir diese Einstellungen nicht aktivieren.

## <a name="creating-an-azure-cosmos-db-account-in-the-portal"></a>Erstellen eines Azure Cosmos DB-Kontos im Portal

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an.
2. Klicken Sie auf **Ressourcen erstellen** > **Datenbanken** > **Azure Cosmos DB**.
   
   ![Bereich „Datenbanken“ im Azure-Portal](../media/1-introduction/create-nosql-db-databases-json-tutorial-1.png)

3. Geben Sie auf der Seite **Neues Konto** die Einstellungen für das neue Azure Cosmos DB-Konto ein.
 
    Einstellung|Wert|BESCHREIBUNG
    ---|---|---
    ID|*Ein eindeutiger Name*|Geben Sie einen eindeutigen Namen ein, der das Azure Cosmos DB-Konto identifiziert. Da *documents.azure.com* an die ID angefügt wird, die Sie bereitstellen, um Ihren URI zu erstellen, sollten Sie eine eindeutige, aber identifizierbare ID verwenden.<br><br>Die ID darf nur Kleinbuchstaben, Zahlen und einen Bindestrich (-) enthalten, und sie muss zwischen 3 und 50 Zeichen lang sein.
    API|SQL|Die API bestimmt den Typ des zu erstellenden Kontos. Azure Cosmos DB stellt fünf APIs bereit, die Sie für Ihre Anwendung auswählen können: SQL (Dokumentdatenbank), Gremlin (Diagrammdatenbank), MongoDB (Dokumentdatenbank), Azure Table und Cassandra. Für jede ist derzeit ein separates Konto erforderlich. <br><br>Wählen Sie **SQL** aus, da Sie in diesem Modul eine Dokumentdatenbank erstellen, die mit SQL-Syntax abgefragt werden kann und für die SQL-API zugänglich ist.|
    Abonnement|*Ihr Abonnement*|Wählen Sie das Azure-Abonnement aus, das Sie für das Azure Cosmos DB-Konto verwenden möchten. 
    Ressourcengruppe|Neu erstellen<br><br>*Derselbe eindeutige Name wie oben für die ID*|Wählen Sie **Neu erstellen** aus, und geben Sie dann einen neuen Ressourcengruppenname für Ihr Konto ein. Der Einfachheit halber können Sie denselben Namen als Ihre ID verwenden. 
    Standort|*Die Region, die Ihren Benutzern am nächsten liegt*|Wählen Sie den geografischen Standort aus, an dem Ihr Azure Cosmos DB-Konto gehostet werden soll. Verwenden Sie einen Standort, der Ihren Benutzern am nächsten liegt, um ihnen einen schnellen Zugriff auf die Daten zu gewähren.
    Georedundanz aktivieren| Nicht ausfüllen | Durch diese Einstellung wird eine replizierte Version Ihrer Datenbank in einer zweiten (zugeordneten) Region erstellt. Lassen Sie dieses Feld leer jetzt, da die Datenbank später repliziert werden kann. 
    Virtuelle Netzwerke|Deaktiviert|Lassen Sie virtuelle Netzwerke für den Moment deaktiviert. Sie können später aktiviert werden. 

4. Klicken Sie auf **Erstellen**.

    ![Die Seite „Neues Konto“ für Azure Cosmos DB](../media/1-introduction/azure-cosmos-db-create-new-account.png)

5. Die Kontoerstellung dauert einige Minuten. Warten Sie, bis das Portal die Benachrichtigung anzeigt, dass die Bereitstellung erfolgreich war, und klicken Sie auf die Benachrichtigung. 

    ![Benachrichtigung](../media/1-introduction/azure-cosmos-db-notification.png)

6. Klicken Sie im Benachrichtigungsfenster auf **Zu Ressource wechseln**.

    ![Zu Ressource wechseln](../media/1-introduction/azure-cosmos-db-go-to-resource.png)

    Im Portal wird **Glückwunsch! Ihr Azure Cosmos DB-Konto wurde erstellt** angezeigt.

    ![Der Bereich „Benachrichtigungen“ im Azure-Portal](../media/1-introduction/azure-cosmos-db-account-created.png)

## <a name="summary"></a>Zusammenfassung

Sie haben ein Azure Cosmos DB-Konto erstellt, was der erste Schritt zur Erstellung einer Azure Cosmos DB-Datenbank ist. Sie haben die entsprechenden Einstellungen für Ihre Datentypen ausgewählt und den Speicherort des Kontos festgelegt, um die Wartezeit für Ihre Benutzer zu minimieren.
