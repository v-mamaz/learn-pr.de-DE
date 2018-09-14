Der erste Schritt zum Erstellen eines Bots besteht darin, einen Standort anzugeben, an dem der Bot in Azure gehostet werden soll. [Web-Apps](https://azure.microsoft.com/services/app-service/web/)-Funktion von Azure App Service eignet sich bestens zum Hosten von Bot-Anwendungen, und Azure Bot Service ist dazu konzipiert, diese für Sie bereitzustellen. In dieser Einheit verwenden Sie das Azure-Portal, um einen Bot für eine Azure-Web-App zu erstellen.

1. Öffnen Sie das [Azure-Portal](https://portal.azure.com/?azure-portal=true) in Ihrem Browser. Wenn Sie aufgefordert werden, sich anzumelden, verwenden Sie dafür Ihr Microsoft-Konto.

1. Klicken Sie auf **+ Ressource erstellen**, klicken Sie anschließend auf **KI und Machine Learning** und dann auf **Web-App-Bot**.
 
    ![Erstellen eines neuen Azure-Web-App-Bots](../media-draft/2-new-bot-service.png)

1. Geben Sie einen Namen wie „qa-factbot“ in das Feld **App-Name** ein. *Dieser Name muss in Azure eindeutig sein, stellen Sie also sicher, dass ein grünes Häkchen daneben angezeigt wird.* Klicken Sie unter **Ressourcengruppe** auf **Neu erstellen**, und geben Sie den Ressourcengruppennamen „factbot-rg“ ein. Wählen Sie den nächstgelegenen Standort aus, und wählen Sie den kostenlosen **F0**-Tarif aus. Klicken Sie dann auf **Botvorlage**.

    ![Konfigurieren des Azure-Web-App-Bots](../media-draft/2-portal-start-bot-creation.png)

1. Wählen Sie **Node.js** als Sprache für das SDK und **Frage und Antwort** als Vorlagentyp aus. Klicken Sie dann unten auf dem Blatt auf **Auswählen**.   
  
    ![Auswählen der Sprache und der Vorlage](../media-draft/2-portal-select-template.png)

1. Klicken Sie nun auf **App Service-Plan/Standort**, klicken Sie dann auf **Neu erstellen**, und erstellen Sie einen App Service-Plan mit dem Namen „qa-factbot-service-plan“ oder einem ähnlichen Namen in der gleichen Region, die Sie in Schritt 3 ausgewählt haben. Klicken Sie danach unten auf dem Blatt „Web-App-Bot“ auf **Erstellen**, um die Bereitstellung zu starten. 

1. Klicken Sie auf dem Menüband auf der linken Seite des Portals auf **Ressourcengruppen**. Klicken Sie anschließend auf **factbot-rg**, um die Ressourcengruppe zu öffnen, die Sie für den Azure-Web-App-Bot erstellt haben. Warten Sie, bis sich „Wird bereitgestellt“ am oberen Rand des Blatts in „Erfolgreich“ ändert. Dies gibt an, dass der Azure-Web-App-Bot erfolgreich bereitgestellt wurde. Die Bereitstellung beansprucht in der Regel zwei Minuten oder weniger. Klicken Sie hin und wieder am oberen Rand des Blatts auf **Aktualisieren**, um den Bereitstellungsstatus zu aktualisieren.

    ![Erfolgreiche Bereitstellung](../media-draft/2-deployment-succeeded.png)
  
Während der Bereitstellung des Azure-Web-App-Bots ist einiges im Hintergrund geschehen. Ein Bot wurde erstellt und registriert, eine [Azure-Web-App](https://azure.microsoft.com/services/app-service/web/) wurde erstellt, um diesen zu hosten, und der Bot wurde so konfiguriert, dass er mit [Microsoft QnA Maker](https://www.qnamaker.ai/) arbeitet. Der nächste Schritt besteht darin, QnA Maker zu verwenden, um eine Wissensdatenbank aus Fragen und Antworten zu erstellen, mit der Sie Intelligenz in den Bot einfügen.