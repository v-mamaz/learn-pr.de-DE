In dieser Einheit verwenden Sie das Azure-Portal, um eine Web-App zu erstellen.

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-web-app"></a>Erstellen einer Web-App

Melden Sie sich beim [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) mit demselben Konto an, über das Sie die Sandbox aktiviert haben.

1. Klicken Sie oben im linken Navigationsbereich auf den Link **Ressource erstellen**. Alle Elemente, die Sie in Azure erstellen, werden als „ Ressource“ bezeichnet.

1. Sie gelangen im Portal zur Seite **Marketplace**. Von hier aus können Sie nach der Ressource suchen, die Sie erstellen möchten, oder eine der beliebten Ressourcen auswählen, die andere Benutzer im Azure-Portal erstellen.

1. Klicken Sie auf **Web** > **-Web-App**. Das Portal leitet Sie zur Seite **Neue Web-App erstellen** weiter.

1. Wenn Sie eine neue Web-App erstellen, fordert das Azure-Portal für das Erstellen der App einige Informationen von Ihnen an. In diesem Abschnitt müssen Sie die folgenden grundlegenden Informationen angeben:

    1. **App-Name**: Ihr Kunde möchte die Anwendung `BestBike` nennen. Geben Sie den Namen in dieses Feld ein. Dieser Wert muss für alle anderen in Azure gehosteten Web-Apps global eindeutig sein, und das Portal überprüft, ob der App-Name bereits vergeben ist. Fügen Sie dem App-Namen einige Zahlen hinzu, um eine eindeutige Variante zu generieren und sicherzustellen, dass Ihr Name eindeutig ist.

    2. **Abonnement:** In diesem Feld müssen Sie über die Dropdownliste ein aktives Azure-Abonnement auswählen. Wählen Sie das Concierge-Abonnement aus.

    3. **Betriebssystem:** In diesem Feld müssen Sie angeben, ob Sie zum Hosten Ihrer neuen Webanwendung **Windows** oder **Linux** verwenden möchten. Diese Einstellung wirkt sich direkt auf den App Service-Plan aus, den Sie unten auswählen oder erstellen. Zur Erinnerung: Ein App Service-Plan ähnelt einem virtuellen Computer, der ein Betriebssystem mit allen Ressourcen (CPU, RAM usw.) ist, die auf diesem Computer benötigt werden, um Ihre Anwendung auszuführen. In diesem Fall möchte Ihr Kunde die Web-App lieber über eine Windows-VM hosten. Wählen Sie daher **Windows** aus.

    4. **Application Insights**: Azure Application Insights hilft Ihnen bei der Erkennung und Diagnose von Qualitätsproblemen in Ihren Web-Apps und Webdiensten macht es leichter, die Aktionen von Benutzern nachzuvollziehen. Der Kunde möchte unter anderem Berichte über den Datenverkehr für seine Website einsehen und Trends für hohen und geringen Datenverkehr untersuchen können. Wählen Sie in diesem Fall die Option **Ein**, um Application Insights für diese Web-App zu aktivieren. Nachdem Sie die Option **Ein** gewählt haben, müssen Sie auch den Standort oder die Region für die Speicherung der Application Insights-Daten auswählen. Beachten Sie, dass Application Insights nur in einer begrenzten Anzahl von Regionen verfügbar ist. Wählen Sie für diese Demo eine der verfügbaren Regionen aus.

## <a name="use-the-sandbox-resource-group"></a>Verwenden der Sandbox-Ressourcengruppe

Eine Azure-Web-App muss einer Ressourcengruppe angehören. Klicken Sie auf **Vorhandene verwenden**, und wählen Sie <rgn>[Name der Sandboxressourcengruppe]</rgn> aus.

## <a name="create-an-app-service-plan"></a>Erstellen eines App Service-Plans

In diesem Feld müssen Sie einen App Service-Plan auswählen, mit dem die Anwendung ausgeführt werden soll. Standardmäßig wählt das Portal den aktuellsten App Service-Plan aus, den Sie erstellt haben. Klicken Sie auf das Feld **App Service-Plan/Standort**, um zur Seite **App Service-Plan** zu navigieren.

Klicken Sie auf den Link **Neu erstellen**, um zur Seite **Neuer App Service-Plan** zu navigieren. Das Portal fordert einige Informationen von Ihnen an, um den neuen App Service-Plan zu erstellen.

1. **App Service-Plan**: In dieses Feld geben Sie einen Namen für den neuen App Service-Plan ein. Geben Sie für diese App den gleichen Web-App-Namen ein, den Sie weiter oben gewählt haben, und fügen Sie das Suffix `-app-service-plan` hinzu, um diese Ressource leichter von anderen unterscheiden zu können.

