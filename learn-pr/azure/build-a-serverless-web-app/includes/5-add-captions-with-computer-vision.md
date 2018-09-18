An diesem Punkt hat die Anwendung den Status einer funktionierenden Galerie, die Ihnen das Hochladen und Anzeigen von Bildern ermöglicht. In diesem Modul wird beschrieben, wie Sie die Maschinelles Sehen-API von Microsoft Cognitive Services verwenden, um Titel für hochgeladene Bilder zu generieren und diese mit den Bildmetadaten in Azure Cosmos DB zu speichern.

## <a name="create-a-computer-vision-account"></a>Erstellen eines Kontos vom Typ „Maschinelles Sehen“

Microsoft Cognitive Services ist eine Sammlung von Diensten, mit denen Entwickler ihre Anwendungen um intelligente Funktionen und Features erweitern können. Die Maschinelles Sehen-API ist ein serverloser Dienst, der Bilder mithilfe von erweiterten Algorithmen verarbeitet und Informationen zu jedem Bild zurückgibt. Sie verfügt über einen kostenlosen Tarif, in dem bis zu 5.000 API-Aufrufe pro Monat möglich sind.

1. Stellen Sie sicher, dass Sie noch in Cloud Shell angemeldet sind. Klicken Sie andernfalls auf die Option **Enter focus mode** (Fokusmodus aktivieren), um ein Cloud Shell-Fenster zu öffnen. 

1. Erstellen Sie in Ihrer Ressourcengruppe ein neues Cognitive Services-Konto vom Typ **ComputerVision** mit einem eindeutigen Namen. Verwenden Sie für den kostenlosen Tarif **F0** als SKU. Falls Sie bereits über ein vorhandenes Konto vom Typ „Maschinelles Sehen“ verfügen, müssen Sie ggf. ein Standard-Konto (S1) erstellen. Hierfür können jedoch Kosten anfallen.

    ```azurecli
    az cognitiveservices account create -g first-serverless-app -n <computer vision account name> --kind ComputerVision --sku F0 -l westcentralus
    ```


## <a name="create-function-app-settings-for-computer-vision-url-and-key"></a>Erstellen von Funktions-App-Einstellungen für die Maschinelles Sehen-API und den Schlüssel

Sie benötigen eine URL und einen Schlüssel, um die Maschinelles Sehen-API aufrufen zu können.

1. Rufen Sie den Schlüssel und die URL für die Maschinelles Sehen-API ab, und speichern Sie diese Angaben in Bash-Variablen.

    ```azurecli
    export COMP_VISION_KEY=$(az cognitiveservices account keys list -g first-serverless-app -n <computer vision account name> --query key1 --output tsv)
    ```
    ```azurecli
    export COMP_VISION_URL=$(az cognitiveservices account show -g first-serverless-app -n <computer vision account name> --query endpoint --output tsv)
    ```

1. Erstellen Sie in der Funktions-App App-Einstellungen mit den Namen **COMP_VISION_KEY** und **COMP_VISION_URL**.

    ```azurecli
    az functionapp config appsettings set -n <function app name> -g first-serverless-app --settings COMP_VISION_KEY=$COMP_VISION_KEY COMP_VISION_URL=$COMP_VISION_URL -o table
    ```

## <a name="call-the-computer-vision-api-from-the-resizeimage-function"></a>Aufrufen der Maschinelles Sehen-API über die ResizeImage-Funktion

Wenn Sie die folgenden Schritte ausführen, ändern Sie die **ResizeImage**-Funktion, um die Maschinelles Sehen-API aufzurufen, um hochgeladene Bilder zu beschreiben und die Beschreibung in Azure Cosmos DB zu speichern.

1. Öffnen Sie Ihre Funktions-App im [Azure-Portal](https://portal.azure.com/?azure-portal=true).

::: zone pivot="csharp"
1. (C#) Verwenden Sie den Navigationsbereich auf der linken Seite, um nach der Funktion **ResizeImage** zu suchen und das zugehörige Codefenster zu öffnen.

1. (C#) Ersetzen Sie den Code durch den Inhalt der Datei [**/csharp/ResizeImage/run-module5.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/ResizeImage/run-module5.csx). In diesem Code wird `HttpClient` verwendet, um die Maschinelles Sehen-API aufzurufen und das Ergebnis in Azure Cosmos DB zu speichern.

::: zone-end

::: zone pivot="javascript"
1. (JavaScript) Für diese Funktion wird das `axios`-Paket aus npm benötigt, um einen HTTP-Aufruf an die Maschinelles Sehen-API zu senden. Klicken Sie zum Installieren des npm-Pakets im linken Navigationsbereich erst auf den Namen der Funktions-App und dann auf **Plattformfeatures**.

1. (JavaScript) Klicken Sie auf **Konsole**, um ein Konsolenfenster anzuzeigen.

1. (JavaScript) Führen Sie den Befehl `npm install axios` in der Konsole aus. Es kann einige Minuten dauern, bis der Vorgang abgeschlossen ist.

1. (JavaScript) Klicken Sie im Navigationsbereich auf der linken Seite auf den Funktionsnamen (**ResizeImage**), um die Funktion anzuzeigen. Ersetzen Sie den Inhalt der **index.js**-Datei durch den Inhalt der Datei [**/javascript/ResizeImage/index-module5.js**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/ResizeImage/index-module5.js).

::: zone-end

1. Klicken Sie unter dem Codefenster auf **Protokolle**, um den Protokollbereich zu erweitern.

1. Klicken Sie auf **Speichern**. Überprüfen Sie den Protokollbereich, um sicherzustellen, dass die Funktion erfolgreich gespeichert wird und keine Fehler aufgetreten sind.


## <a name="test-the-application"></a>Testen der Anwendung

1. Öffnen Sie die Anwendung in einem Browser. 

1. Wählen Sie eine Bilddatei aus, und laden Sie sie hoch.

1. Nach einigen Sekunden sollte die Miniaturansicht des neuen Bilds auf der Seite angezeigt werden. Zeigen Sie auf das Bild, um die von der Maschinelles Sehen-API generierte Beschreibung anzuzeigen.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie erfahren, wie Sie mithilfe der Maschinelles Sehen-API von Microsoft Cognitive Services die automatische Generierung von Bildtiteln für hochgeladene Bilder verwenden können. Als Nächstes wird beschrieben, wie Sie der Anwendung mithilfe der Azure App Service-Authentifizierung eine Authentifizierung hinzufügen.