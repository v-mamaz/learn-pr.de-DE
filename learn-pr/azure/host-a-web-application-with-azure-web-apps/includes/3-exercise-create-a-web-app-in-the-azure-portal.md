In dieser Übung verwenden Sie das Azure-Portal, um eine Azure-Web-App zu erstellen.

## <a name="log-in-to-the-azure-portal"></a>Anmelden beim Azure-Portal

Im ersten Schritt melden Sie sich beim Azure-Portal an:

1. Öffnen Sie einen Browser, und navigieren Sie zum [Azure-Portal](https://portal.azure.com).
2. Melden Sie sich mit Ihren Anmeldeinformationen an.
3. Nach erfolgreicher Anmeldung gelangen Sie zum **Dashboard** oder zur Startseite des Azure-Portals.

    ![Azure-Portal](../media-draft/3-azure-portal.PNG)

## <a name="create-an-azure-web-app"></a>Erstellen einer Azure-Web-App

Lassen Sie uns, nachdem wir uns beim Azure Portal angemeldet haben, mithilfe der Vorlage eine Azure Web-App erstellen.

1. Klicken Sie links oben auf dem Bildschirm auf **+ Ressource erstellen**. Alle Elemente, die Sie in Azure erstellen, heißen Ressourcen.

    ![Azure Marketplace](../media-draft/3-market-place.PNG)

1. Sie gelangen im Portal zum Blatt **Marketplace**. Hier können Sie nach der Ressource suchen, die Sie erstellen möchten, oder eine der beliebten Ressourcen auswählen, die andere Benutzer im Azure-Portal erstellen.

1. Klicken Sie im Abschnitt **Beliebt** auf **Web-App**. Das Portal leitet Sie zum Blatt **Neue Web-App erstellen** weiter.

    ![Blatt „Neue Web-App erstellen“](../media-draft/3-create-new-web-app-page.PNG)

1. Wenn Sie eine neue Web-App erstellen, fordert das Azure-Portal für das Erstellen der App einige Informationen von Ihnen an. In diesem Abschnitt müssen Sie die folgenden grundlegenden Informationen angeben:

    1. **App-Name**: Ihr Kunde möchte die Anwendung benennen`BestBike`. Geben Sie den Namen in dieses Feld ein. Das Azure-Portal prüft und validiert die Verfügbarkeit des Web-App-Namens unter allen in Azure gehosteten Web-Apps, um sicherzustellen, dass niemand sonst den App-Namen `BestBike` gewählt hat.

    2. **Abonnement**: In diesem Feld müssen Sie in der Dropdownliste ein aktives Azure-Abonnement auswählen.

    3. **Betriebssystem**: In diesem Feld müssen Sie entscheiden, ob Sie zum Hosten Ihrer neuen Webanwendung **Windows** oder **Linux** verwenden möchten. Diese Einstellung wirkt sich direkt auf den App Service-Plan aus, den Sie unten auswählen oder erstellen. Zur Erinnerung: Ein App Service-Plan ähnelt einem virtuellen Computer, der ein Betriebssystem mit allen Ressourcen (CPU, RAM usw.) ist, die auf diesem Computer benötigt werden, um Ihre Anwendung auszuführen. In diesem Fall möchte Ihr Kunde die Web-App lieber über eine Windows-VM hosten. Wählen Sie daher **Windows** aus.

    4. **Application Insights**: Azure Application Insights hilft Ihnen bei der Erkennung und Diagnose von Qualitätsproblemen in Ihren Web-Apps und Webdiensten und erleichtert Ihnen zu verstehen, was Ihre Benutzer tatsächlich damit tun. Eine der Anforderungen Ihres Kunden ist die Fähigkeit, Berichte über den Datenverkehr, der über seine Website läuft, einzusehen und Trends zu untersuchen, wann der Datenverkehr hoch und wann niedrig ist. Wählen Sie in diesem Fall die Option **Ein**, um Application Insights für diese Web-App zu aktivieren. Nachdem Sie die Option **Ein** gewählt haben, müssen Sie auch den Standort bzw. die Region auswählen, in der die Application Insights-Daten gespeichert werden sollen. Beachten Sie, dass Application Insights nur in einer begrenzten Anzahl von Regionen verfügbar ist. Wählen Sie für diese Demo im Feld **Application Insights-Standort** die Region **USA, Osten** aus.

## <a name="create-a-new-resource-group"></a>Erstellen einer neuen Ressourcengruppe

Eine Azure-Web-App muss einer Ressourcengruppe angehören. Erstellen wir also eine, um alle zugehörigen Ressourcen zu gruppieren.

Wählen Sie die Option **Neu erstellen** aus (die standardmäßig ausgewählt ist). Beachten Sie, dass Azure bereits einen eindeutigen Ressourcengruppennamen für Sie generiert hat, der auf dem von Ihnen gewählten **App-Namen** basiert. Sie können wahlweise den Namen der Ressourcengruppe ändern oder den von Azure generierten Namen beibehalten. In diesem Fall behalten Sie den von Azure generierten Namen bei.

## <a name="create-an-app-service-plan"></a>Erstellen eines App Service-Plans

In diesem Feld müssen Sie einen App Service-Plan auswählen, mit dem die Anwendung ausgeführt werden soll. Standardmäßig wählt das Portal den letzten App Service-Plan aus, den Sie zuvor erstellt haben. Klicken Sie auf das Zeichen **>**, um zum Blatt **App Service-Plan** zu navigieren.

![Blatt „App Service-Plan“](../media-draft/3-create-app-service-plan.PNG)

Klicken Sie auf den Link **+ Neu erstellen**, um einen neuen App Service-Plan zu erstellen. Sie gelangen im Portal zum Blatt **Neuer App Service-Plan**. Das Portal fordert einige Informationen von Ihnen an, um den neuen App Service-Plan zu erstellen.

![Blatt „Neuer App Service-Plan“](../media-draft/3-new-app-service-plan.PNG)

1. **App Service-Plan**: In dieses Feld geben Sie einen eindeutigen Namen für den neuen App Service-Plan ein. Geben Sie den gleichen Web-App-Namen ein, den Sie oben gewählt haben, und fügen Sie das Suffix `-app-service-plan` hinzu, um diese Ressource leichter von anderen zu unterscheiden. Das Azure-Portal prüft und validiert die Verfügbarkeit des App Service-Plans unter allen in Azure gehosteten App Service-Plänen.

2. **Standort**: In diesem Feld müssen Sie die **Region** auswählen, in der sich dieser App Service-Plan befindet. Wählen Sie also den geografischen Ort, an dem gemäß dem App Service-Plan die virtuellen Computer eingerichtet werden, die für die Ausführung Ihrer Anwendung erforderlich sind. In diesem Fall können Sie eine beliebige Option in der Liste auswählen. Ihr Kunde möchte die Hostserver in der Nähe der Ostküste betreiben, wo die meisten seiner Kunden angesiedelt sind. Deshalb wählen Sie **USA, Osten** als Wert aus.

3. **Tarif**: In diesem Feld müssen Sie die Größe des virtuellen Computers auswählen, der zum Hosten Ihrer Anwendung dient. Klicken Sie auf das Zeichen **>**, um zum Blatt **Tarif** zu navigieren.

    ![Blatt „Tarif“](../media-draft/3-pricing-tier-blade.PNG)

    Hier stehen Ihnen zahlreiche Optionen zur Auswahl. Das Portal gruppiert diese Optionen anhand des Umfangs der benötigten Workload. Die drei verfügbaren Kategorien von Workloads sind „Dev/Test“, „Produktion“ und „App Service (isoliert)“. Je nach Anforderungen der Anwendung, die Sie in Azure hosten möchten, wählen Sie die entsprechende Workloadkategorie aus. Da die Anwendung `BestBike` sich gerade erst im Aufbau befindet, beginnen Sie mit der minimalen Workloadkategorie, die für Sie am besten geeignet ist. Denken Sie daran, dass eine der Anforderungen des Kunden die Möglichkeit war, alle neuen Änderungen, die an der Anwendung vorgenommen wurden, live zu testen. In den kommenden Einheiten werden Sie sehen, dass Sie zur Erfüllung dieser Anforderung **Bereitstellungsslots** hinzufügen müssen. Bereitstellungsslots sind nur im Mindesttarif **S1** verfügbar. Wählen Sie deshalb in der Kategorie **Produktionsworkload** den Tarif **S1** aus. Klicken Sie dann auf **Übernehmen**, um den Tarif zu bestätigen, den Sie oben ausgewählt haben.

    > Sie werden in diesem Modul feststellen, dass nur die Workloadkategorien **Produktion** und **App Service (isoliert)**  Ihnen erlauben, **Bereitstellungsslots** zu Ihrer Web-App hinzuzufügen.

Nun befinden Sie sich wieder auf dem Blatt **Neuer App Service-Plan**.

Klicken Sie auf **OK**.

Im Portal gelangen Sie zurück zum Hauptblatt **Web-App erstellen**.

![Blatt „Neue Web-App erstellen“ mit Daten](../media-draft/3-new-web-app-with-data.PNG)

Klicken Sie auf die Schaltfläche **Erstellen**, um die Erstellung der Web-App zu starten.

> Normalerweise dauert es einige Sekunden, bis das Azure-Portal Ihre Web-App erstellt und für Sie bereitstellt.

Das Portal leitet Sie zur Seite „Dashboard“ weiter und benachrichtigt Sie, sobald die Web-App erstellt wurde.

Wenn die App betriebsbereit ist, klicken Sie links auf dem Dashboard auf das Menü **Alle Ressourcen**. Auf dem Blatt **Alle Ressourcen** sind alle Ressourcen aufgelistet, die Sie im Azure-Portal erstellt haben.

Klicken Sie auf die Web-App, die Sie gerade erstellt haben. Sie gelangen im Portal zum Blatt „Web-App“.

![Blatt „Web-App“](../media-draft/3-web-app.PNG)

Im Portal wird die Startseite der Web-App geöffnet.

![Startseite der Web-App](../media-draft/3-web-app-home.PNG)

Klicken Sie rechts oben im Azure-Portal auf die **URL**. Wenn Sie eine Seite sehen, die der folgenden ähnlich ist, bedeutet dies, dass Sie die Web-App erfolgreich erstellt haben.

![Standardseite der Web-App](../media-draft/3-default-home-page.PNG)
