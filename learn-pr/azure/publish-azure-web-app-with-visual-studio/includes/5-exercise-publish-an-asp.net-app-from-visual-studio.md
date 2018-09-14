Sie verfügen nun über eine lokal ausgeführte ASP.NET Core-Webanwendung. In dieser Einheit veröffentlichen Sie Ihre Anwendung in Azure App Service.

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

### <a name="visual-studio-for-windows"></a>Visual Studio für Windows

1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf Ihr Projekt, und wählen Sie **Veröffentlichen** aus.

1. Wählen Sie im angezeigten Dialogfeld auf der linken Seite **App Service** als Veröffentlichungsziel aus.  Wählen Sie auf der rechten Seite **neu erstellen** zum Erstellen einer App Service-app.

1. Klicken Sie auf die **veröffentlichen** klicken, um Ihre app zu erstellen.

> [!NOTE]
> Wenn Sie Ihre Apps bereitstellen, können Sie einen App Service-Plan erstellen oder weiterhin Apps zu einem bestehenden Plan hinzufügen. In dieser Übung erstellen Sie eine app im **Azure App Service**.

### <a name="visual-studio-mac"></a>Visual Studio für Mac

1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf Ihr Projekt.

1. Wählen Sie **Veröffentlichen** aus.

1. Klicken Sie auf **Veröffentlichen in Azure**. Dadurch wird eine Verbindung mit Ihrem Azure-Konto hergestellt. Es kann einige Minuten dauern, bis die Verbindung hergestellt ist und Ihre aktuellen Dienste aufgelistet sind.

1. Klicken Sie auf **neu** zum Erstellen einer app.

## <a name="configure-your-new-azure-app-service"></a>Konfigurieren Ihrer neuen Azure App Service-Instanz

1. Klicken Sie im Dialogfeld **App Service erstellen** auf **Konto hinzufügen**, und melden Sie sich bei Ihrem Azure-Abonnement an. Falls Sie bereits angemeldet sind, können Sie im Dropdownmenü das Konto mit dem gewünschten Abonnement auswählen.

1. Geben Sie die erforderlichen Informationen zu Ihrem App Service-Plan ein.

    ![Erstellen einer App Service-Instanz](../media-draft/5-CreateAppService.png)

    Geben Sie im Dialogfeld **App Service erstellen** folgende Informationen an:

    - **App-Name**: Dies ist der Name Ihrer Anwendung.  Mit ihm wird die URL der veröffentlichten Anwendung festgelegt, die https://_App-Name_.azurewebsites.net lauten wird.  Der eingegebene Wert muss eindeutig sein. Daher müssen Sie verschiedene Namen ausprobieren, um einen noch nicht reservierten Namen zu finden.

    - **Abonnement**: das Azure-Abonnement, die Sie die app bereitstellen möchten.

    - **Ressourcengruppe:** wählen Sie den vorhandenen <rgn>[Ressourcengruppennamen Sandkasten]</rgn> Ressourcengruppe aus.

    - **Hostingplan**: Der Hostingplan gibt den Standort, die Größe und die Funktionen der Webserverfarm an, die Ihre App hostet. Sie können einen vorhandenen Hostingplan auswählen oder einen Plan erstellen. In dieser Übung erstellen Sie eine.

        Klicken Sie neben dem Hostingplan auf die Schaltfläche **Neu...** .

        ![Neuer Hostingplan](../media-draft/5-NewHostingPlan.png)

        Benennen Sie Ihren Hostingplan, und geben Sie dann den Speicherort und die Größe an.  
        
        > [!NOTE]
        > Die Angabe unterschiedlicher Standorte und Größen wirkt sich auf die Kosten für den Dienst aus. Für diese Übung wird empfohlen, die Größe auf **Free** festzulegen, um sicherzustellen, dass Ihnen keine Kosten entstehen.

    - **Application Insights**: Gibt an, ob Sie Application Insights für Ihre Anwendung verwenden möchten. Für diese Übung wird empfohlen, **None** (Keine) auszuwählen.

1. Klicken Sie auf die **erstellen** Schaltfläche zum Starten der Bereitstellung Ihrer app. Während der Bereitstellung wird der Fortschritt angezeigt:

    ![Fortschritt der Bereitstellung](../media-draft/5-DeployProgress.png)

1. Nachdem die app bereitgestellt wurde, wird Visual Studio erstellen und Bereitstellen von Anwendungscode.  In der von Visual Studio kompilierten Ausgabe wird die Ausgabe der Bereitstellung angezeigt.

    ![Veröffentlichen des Ergebnisses](../media-draft/5-PublishResult.png)

1. Herzlichen Glückwunsch, Ihre ASP.NET Core-Webanwendung ist nun veröffentlicht und online verfügbar. Sie werden die endgültige URL für Ihre Website in der Buildausgabe sowie auf der Veröffentlichungsseite in Visual Studio angezeigt.

    ![Veröffentlichen des Ergebnisses](../media-draft/5-PublishPage.png)

1. Um Ihre Website zu testen, öffnen Sie die angegebene URL.

    ![Livewebsite](../media-draft/5-WebPageLive.png)

## <a name="summary"></a>Zusammenfassung

In dieser Übung veranschaulicht den Prozess der Bereitstellung einer app in Azure App Service und Bereitstellen einer ASP.NET Core-Webanwendung. Sie verfügen nun über eine Livewebanwendung.
