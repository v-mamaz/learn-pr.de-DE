Die Azure Cosmos DB-Erweiterung für Visual Studio Code vereinfacht das Erstellen von Konten, Datenbanken und Sammlungen, indem Ihnen das Erstellen von Ressourcen über das Befehlsfenster ermöglicht wird.

Im Rahmen dieser Einheit installieren Sie die Azure Cosmos DB-Erweiterung für Visual Studio, und verwenden diese dann zum Erstellen eines Kontos, einer Datenbank und einer Sammlung.

## <a name="install-the-azure-cosmos-db-extension-for-visual-studio"></a>Installieren der Azure Cosmos DB-Erweiterung für Visual Studio

1. Wechseln Sie zum [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-cosmosdb), und installieren Sie die Erweiterung **Azure Cosmos DB** für Visual Studio Code.

1. Wenn die Registerkarte der Erweiterung in Visual Studio Code geladen wird, klicken Sie auf **Installieren**.

1. Klicken Sie nach Abschluss der Installation auf **Erneut laden**.

    Visual Studio Code zeigt das ![Azure-Symbol](../media/2-setup/visual-studio-code-explorer-icon.png) Azure-Symbol auf der linken Seite des Bildschirms an, nachdem die Erweiterung installiert und neu geladen wurde.

## <a name="create-an-azure-cosmos-db-account-in-visual-studio-code"></a>Erstellen eines Azure Cosmos DB-Kontos in Visual Studio Code

[!include[](../../../includes/azure-sandbox-activate.md)]

1. Melden Sie sich in Visual Studio Code bei Azure an, indem Sie auf **Ansicht** > **Befehlspalette** klicken und **Azure: Sign In** eingeben. Damit Sie „Azure: Sign In“ verwenden können, muss die Erweiterung [Azure-Konto](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account) installiert sein.

    > [!IMPORTANT]
    > Melden Sie sich bei Azure mit dem Konto an, mit dem die Sandbox erstellt wurde. Die Sandbox ermöglicht den Zugriff auf ein Concierge-Abonnement.

    Führen Sie die Anweisungen aus, um den bereitgestellten Code zu kopieren und in den Webbrowser einzufügen, wodurch Ihre Visual Studio Code-Sitzung authentifiziert wird.

1. Klicken Sie im linken Menü auf das **Azure-Symbol** ![Azure-Symbol](../media/2-setup/visual-studio-code-explorer-icon.png). Klicken Sie anschließend mit der rechten Maustaste auf Ihr **Concierge-Abonnement** und danach auf **Konto erstellen**.

    Sollte das Concierge-Abonnement nicht angezeigt werden, vergewissern Sie sich, dass Sie sich in Visual Studio Code bei Azure mit dem Konto angemeldet haben, mit dem die Sandbox erstellt wurde. Falls Sie Ihre Azure-Abonnements in der Erweiterung „Azure-Konto“ gefiltert haben, vergewissern Sie sich außerdem, dass das Concierge-Abonnement im Befehl `> Azure: Select Subscriptions` aktiviert ist.

1. Klicken Sie auf die Schaltfläche __+__, um mit der Erstellung eines Cosmos DB-Kontos zu beginnen. Falls Sie über mehrere Abonnements verfügen, werden Sie aufgefordert, das gewünschte Abonnement auszuwählen.

1. Geben Sie im Textfeld im oberen Bereich des Bildschirms einen eindeutigen Namen für Ihr Azure Cosmos DB-Konto ein, und drücken Sie die EINGABETASTE. Der Kontoname darf nur Kleinbuchstaben, Zahlen und das Zeichen „-“ enthalten und muss zwischen 3 bis 31 Zeichen lang sein.

1. Klicken Sie als Nächstes auf **SQL (DocumentDB)** > **<rgn>[Sandbox-Ressourcengruppenname]</rgn>**, und wählen Sie einen Standort aus.

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

    In Visual Studio Code wird auf der Registerkarte „Ausgabe“ der Fortschritt der Kontoerstellung angezeigt. Der Vorgang kann einige Minuten dauern.

1. Nachdem das Konto erstellt wurde, erweitern Sie im Bereich **Azure Cosmos DB** Ihr Azure-Abonnement. Die Erweiterung zeigt nun das neue Azure Cosmos DB-Konto an. Im folgenden Bild heißt das Konto **learning-modules**.

    ![Azure Cosmos DB-Erweiterung in Visual Studio Code](../media/2-setup/azure-cosmos-db-vs-code-extension.png)

## <a name="create-an-azure-cosmos-db-database-and-collection-in-visual-studio-code"></a>Erstellen einer Azure Cosmos DB-Datenbank und -Sammlung in Visual Studio Code

Erstellen Sie nun eine neue Datenbank und Sammlung für Ihre Kunden.

1. Klicken Sie im Bereich „Azure Cosmos DB“ mit der rechten Maustaste auf Ihr neu erstelltes Konto, und klicken Sie dann auf **Datenbank erstellen**.
1. Geben Sie in der Eingabepalette im oberen Bereich des Bildschirms `Users` als Datenbankname ein, und drücken Sie die EINGABETASTE.
1. Geben Sie `WebCustomers` als Sammlungsname ein, und drücken Sie die EINGABETASTE.
1. Geben Sie `userId` als Partitionsschlüssel ein, und drücken Sie die EINGABETASTE.
1. Bestätigen Sie abschließend `1000` als anfängliche Durchsatzkapazität, und drücken Sie die EINGABETASTE.
1. Wenn Sie jetzt das Konto im Bereich **Azure: Cosmos DB** erweitern, werden die neue Datenbank **Users** und die Sammlung **WebCustomers** angezeigt.

    ![Animation zur Veranschaulichung der obigen Schritte in der Azure Cosmos DB-Erweiterung in Visual Studio Code.](../media/2-setup/vs-code-azure-cosmos-db-extension.gif)

Da Sie nun über ein Azure Cosmos DB-Konto verfügen, können Sie mit der Arbeit in Visual Studio Code beginnen.
