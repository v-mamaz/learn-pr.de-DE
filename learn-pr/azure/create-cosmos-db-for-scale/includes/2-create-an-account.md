## <a name="motivation"></a>Motivation

Ihr Unternehmen wurde ausgewählt, dass Azure Cosmos DB, um ihren wachsenden Kunden- und Produktinformationen, die Basis der Anforderungen erfüllen. Sie haben damit beauftragt wurde die Datenbank zu erstellen.

Die Firststep ist ein Azure Cosmos DB-Konto erstellen. 

## <a name="what-is-an-azure-cosmos-db-account"></a>Was ist ein Azure Cosmos DB-Konto?

Azure Cosmos DB-Konto ist eine Azure-Ressource, die fungiert als eine Entität in der Organisation für Ihre Datenbanken aus, und verbindet Ihre Nutzung zu Ihrem Azure-Abonnement für Abrechnungszwecke festzulegen.

Jedes Azure Cosmos DB-Konto zugeordnet ist, mit einem der Daten mehrere Modelle Azure Cosmosdb unterstützt, und Sie können beliebig viele Konten, die Sie nach Bedarf erstellen. 

SQL-API ist das bevorzugte-Datenmodell an, wenn Sie eine neue Anwendung erstellen. Wenn Sie arbeiten mit Diagrammen oder Tabellen, oder Migrieren Ihre MongoDB- oder Cassandra-Daten in Azure, zusätzliche Konten zu erstellen und relevanten Datenmodelle auswählen.

Wenn Sie ein Konto zu erstellen, wählen Sie eine ID, die für Sie sinnvollen; Es ist, wie Sie Ihr Konto identifizieren. Darüber hinaus erstellen Sie das Konto in Azure-Region, die Wartezeit zwischen dem Datencenter und Ihre Benutzer zu verringern, Ihren Benutzern am nächsten ist.

Sie können optional virtuelle Netzwerke und geografische Redundanz festlegen, während der kontoerstellung, aber dies kann auch später durchgeführt werden. In diesem Modul werden wir diese Einstellungen nicht aktivieren.

## <a name="creating-an-azure-cosmos-db-account-in-the-portal"></a>Erstellen ein Azure Cosmos DB-Konto im portal

<!--TODO: Update portal link with one that routes to free Learning acct-->
1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/)an.
2. Klicken Sie auf **Ressourcen erstellen** > **Datenbanken** > **Azure Cosmos DB**.
   
   ![Die Bereich „Datenbanken“ im Azure-Portal](../media/1-introduction/create-nosql-db-databases-json-tutorial-1.png)

3. Geben Sie auf der Seite **Neues Konto** die Einstellungen für das neue Azure Cosmos DB-Konto ein.
 
    Einstellung|Wert|BESCHREIBUNG
    ---|---|---
    ID|*Ein eindeutiger Name*|Geben Sie einen eindeutigen Namen ein, der das Azure Cosmos DB-Konto identifiziert. Da *documents.azure.com* an die ID angefügt wird, die Sie bereitstellen, um Ihren URI zu erstellen, sollten Sie eine eindeutige, aber identifizierbare ID verwenden.<br><br>Die ID darf nur Kleinbuchstaben, Zahlen und den Bindestrich (-) enthalten, und sie muss zwischen 3 und 50 Zeichen lang sein.
    API|SQL|Die API bestimmt den Typ des zu erstellenden Kontos. Azure Cosmos DB stellt fünf APIs entsprechend den Anforderungen Ihrer Anwendung zur Verfügung: SQL (Dokumentendatenbank), Gremlin (Diagrammdatenbank), MongoDB (Dokumentendatenbank), Azure Table und Cassandra, jede ist derzeit ein separates Konto erforderlich. <br><br>Wählen Sie **SQL** da in diesem Modul Sie eine dokumentdatenbank erstellen, die mit SQL-Syntax abgefragt werden kann und für die SQL-API zugänglich ist.|
    Abonnement|*Ihr Abonnement*|Wählen Sie das Azure-Abonnement, das Sie für dieses Azure Cosmos DB-Konto verwenden möchten, aus. 
    Ressourcengruppe|Neu erstellen<br><br>*Derselbe eindeutige Name wie oben für die ID*|Wählen Sie **Neu erstellen** aus, und geben Sie dann einen neuen Ressourcengruppenname für Ihr Konto ein. Der Einfachheit halber können Sie denselben Namen wie bei Ihrer ID verwenden. 
    Speicherort|*Die Region, die Ihren Benutzern am nächsten liegt*|Wählen Sie den geografischen Standort, an dem Ihr Azure Cosmos DB-Konto gehostet werden soll, aus. Verwenden Sie einen Standort, der Ihren Benutzern am nächsten liegt, um ihnen einen schnellen Zugriff auf die Daten zu gewähren.
    Georedundanz aktivieren| Nicht ausfüllen | Dadurch wird eine replizierte Version Ihrer Datenbank in einer zweiten (zugeordneten) Region erstellt. Lassen Sie dieses Feld leer jetzt wie die Datenbank später repliziert werden kann. 
    Virtuelle Netzwerke|Deaktiviert|Virtuelle Netzwerke, die jetzt deaktiviert lassen, können sie später aktiviert werden. 

4. Klicken Sie auf **Erstellen**.

    ![Die Seite „Neues Konto“ für Azure Cosmos DB](../media/1-introduction/azure-cosmos-db-create-new-account.png)

5. Die kontoerstellung dauert einige Minuten, Warten Sie, bis das Portal, um die Benachrichtigung, dass die Bereitstellung erfolgreich war, und klicken Sie auf die Benachrichtigung angezeigt. 

    ![Benachrichtigung](../media/1-introduction/azure-cosmos-db-notification.png)

6. Klicken Sie in das Benachrichtigungsfenster **zu Ressource wechseln**.

    ![Zu Ressource wechseln](../media/1-introduction/azure-cosmos-db-go-to-resource.png)

7. Das Portal zeigt die **Herzlichen Glückwunsch! Ihr Azure Cosmos DB-Konto wurde erstellt** anzeigt.

    ![Der Bereich „Benachrichtigungen“ im Azure-Portal](../media/1-introduction/azure-cosmos-db-account-created.png)

## <a name="summary"></a>Zusammenfassung

Sie haben ein Azure Cosmos DB-Konto erstellt, wird der erste Schritt beim Erstellen einer Azure-Cosmos-Datenbank. Sie geeignete Einstellungen für Ihre Datentypen ausgewählt, und legen den Standort, die Wartezeit für Ihre Benutzer zu verringern.