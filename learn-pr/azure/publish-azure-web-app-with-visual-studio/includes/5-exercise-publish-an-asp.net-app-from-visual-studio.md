Sie verfügen nun über eine lokal ausgeführte ASP.NET Core-Webanwendung. In dieser Einheit veröffentlichen Sie Ihre Anwendung in Azure App Service.

### <a name="visual-studio-for-windows"></a>Visual Studio für Windows

1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf Ihr Projekt, und wählen Sie **Veröffentlichen** aus.

1. Wählen Sie im angezeigten Dialogfeld auf der linken Seite **App Service** als Veröffentlichungsziel aus.  Zum Erstellen eines neuen App-Diensts wählen Sie rechts **Neu erstellen** aus.

1. Klicken Sie auf die Schaltfläche **Veröffentlichen**, um Ihren neuen App-Dienst zu erstellen.

> [!NOTE]
> Wenn Sie Ihre Apps bereitstellen, können Sie einen neuen App Service-Plan erstellen oder weiterhin Apps zu einem bestehenden Plan hinzufügen. Für diese Übung erstellen Sie eine neue **Azure App Service**-Instanz.

### <a name="visual-studio-mac"></a>Visual Studio für Mac

1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf Ihr Projekt.

1. Wählen Sie **Veröffentlichen** aus.

1. Klicken Sie auf **Veröffentlichen in Azure**. Dadurch wird eine Verbindung mit Ihrem Azure-Konto hergestellt. Es kann einige Minuten dauern, bis die Verbindung hergestellt ist und Ihre aktuellen Dienste aufgelistet sind.

1. Klicken Sie auf **Neu**, um einen neuen App-Dienst zu erstellen.

## <a name="configure-your-new-azure-app-service"></a>Konfigurieren Ihrer neuen Azure App Service-Instanz

1. Klicken Sie im Dialogfeld **App Service erstellen** auf **Konto hinzufügen**, und melden Sie sich bei Ihrem Azure-Abonnement an. Falls Sie bereits angemeldet sind, können Sie im Dropdownmenü das Konto mit dem gewünschten Abonnement auswählen.

1. Geben Sie die erforderlichen Informationen zu Ihrem App Service-Plan ein.

    ![Erstellen einer App Service-Instanz](../media-draft/5-CreateAppService.png)

    Geben Sie im Dialogfeld **App Service erstellen** folgende Informationen an:

    - **App-Name**: Dies ist der Name Ihrer Anwendung.  Mit ihm wird die URL der veröffentlichten Anwendung festgelegt, die https://_App-Name_.azurewebsites.net lauten wird.  Der eingegebene Wert muss eindeutig sein. Daher müssen Sie verschiedene Namen ausprobieren, um einen noch nicht reservierten Namen zu finden.

    - **Abonnement**: Das Azure-Abonnement, für das Sie den App-Dienst bereitstellen möchten.

    - **Ressourcengruppe**: Klicken Sie neben der Ressourcengruppe auf die Schaltfläche **Neu...**, und geben Sie einen eindeutigen Namen für die Ressourcengruppe ein.

        ![Neue Ressourcengruppe](../media-draft/5-NewResourceGroup.png)

    - **Hostingplan**: Der Hostingplan gibt den Standort, die Größe und die Funktionen der Webserverfarm an, die Ihre App hostet. Sie können einen vorhandenen Hostingplan auswählen oder einen neuen Plan erstellen. Für diese Übung erstellen Sie einen neuen Plan.

        Klicken Sie neben dem Hostingplan auf die Schaltfläche **Neu...** .

        ![Neuer Hostingplan](../media-draft/5-NewHostingPlan.png)

        Benennen Sie Ihren Hostingplan, und geben Sie dann den Speicherort und die Größe an.  
        
        > [!NOTE]
        > Die Angabe unterschiedlicher Standorte und Größen wirkt sich auf die Kosten für den Dienst aus. Für diese Übung wird empfohlen, die Größe auf **Free** festzulegen, um sicherzustellen, dass Ihnen keine Kosten entstehen.

    - **Application Insights**: Gibt an, ob Sie Application Insights für Ihre Anwendung verwenden möchten. Für diese Übung wird empfohlen, **None** (Keine) auszuwählen.

1. Klicken Sie auf die Schaltfläche **Erstellen**, um die Bereitstellung Ihres App-Diensts zu starten. Während der Bereitstellung wird der Fortschritt angezeigt:

    ![Fortschritt der Bereitstellung](../media-draft/5-DeployProgress.png)

1. Sobald der App-Dienst verfügbar ist, wird Visual Studio Ihre Web-App erstellen und bereitstellen.  In der von Visual Studio kompilierten Ausgabe wird die Ausgabe der Bereitstellung angezeigt.

    ![Veröffentlichen des Ergebnisses](../media-draft/5-PublishResult.png)

1. Herzlichen Glückwunsch, Ihre ASP.NET Core-Webanwendung ist nun veröffentlicht und online verfügbar. Sie können die endgültige URL für Ihre Website in der Buildausgabe und auch auf der Veröffentlichungsseite in Visual Studio sehen.

    ![Ergebnis der Veröffentlichung](../media-draft/5-PublishPage.png)

1. Um Ihre Website zu testen, öffnen Sie die angegebene URL.

    ![Livewebsite](../media-draft/5-WebPageLive.png)

## <a name="summary"></a>Zusammenfassung

Diese Übung veranschaulichte den Prozess der Bereitstellung einer Azure App Service-Instanz und einer ASP.NET Core-Webanwendung. Sie verfügen nun über eine Livewebanwendung.
