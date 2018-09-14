In dieser Einheit verwenden Sie das Azure-Portal zum Erstellen einer WebApp.

## <a name="sign-in-to-the-azure-portal"></a>Melden Sie sich beim Azure-Portal an.

[!include[](../../../includes/azure-sandbox-activate.md)]

Im ersten Schritt melden Sie sich beim Azure-Portal an:

Öffnen Sie einen Browser, und navigieren Sie zum [Azure-Portal](https://portal.azure.com/?azure-portal=true).

## <a name="create-a-web-app"></a>Erstellen einer Web-App

Nun, da es sich beim Azure-Portal angemeldet sind, erstellen wir eine Web-app.

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. Klicken Sie oben im linken Navigationsbereich auf den Link **Ressource erstellen**. Alle Elemente, die Sie in Azure erstellen, heißen Ressourcen.

1. Das Portal zu gelangen Sie zu der **Marketplace** Seite. Hier können Sie nach der Ressource suchen, die Sie erstellen möchten, oder eine der beliebten Ressourcen auswählen, die andere Benutzer im Azure-Portal erstellen.

1. Klicken Sie auf **Web** > **-Web-App**. Das Portal gelangen Sie zu der **Create New Web App** Seite.

1. Wenn Sie eine neue Web-App erstellen, fordert das Azure-Portal für das Erstellen der App einige Informationen von Ihnen an. In diesem Abschnitt müssen Sie die folgenden grundlegenden Informationen angeben:

    1. **App-Name**: Ihr Kunde möchte die Anwendung benennen`BestBike`. Geben Sie den Namen in dieses Feld ein. Dieser Wert muss für alle anderen in Azure gehosteten Web-Apps global eindeutig sein, und das Portal überprüft, ob der App-Name bereits vergeben ist. Fügen Sie dem App-Namen einige Zahlen hinzu, um eine eindeutige Variante zu generieren und sicherzustellen, dass Ihr Name eindeutig ist.

    2. **Abonnement**: In diesem Feld müssen Sie in der Dropdownliste ein aktives Azure-Abonnement auswählen.

    3. **Betriebssystem**: In diesem Feld müssen Sie entscheiden, ob Sie zum Hosten Ihrer neuen Webanwendung **Windows** oder **Linux** verwenden möchten. Diese Einstellung wirkt sich direkt auf den App Service-Plan aus, den Sie unten auswählen oder erstellen. Zur Erinnerung: Ein App Service-Plan ähnelt einem virtuellen Computer, der ein Betriebssystem mit allen Ressourcen (CPU, RAM usw.) ist, die auf diesem Computer benötigt werden, um Ihre Anwendung auszuführen. In diesem Fall möchte Ihr Kunde die Web-App lieber über eine Windows-VM hosten. Wählen Sie daher **Windows** aus.

    4. **Application Insights**: Azure Application Insights hilft Ihnen bei der Erkennung und Diagnose von Qualitätsproblemen in Ihren Web-Apps und Webdiensten und erleichtert Ihnen zu verstehen, was Ihre Benutzer tatsächlich damit tun. Der Kunde möchte unter anderem Berichte über den Datenverkehr für seine Website einsehen und Trends für hohen und geringen Datenverkehr untersuchen können. Wählen Sie in diesem Fall die Option **Ein**, um Application Insights für diese Web-App zu aktivieren. Nachdem Sie die Option **Ein** ausgewählt haben, müssen Sie auch den Standort bzw. die Region auswählen, wo die Application Insights-Daten gespeichert werden sollen. Beachten Sie, dass Application Insights nur in einer begrenzten Anzahl von Regionen verfügbar ist. Wählen Sie für diese Demo eine der verfügbaren Regionen.

## <a name="use-the-sandbox-resource-group"></a>Verwenden Sie die Sandbox-Ressourcengruppe

Eine Azure-Web-App muss einer Ressourcengruppe angehören. Wählen Sie **vorhandene** , und wählen Sie <rgn>[Ressourcengruppennamen Sandkasten]</rgn>.

## <a name="create-an-app-service-plan"></a>Erstellen eines App Service-Plans

In diesem Feld müssen Sie einen App Service-Plan auswählen, mit dem die Anwendung ausgeführt werden soll. Standardmäßig wählt das Portal die letzte App Service-Plan, den Sie erstellt haben. Klicken Sie auf die **App Service-Plan/Standort** Feld zum Navigieren der **App Service-Plan** Seite.

Klicken Sie auf die **neu erstellen** Link zum Navigieren zu den **neuen App Service-Plan** Seite. Das Portal fordert einige Informationen von Ihnen an, um den neuen App Service-Plan zu erstellen.

1. **App Service-Plan**: In diesem Feld Geben Sie einen Namen für den neuen App Service-Plan. Geben Sie für diese App den gleichen Web-App-Namen ein, den Sie weiter oben gewählt haben, und fügen Sie das Suffix `-app-service-plan` hinzu, um diese Ressource leichter von anderen unterscheiden zu können.

2. **Speicherort**: In diesem Feld müssen Sie die Region auswählen, in der sich dieser App Service-Plan befindet. Wählen Sie also den geografischen Ort aus, an dem gemäß dem App Service-Plan die virtuellen Computer eingerichtet werden, die für die Ausführung Ihrer Anwendung erforderlich sind. In diesem Fall können Sie eine beliebige Option in der Liste auswählen.

3. **Tarif**: In diesem Feld müssen Sie die Größe des virtuellen Computers auswählen, der zum Hosten Ihrer Anwendung dient. Klicken Sie auf die **>** melden, navigieren bei der **Tarif** Seite.

    Hier stehen Ihnen zahlreiche Optionen zur Auswahl. Das Portal gruppiert diese Optionen anhand des Umfangs der benötigten Workload. Die drei verfügbaren Kategorien von Workloads sind „Dev/Test“, „Produktion“ und „App Service (isoliert)“. Je nach Anforderungen der Anwendung, die Sie in Azure hosten möchten, wählen Sie die entsprechende Workloadkategorie aus. Da die Anwendung **BestBike** sich gerade erst im Aufbau befindet, beginnen Sie mit der minimalen Workloadkategorie, die für Sie am besten geeignet ist. Denken Sie daran, dass eine der Anforderungen des Kunden die Möglichkeit war, alle neuen Änderungen, die an der Anwendung vorgenommen wurden, live zu testen. In den kommenden Einheiten werden Sie sehen, dass Sie zur Erfüllung dieser Anforderung **Bereitstellungsslots** hinzufügen müssen. Bereitstellungsslots sind erst ab dem Tarif **S1** verfügbar. Wählen Sie deshalb in der Kategorie **Produktionsworkload** den Tarif **S1** aus. Klicken Sie dann auf **Übernehmen**, um den Tarif zu bestätigen, den Sie oben ausgewählt haben.

    > [!NOTE]
    > Sie werden in diesem Modul feststellen, dass nur die Workloadkategorien **Produktion** und **App Service (isoliert)**  Ihnen erlauben, **Bereitstellungsslots** zu Ihrer Web-App hinzuzufügen.

    Nun, Sie sind an die **neuen App Service-Plan** Seite.

    ![Screenshot der Seite neue App Service-Plan mit Beispielwerte für diese Übung in den Einstellungen](../media/3-new-app-service-plan.PNG)

4. Klicken Sie auf die Schaltfläche **OK**, um Ihren neuen App Service-Plan zu verwenden.

    Das Portal gelangen Sie zurück zum haupthub **Web-App erstellen** Seite.

    ![Der Screenshot zeigt die neue Seite für die Ressource in Azure mit den zeitlichen Ablauf finden Sie die Web-App-Ressource, die hervorgehoben.](../media/3-new-web-app.png)

5. Klicken Sie auf die Schaltfläche **Erstellen**, um die Erstellung der Web-App zu starten.

    > [!NOTE]
    > Es dauert unter Umständen ein paar Sekunden, bis Ihre Web-App erstellt wurde und einsatzbereit ist.

Das Portal zeigt die Dashboardseite an und benachrichtigt Sie, sobald die Web-App erstellt wurde.

Wenn die App bereit ist, navigieren Sie im Azure-Portal zu der neuen App.

1. Klicken Sie im linken Navigationsbereich auf das Menü **Alle Ressourcen**. Die **alle Ressourcen** Seite listet alle Ressourcen, die Sie im Azure-Portal erstellt haben.

2. Klicken Sie sich durch den App Service BestBike, der soeben für Sie erstellt wurde.

    > [!NOTE]
    > Wenn Sie anhand des Namens BestBike nach Ihrer App suchen, finden Sie unter Umständen auch die Application Insights- und App Service-Plan-Ressourcen, die für Ihre neue Web-App erstellt wurden. Achten Sie darauf, dass Sie sich durch die Ressource vom Typ **App Service** klicken.

    ![Screenshot zeigt ein Beispiel für Suchergebnis innerhalb der Seite "alle Ressourcen" mit einem neu erstellten BestBike123 App Service-hervorgehoben.](../media/3-web-app.PNG)

Das Portal öffnet die Startseite des Web-App-Diensts mit dem Abschnitt **Übersicht**.

![Screenshot die BestBike App Service-Seite mit der URL-Link, der den Abschnitt "Übersicht" hervorgehoben angezeigt.](../media/3-web-app-home.PNG)

Klicken Sie rechts oben im Azure-Portal auf die **URL**, um eine Vorschau des Standardinhalts Ihrer neuen Web-App anzuzeigen. Wird eine Platzhalter-Webseite angezeigt, haben Sie die Web-App erfolgreich erstellt.
