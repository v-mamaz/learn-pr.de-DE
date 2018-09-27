Die App und Azure-Funktion sind nun vollständig und werden lokal ausgeführt. In dieser Einheit veröffentlichen Sie die Funktion in Azure, um diese in der Cloud auszuführen.

> [!Note]
> Sie veröffentlichen Ihre Funktion über Visual Studio. Dies ist ein guter Einstieg in Proof of Concepts, Prototypen und zum Lernen. Für Apps mit Produktionsqualität sollten Sie diese Methode jedoch **nicht** verwenden. Sie sollte eine CI-basierte Bereitstellung verwenden. Weitere Informationen zu diesem Thema finden Sie in der [Dokumentation zur Bereitstellung von Azure-Funktionen](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment?azure-portal=true).

## <a name="publishing-your-app-to-azure"></a>Veröffentlichen der App in Azure

Azure-Funktionen können über Visual Studio in Azure veröffentlicht werden.

1. Beenden Sie die lokale Azure Functions-Runtime, wenn diese noch von der vorherigen Einheit ausgeführt wird.

1. Klicken Sie mit der rechten Maustaste auf die `ImHere.Functions`-App im Projektmappen-Explorer, und klicken Sie dann auf *Veröffentlichen...*.

    ![Veröffentlichen per Rechtsklick über die Funktions-App](../media/8-right-click-publish.png)

1. Klicken Sie im Dialogfeld **Veröffentlichungsziel auswählen** auf *Azure-Funktions-App*, und klicken Sie bei **Azure App Service** auf *Neu erstellen*. Klicken Sie auf **Veröffentlichen**.

    ![Erstellen eines neuen Azure App Service, mit dem veröffentlicht werden soll](../media/8-pick-publish-target.png)

1. Melden Sie sich mit Ihrem Benutzernamen und Kennwort auf der Registerkarte **Ressourcen** dieser Anweisungen bei Azure an. Wenn Sie diese App lokal und nicht auf einer VM erstellen, melden Sie sich mit Ihrem Azure-Konto an, und erstellen Sie bei Bedarf ein neues über die Links im Dialogfeld.

1. Übernehmen Sie in allen Feldern die Standardwerte, denn so wird die notwendige Infrastruktur zum Ausführen Ihrer Funktions-App erstellt.

1. Klicken Sie auf **Erstellen**, um alle Ressourcen in Azure bereitzustellen und Ihre Azure-Funktions-Apps zu veröffentlichen.

    ![Erstellen des App Service](../media/8-create-app-service.png)

1. Möglicherweise werden Sie gefragt, ob Sie die Azure Functions-Version in Azure aktualisieren möchten. Wenn dieses Dialogfeld angezeigt wird, wählen Sie **Ja** aus, um sicherzustellen, dass Ihre Funktions-App mit der neuesten Version der Azure Functions-Runtime veröffentlicht wird.
    ![Das Dialogfeld für das Update von Azure Functions](../media/8-update-functions-on-azure.png)

Die Bereitstellung dauert einige Minuten. Die folgenden Ressourcen werden bereitgestellt:

- Ein Speicherkonto, um die Dateien zu speichern, die für die Azure-Funktions-App erforderlich sind
- Ein App Service-Plan, um die Computeressourcen zu verwalten, die für die Azure-Funktions-App erforderlich sind
- Der App Service, der die Azure-Funktion ausführt

Die Funktion wird nun veröffentlicht und kann über **https://\<Name_Ihrer_App\>.azurewebsites.net/api/SendLocation** abgerufen werden.

## <a name="configuring-your-app"></a>Konfigurieren der App

Als die Azure-Funktion lokal ausgeführt wurde, wurden Twilio-Anmeldeinformationen verwendet, die in einer `local.settings.json`-Datei gespeichert wurden. Wie der Name erkennen lässt, ist diese Datei für lokale Einstellungen, nicht für Azure-Einstellungen gedacht. Bevor die Azure-Funktion in Azure aufgerufen werden kann, müssen die Einstellungen `TwilioAccountSid` und `TwilioAuthToken` konfiguriert werden.

1. Klicken Sie in der Registerkarte „Veröffentlichen“ auf die Option **Anwendungseinstellungen verwalten**.

    ![Option „Anwendungseinstellungen verwalten“](../media/8-application-settings-option.png)

1. Im Dialogfeld **Anwendungseinstellungen** werden die Anwendungseinstellungen mit einem lokalen und einem Remotewert angezeigt. Der lokale Wert stammt dabei aus Ihrer `local.settings.json`-Datei, und der Remotewert wird von Ihrer Funktion verwendet, wenn sie in Azure gehostet wird. Kopieren Sie die Werte aus dem Feld *Lokal* in das Feld *Remote* für die Werte **TwilioAccountSid** und **TwilioAuthToken**.

    ![Festlegen der Twilio-Anmeldeinformationen in den Anwendungseinstellungen](../media/8-set-creds-in-app-settings.png)

1. Klicken Sie auf **OK**. Dadurch werden die Werte in der Azure-Funktions-App veröffentlicht.

## <a name="pointing-the-mobile-app-to-azure"></a>Verweisen der mobilen App auf Azure

1. Kopieren Sie die **Website-URL** von der Registerkarte „Veröffentlichen“ mithilfe der Schaltfläche **In Zwischenablage kopieren**, die sich neben dem Wert befindet.

    ![Kopieren der Website-URL von der Registerkarte „Veröffentlichen“](../media/8-copy-site-url.png)

1. Öffnen Sie `MainViewModel` über das `ImHere`-Projekt.

1. Aktualisieren Sie den Wert des `baseUrl`-Felds auf die Website-URL, die Sie von der Registerkarte „Veröffentlichen“ kopiert haben.

## <a name="test-it-out"></a>Testen

1. Legen Sie die `ImHere.UWP`-App als Start-App fest, und führen Sie diese aus.

1. Geben Sie eine Telefonnummer ein, und klicken Sie auf die Schaltfläche **Standort senden**.

1. Sie sollten den Standort als SMS-Nachricht erhalten.

1. Wenn der Fehler *Dienst nicht verfügbar* zurückgegeben wird, überprüfen Sie, welche Version des NuGet-Pakets „Microsoft.Azure.WebJobs.Extensions.Twilio“ Ihre Funktions-App verwendet. Es sollte 3.0.0-rc1, nicht 3.0.0 sein.
1. Wenn der Fehler *Dienst nicht verfügbar* zurückgegeben wird, überprüfen Sie, welche Version des NuGet-Pakets „Microsoft.Azure.WebJobs.Extensions.Twilio“ Ihre Funktions-App verwendet. Es sollte 3.0.0-rc1, **nicht** 3.0.0 sein.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie gelernt, wie Sie ein Azure Functions-Projekt über Visual Studio in Azure veröffentlichen und die Anwendungseinstellungen konfigurieren.