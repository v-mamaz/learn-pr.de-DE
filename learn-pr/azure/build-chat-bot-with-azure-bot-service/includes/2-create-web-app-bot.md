> [!NOTE]
> Nachdem der virtuelle Computer gestartet wurde, finden Sie den Benutzernamen und das Kennwort zur Anmeldung auf der Registerkarte **Ressourcen** neben den Anweisungen.

Der erste Schritt zum Erstellen eines Bots besteht darin, einen Standort anzugeben, an dem der Bot in Azure gehostet werden soll. Das Web-Apps-Feature von Azure App Service eignet sich hervorragend zum Hosten von Botanwendungen. Azure Bot Service wurde so konzipiert, diese für Sie bereitzustellen. In dieser Einheit verwenden Sie das Azure-Portal, um einen Bot für eine Azure-Web-App zu erstellen.

1. Melden Sie sich beim Azure-Portal an, indem Sie https://portal.azure.com im Browser des virtuellen Computers öffnen.

1. Wählen Sie **+ Ressource erstellen**, dann **KI + Machine Learning**, und anschließend **Web-App-Bot**.

    ![Screenshot des Azure-Portals mit dem Blatt „Ressource erstellen“ und hervorgehobenem Ressourcentyp „Web-App-Bot“.](../media/2-new-bot-service.png)

1. Geben Sie einen Namen wie „qa-factbot“ in das Feld **App-Name** ein. *Dieser Name muss in Azure eindeutig sein. Stellen Sie also sicher, dass ein grünes Häkchen daneben angezeigt wird.*

1. Wählen Sie unter **Abonnement** und **Ressourcengruppe** die bereits vorhandenen Ressourcen.

1. Wählen Sie den nächstgelegenen Standort aus, und wählen Sie den Tarif **S1**.

1. Wählen Sie anschließend **Botvorlage**. Wählen Sie **SDK v3** als Version, **Node.js** als Sprache für das SDK und **Frage und Antwort** als Vorlagentyp aus. Klicken Sie dann unten auf dem Blatt auf **Auswählen**.

    ![Screenshot des Azure-Portals mit dem Blatt „Botvorlage“ und dem Erstellungsprozess des Bots, wobei Node.js als SDK-Sprache und Vorlagenoptionen für „Frage und Antwort“ hervorgehoben sind.](../media/2-portal-select-template.png)

1. Wählen Sie nun **App Service-Plan/Standort** und anschließend **Neu erstellen**, und erstellen Sie dann einen App Service-Plan mit dem Namen „qa-factbot-service-plan“ oder einem ähnlichen Namen in der gleichen Region, die Sie im vorherigen Schritt ausgewählt haben. Klicken Sie danach unten auf dem Blatt „Web-App-Bot“ auf **Erstellen**, um die Bereitstellung zu starten.

    ![Screenshot des Azure-Portals mit einem Beispielkonfigurationsblatt für einen neuen Web-App-Bot.](../media/2-portal-start-bot-creation.png)

    > [!NOTE]
    > Die Bereitstellung dauert in der Regel maximal zwei Minuten.

1. Nachdem die Bereitstellung abgeschlossen ist, klicken Sie im Menüband auf der linken Seite des Portals auf **Ressourcengruppen**.
1. Wählen Sie die bereits für diese Gruppe erstellte Ressourcengruppe aus, um die Ressourcengruppe zu öffnen, in der wir den Azure Web-App-Bot bereitgestellt haben.

Ihnen sollten nun verschiedene Ressourcen angezeigt werden, die für Ihren Azure Web-App-Bot erstellt wurden. Während der Bereitstellung des Azure-Web-App-Bots ist im Hintergrund Folgendes geschehen: Ein Bot wurde erstellt und registriert, eine [Azure-Web-App](https://azure.microsoft.com/services/app-service/web/) wurde erstellt, um diesen zu hosten, und der Bot wurde so konfiguriert, dass er mit [Microsoft QnA Maker](https://www.qnamaker.ai/) arbeitet. Der nächste Schritt besteht darin, QnA Maker zu verwenden, um eine Wissensdatenbank aus Fragen und Antworten zu erstellen, mit der Sie Intelligenz in den Bot einfügen.
