An diesem Punkt ist die Anwendung eine funktionale Katalog, der Ihnen die Möglichkeit zum Hochladen und Anzeigen von Bildern. In diesem Modul erfahren Sie, wie Sie mit der maschinelles sehen-API von Microsoft Cognitive Services zum Generieren von Untertiteln für hochgeladene Bilder, und speichern die Beschriftungen der Image-Metadaten in Cosmos DB.

## <a name="create-a-computer-vision-account"></a>Erstellen Sie ein Konto für die maschinelles sehen

Microsoft Cognitive Services ist eine Sammlung von Diensten, die für Entwickler, um ihre Anwendungen intelligenter zu machen. Das Computer Vision-API ist ein serverlose Dienst, der Images, die mithilfe von erweiterten Algorithmen verarbeitet, und gibt Informationen über jedes Image zurück. Er verfügt über einen free-Tarif, der bis zu 5000-API-Aufrufe pro Monat bereitstellt.

1. Stellen Sie sicher, dass Sie immer noch in der Cloud Shell angemeldet sind. Wählen Sie andernfalls **EINGABETASTE fokusmodus** um eine Cloud Shell-Fenster zu öffnen. 

1. Erstellen eines neuen Cognitive Services-Kontos Art **ComputerVision** durch einen eindeutigen Namen in der Ressourcengruppe. Verwenden Sie für den free-Tarif, **F0** als SKU. Wenn Sie bereits ein vorhandenes Computer Vision-Konto verfügen, müssen Sie möglicherweise zum Erstellen eines Standard-Kontos (S1); Allerdings kann dies einige Kosten anfallen.

    ```azurecli
    az cognitiveservices account create -g first-serverless-app -n <computer vision account name> --kind ComputerVision --sku F0 -l westcentralus
    ```


## <a name="create-function-app-settings-for-computer-vision-url-and-key"></a>Erstellen von Funktionen-App-Einstellungen für Computer Vision-URL und Schlüssel

Zum Aufrufen der maschinelles sehen-API sind eine URL und den Schlüssel erforderlich.

1. Erhalten Sie das Computer Vision-API-Schlüssel und die URL zu, und speichern Sie sie in der Bash-Variablen.

    ```azurecli
    export COMP_VISION_KEY=$(az cognitiveservices account keys list -g first-serverless-app -n <computer vision account name> --query key1 --output tsv)
    ```
    ```azurecli
    export COMP_VISION_URL=$(az cognitiveservices account show -g first-serverless-app -n <computer vision account name> --query endpoint --output tsv)
    ```

1. Erstellen von Appeinstellungen, die mit dem Namen **COMP_VISION_KEY** und **COMP_VISION_URL**, in der Funktions-app.

    ```azurecli
    az functionapp config appsettings set -n <function app name> -g first-serverless-app --settings COMP_VISION_KEY=$COMP_VISION_KEY COMP_VISION_URL=$COMP_VISION_URL -o table
    ```


## <a name="call-computer-vision-api-from-resizeimage-function"></a>Rufen Sie die Computer Vision-API von ResizeImage-Funktion

In den folgenden Schritten ändern Sie die **ResizeImage** Funktion zum Aufrufen der maschinelles sehen-API zum Beschreiben jedes hochgeladene Bild aus, und speichern die Beschreibung in Cosmos DB.

1. Öffnen Sie Ihre Funktionen-app im Azure-Portal an.

1. **C#**

    1. (C#) Suchen Sie im linken Navigationsbereich mit der **ResizeImage** Funktion, und öffnen Sie das Codefenster.

    1. (C#) Ersetzen Sie den Code mit dem Inhalt der [ **/csharp/ResizeImage/run-module5.csx**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/csharp/ResizeImage/run-module5.csx). Dieser Code verwendet `HttpClient` Computer Vision-API aufrufen, und speichern das Ergebnis in Cosmos DB.

1. **JavaScript**

    1. (JavaScript) Diese Funktion erfordert die `axios` Paket von Npm, um die Computer Vision-API eine HTTP-aufrufen. Klicken Sie zum Installieren des Npm-Pakets klicken Sie auf der Funktions-App-Namen im linken Navigationsbereich, und klicken Sie auf **Plattformfeatures**.

    1. (JavaScript) Klicken Sie auf **Konsole** um ein Konsolenfenster anzuzeigen.

    1. (JavaScript) Führen Sie den Befehl `npm install axios` in der Konsole. Es dauert etwas, um den Vorgang abzuschließen.

    1. (JavaScript) Klicken Sie auf den Namen der Funktion (**ResizeImage**) im linken Navigationsbereich auf die Funktion anzuzeigen, und Ersetzen Sie alle **"Index.js"** mit dem Inhalt der [ **/javascript/ ResizeImage/Index-module5.js**](https://raw.githubusercontent.com/Azure-Samples/functions-first-serverless-web-application/master/javascript/ResizeImage/index-module5.js).

1. Klicken Sie auf **Protokolle** unter dem Codefenster, um den Bereich der Protokolle zu erweitern.

1. Klicken Sie auf **Speichern**. Überprüfen Sie im Bereich Protokolle, um sicherzustellen, dass die Funktion wurde erfolgreich gespeichert. keine Fehler vorliegen.


## <a name="test-the-application"></a>Testen der Anwendung

1. Öffnen Sie die Anwendung in einem Browser. Wählen Sie eine Bilddatei, und Laden Sie es hoch.

1. Nach einigen Sekunden sollte die Miniaturansicht des neuen Images auf der Seite angezeigt werden. Zeigen Sie auf das Bild, das die Beschreibung, die vom Computer Vision anzuzeigen.


## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie gelernt, wie Beschriftungen für jedes hochgeladene Bild mithilfe von Microsoft Cognitive Services-Computer Vision-API automatisch zu generieren. Als Nächstes erfahren Sie, wie Sie Authentifizierung mithilfe von Azure App Service-Authentifizierung zur Anwendung hinzufügen.