2. **Standort**: In diesem Feld müssen Sie die Region auswählen, in der sich dieser App Service-Plan befindet. Wählen Sie also den geografischen Ort aus, an dem gemäß dem App Service-Plan die virtuellen Computer eingerichtet werden, die für die Ausführung Ihrer Anwendung erforderlich sind. In diesem Fall können Sie eine beliebige Option aus der Liste verwenden.

[!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

3. **Tarif:** In diesem Feld müssen Sie die Größe des virtuellen Computers auswählen, der Ihre Anwendung hosten soll. Klicken Sie auf das Zeichen **>**, um zur Seite **Tarif** zu navigieren.

    Hier stehen zahlreiche Optionen zur Auswahl. Das Portal gruppiert diese Optionen anhand des Umfangs der benötigten Workload. Die drei verfügbaren Kategorien von Workloads sind „Dev/Test“, „Produktion“ und „App Service (isoliert)“. Wählen Sie je nach den Anforderungen der Anwendung, die Sie in Azure hosten möchten, die passende Workloadkategorie aus. Da die Anwendung **BestBike** sich gerade erst im Aufbau befindet, beginnen Sie mit der minimalen Workloadkategorie, die für Sie am besten geeignet ist. Denken Sie daran, dass eine der Anforderungen des Kunden die Möglichkeit war, alle neuen Änderungen, die an der Anwendung vorgenommen wurden, live zu testen. In den kommenden Einheiten werden Sie sehen, dass Sie zur Erfüllung dieser Anforderung **Bereitstellungsslots** hinzufügen müssen. Bereitstellungsslots sind erst ab dem Tarif **S1** verfügbar. Wählen Sie deshalb in der Kategorie **Produktionsworkload** den Tarif **S1** aus. Klicken Sie dann auf **Übernehmen**, um den Tarif zu bestätigen, den Sie oben ausgewählt haben.

    > [!NOTE]
    > Sie werden in diesem Modul feststellen, dass nur die Workloadkategorien **Produktion** und **App Service (isoliert)**  Ihnen erlauben, **Bereitstellungsslots** zu Ihrer Web-App hinzuzufügen.

    Nun befinden Sie sich wieder auf der Seite **Neuer App Service-Plan**.

    ![Screenshot der Seite „Neuer App Service-Plan“ mit Beispielwerten für diese Übung in den Einstellungen](../media/3-new-app-service-plan.PNG)

4. Klicken Sie auf die Schaltfläche **OK**, um Ihren neuen App Service-Plan zu verwenden.

    Im Portal gelangen Sie zurück zur Hauptseite **Web-App erstellen**.

    ![Screenshot der Seite „Neue Ressource“ in Azure mit hervorgehobener Navigation zur Web-App-Ressource.](../media/3-new-web-app.png)

5. Klicken Sie auf die Schaltfläche **Erstellen**, um die Erstellung der Web-App zu starten.

    > [!NOTE]
    > Es dauert unter Umständen ein paar Sekunden, bis Ihre Web-App erstellt wurde und einsatzbereit ist.

Das Portal zeigt die Dashboardseite an und benachrichtigt Sie, sobald die Web-App erstellt wurde.

Wenn die App bereit ist, navigieren Sie im Azure-Portal zu der neuen App.

1. Klicken Sie im linken Navigationsbereich auf das Menü **Alle Ressourcen**. Auf der Seite **Alle Ressourcen** werden alle Ressourcen aufgelistet, die Sie im Azure-Portal erstellt haben.

2. Klicken Sie sich durch den App Service „BestBike“, der soeben für Sie erstellt wurde.

    > [!NOTE]
    > Wenn Sie anhand des Namens „BestBike“ nach Ihrer App suchen, finden Sie unter Umständen auch die Application Insights- und App Service-Plan-Ressourcen, die für Ihre neue Web-App erstellt wurden. Achten Sie darauf, dass Sie sich durch die Ressource vom Typ **App Service** klicken.

    ![Screenshot mit einem Beispielsuchergebnis auf der Seite „Alle Ressourcen“ und hervorgehobenem neu erstelltem App Service BestBike123.](../media/3-web-app.PNG)

Das Portal öffnet die Startseite des Web-App-Diensts. Dabei ist der Abschnitt **Übersicht** ausgewählt.

![Screenshot der App Service-Seite „BestBike“ mit hervorgehobenem URL-Link des Abschnitts „Übersicht“.](../media/3-web-app-home.PNG)

Klicken Sie rechts oben im Azure-Portal auf die **URL**, um eine Vorschau des Standardinhalts Ihrer neuen Web-App anzuzeigen. Wird eine Platzhalter-Webseite angezeigt, haben Sie die Web-App erfolgreich erstellt.
