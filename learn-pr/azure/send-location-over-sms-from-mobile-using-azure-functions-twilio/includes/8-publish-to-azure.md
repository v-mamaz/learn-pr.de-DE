Die App und die Azure-Funktion sind nun vollständig und werden lokal ausgeführt. In dieser Einheit veröffentlichen Sie die Azure-Funktion in Azure, um diese in der Cloud auszuführen.

> In dieser Einheit veröffentlichen Sie Ihre Funktion über Visual Studio. Dies ist ein guter Einstieg in Proof of Concepts, Prototypen und zum Lernen. Für Apps mit Produktionsqualität sollten Sie diese Methode jedoch **nicht** verwenden. Sie sollte eine CI-basierte Bereitstellung verwenden. Weitere Informationen zu diesem Thema finden Sie in der [Dokumentation zur Bereitstellung von Azure-Funktionen](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment).
>
> [![Freunde lassen nicht zu, dass ihre Freunde per Rechtsklick veröffentlichen](../media/8-friends-dont-let-friends-publish.png)](https://damianbrady.com.au/2018/02/01/friends-dont-let-friends-right-click-publish/)

## <a name="publishing-your-app-to-azure"></a>Veröffentlichen der App in Azure

Azure-Funktionen können über Visual Studio in Azure veröffentlicht werden.

1. Beenden Sie die lokale Azure Functions-Runtime, wenn diese noch von der vorherigen Einheit ausgeführt wird.

2. Klicken Sie mit der rechten Maustaste auf die `ImHere.Functions`-App im Projektmappen-Explorer, und klicken Sie dann auf *Veröffentlichen...*.

    ![Veröffentlichen per Rechtsklick über die Funktions-App](../media/8-right-click-publish.png)

3. Klicken Sie im Dialogfeld **Veröffentlichungsziel auswählen** auf *Azure-Funktions-App*, und klicken Sie bei **Azure App Service** auf *Neu erstellen*. Klicken Sie auf **Veröffentlichen**.

    ![Erstellen eines neuen Azure App Service, in den veröffentlicht werden soll](../media/8-pick-publish-target.png)

4. Wählen Sie Ihr Azure-Konto aus der Dropdownliste in der oberen rechten Ecke aus, wenn Sie mehr als ein Azure-Konto besitzen und das richtige nicht ausgewählt ist.

5. Benennen Sie Ihre Funktions-App. Dieser Name muss für alle Funktions-Apps in Azure global eindeutig sein, also verwenden Sie einen Namen wie „ImHere-\<IhrName\>“.

6. Wählen Sie das Abonnement aus, unter dem Sie die Funktions-App erstellen möchten.

7. Erstellen Sie eine neue Ressourcengruppe für diese Funktions-App, indem Sie auf die Schaltfläche **Neu...** neben dem Dropdownmenü **Ressourcengruppe** klicken und dieser einen Namen wie „ImHere“ geben. Die Namen von Ressourcengruppen müssen nur in Ihrem Abonnement, nicht global in Azure eindeutig sein. Klicken Sie dann auf **OK**.

    ![Erstellen einer neuen Ressourcengruppe](../media/8-create-new-resource-group.png)

   Das Erstellen einer neuen Ressourcengruppe erleichtert später die Bereinigung. Sie können die Ressourcengruppe löschen und wissen, dass alle für die Funktions-App erstellten Elemente gleichzeitig gelöscht werden.

8. Erstellen Sie einen neuen Hostingplan, indem Sie auf die Schaltfläche **Neu...** neben dem Dropdownmenü **Hostingplan** klicken. Der Name des App Service-Plans wird standardmäßig auf den Namen Ihrer App mit „Plan“ am Ende festgelegt. Legen Sie den **Standort** auf den nächstgelegenen Standort fest, und stellen Sie sicher, dass **Größe** auf „Verbrauch“ festgelegt ist. Klicken Sie dann auf **OK**.

    ![Konfigurieren des Hostingplans](../media/8-configure-hosting-plan.png)

9. Erstellen Sie ein neues Speicherkonto, indem Sie auf die Schaltfläche **Neu...** neben dem Dropdownmenü **Speicherkonto** klicken. Ein Standardname wird bereitgestellt, also behalten Sie die Standardwerte bei, und klicken Sie auf **OK**.

    ![Speicherkonto erstellen](../media/8-create-storage-account.png)

10. Klicken Sie auf **Erstellen**, um alle Ressourcen in Azure bereitzustellen und Ihre Azure-Funktions-Apps bereitzustellen.

    ![Erstellen des App Service](../media/8-create-app-service.png)

Die Bereitstellung dauert einige Minuten. Folgende Ressourcen werden bereitgestellt:

* Ein Speicherkonto, um die Dateien zu speichern, die für die Azure-Funktions-App erforderlich sind
* Ein App Service-Plan, um die Computeressourcen zu verwalten, die für die Azure-Funktions-App erforderlich sind
* Der App Service, der die Azure-Funktion ausführt

Die Funktion wird nun veröffentlicht und kann über https://<Name_Ihrer_App>.azurewebsites.net/api/SendLocation abgerufen werden.

## <a name="configuring-your-app"></a>Konfigurieren der App

Als die Azure-Funktion lokal ausgeführt wurde, wurden Twilio-Anmeldeinformationen verwendet, die in einer `local.settings.json`-Datei gespeichert wurden. Wie der Name erkennen lässt, ist diese Datei für lokale Einstellungen, nicht für Azure-Einstellungen gedacht. Bevor die Azure-Funktion in Azure aufgerufen werden kann, müssen die Einstellungen `TwilioAccountSid` und `TwilioAuthToken` konfiguriert werden.

1. Klicken Sie in der Registerkarte „Veröffentlichen“ auf die Option **Anwendungseinstellungen verwalten**.

    ![Option „Anwendungseinstellungen verwalten“](../media/8-application-settings-option.png)

2. Klicken Sie auf die Schaltfläche **Hinzufügen**, um eine neue Einstellung hinzuzufügen. Nennen Sie diese „TwilioAccountSid“, und legen Sie den Wert auf die SID Ihres Twilio-Kontos fest. Wiederholen Sie diesen Schritt für Ihr Authentifizierungstoken, indem Sie den Namen „TwilioAuthToken“ verwenden.

    ![Festlegen der Twilio-Anmeldeinformationen in den Anwendungseinstellungen](../media/8-set-creds-in-app-settings.png)

3. Klicken Sie auf **OK**.

4. Klicken Sie auf **Veröffentlichen**, um die Azure-Funktions-App mit den neuen Anwendungseinstellungen erneut zu veröffentlichen.

    ![Schaltfläche „Veröffentlichen“](../media/8-publish-application-button.png)

## <a name="pointing-the-mobile-app-to-azure"></a>Verweisen der mobilen App auf Azure

1. Kopieren Sie die **Website-URL** von der Registerkarte „Veröffentlichen“ mithilfe der Schaltfläche zum Kopieren, die sich neben dem Wert befindet.

    ![Kopieren der Website-URL von der Registerkarte „Veröffentlichen“](../media/8-copy-site-url.png)

2. Öffnen Sie `MainViewModel` über das `ImHere`-Projekt.

3. Aktualisieren Sie den Wert des `baseUrl`-Felds, damit dieser der Website-URL entspricht, die Sie von der Registerkarte „Veröffentlichen“ kopiert haben.

4. Ändern Sie das Protokoll für diesen Wert von `http` in `https`. Die Website-URL wird immer mit HTTP bereitgestellt, Sie müssen jedoch HTTPS verwenden, um eine Azure-Funktion aufzurufen.

## <a name="test-it-out"></a>Testen

1. Legen Sie die `ImHere.UWP`-App als Start-App fest, und führen Sie diese aus.

2. Geben Sie eine Telefonnummer ein, und klicken Sie auf die Schaltfläche **Standort senden**.

3. Sie sollten den Standort als SMS-Nachricht erhalten.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie gelernt, wie Sie ein Azure Functions-Projekt über Visual Studio in Azure veröffentlichen und die Anwendungseinstellungen konfigurieren.