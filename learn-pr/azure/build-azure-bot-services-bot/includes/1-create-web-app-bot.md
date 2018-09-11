### <a name="exercise-1-create-an-azure-web-app-bot"></a>Übung 1: Erstellen eines Bots für die Azure-Web-App

Der erste Schritt zum Erstellen eines Bots besteht darin, einen Standort anzugeben, an dem der Bot in Azure gehostet werden soll. [Azure-Web-Apps](https://azure.microsoft.com/services/app-service/web/) eignen sich bestens zum Hosten von Bot-Anwendungen, und Azure Bot Service ist dazu konzipiert, diese für Sie bereitzustellen. In dieser Übung verwenden Sie das Azure-Portal, um einen Bot für eine Azure-Web-App zu erstellen.

1. Öffnen Sie das [Azure-Portal](https://portal.azure.com) in Ihrem Browser. Wenn Sie aufgefordert werden, sich anzumelden, verwenden Sie dafür Ihr Microsoft-Konto.

1. Klicken Sie auf **+ Ressource erstellen**, klicken Sie anschließend auf **KI + Machine Learning** und dann auf **Web App Bot** (Web-App-Bot).
 
    ![Erstellen eines neuen Azure-Web-App-Bots](../images/new-bot-service.png)

    _Erstellen eines neuen Azure-Web-App-Bots_
  
1. Geben Sie einen Namen wie „qa-factbot“ in das Feld **App-Name** ein. *Dieser Name muss in Azure eindeutig sein, stellen Sie also sicher, dass ein grünes Häkchen daneben angezeigt wird.* Klicken Sie unter **Ressourcengruppe** auf **Neu erstellen**, und geben Sie den Ressourcengruppenname „factbot-rg“ ein. Wählen Sie den nächstgelegenen Standort aus, und wählen Sie den kostenlosen **F0**-Tarif aus. Klicken Sie dann auf **Botvorlage**.

    ![Konfigurieren des Azure-Web-App-Bots](../images/portal-start-bot-creation.png)

    _Konfigurieren des Azure-Web-App-Bots_

1. Wählen Sie **Node.js** als Sprache für das SDK und **Frage und Antwort** als Vorlagentyp aus. Klicken Sie dann unten auf dem Blatt auf **Auswählen**.   
  
    ![Auswählen der Sprache und der Vorlage](../images/portal-select-template.png)

    _Auswählen der Sprache und der Vorlage_

1. Klicken Sie nun auf **App Service-Plan/Standort**, klicken Sie dann auf **Neu erstellen**, und erstellen Sie einen App Service-Plan mit dem Namen „qa-factbot-service-plan“ oder einem ähnlichen Namen in der gleichen Region, die Sie in Schritt 3 ausgewählt haben. Klicken Sie danach unten auf dem Blatt „Web-App-Bot“ auf **Erstellen**, um die Bereitstellung zu starten. 

1. Klicken Sie auf dem Menüband auf der linken Seite des Portals auf **Ressourcengruppen**. Klicken Sie dann auf **factbot-rg**, um die Ressourcengruppe zu öffnen, die Sie für den Azure-Web-App-Bot erstellt haben. Warten Sie, bis „Wird bereitgestellt“ am oberen Rand des Blatts sich in „Erfolgreich“ ändert, was angibt, dass der Azure-Web-App-Bot erfolgreich bereitgestellt wurde. Die Bereitstellung beansprucht in der Regel zwei Minuten oder weniger. Klicken Sie hin und wieder am oberen Rand des Blatts auf **Aktualisieren**, um den Bereitstellungsstatus zu aktualisieren.

    ![Erfolgreiche Bereitstellung](../images/deployment-succeeded.png)

    _Erfolgreiche Bereitstellung_
  
Während der Bereitstellung des Azure-Web-App-Bots ist einiges im Hintergrund geschehen. Ein Bot wurde erstellt und registriert, eine [Azure-Web-App](https://azure.microsoft.com/services/app-service/web/) wurde erstellt, um diesen zu hosten, und der Bot wurde so konfiguriert, dass er mit [Microsoft QnA Maker](https://www.qnamaker.ai/) arbeitet. Der nächste Schritt besteht darin, QnA Maker zu verwenden, um eine Wissensdatenbank aus Fragen und Antworten zu erstellen, mit der Sie Intelligenz in den Bot einfügen.