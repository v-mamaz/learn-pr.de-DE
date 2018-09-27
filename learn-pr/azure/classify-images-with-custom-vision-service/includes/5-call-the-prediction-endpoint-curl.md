In der letzten Übung haben Sie das trainierte Modell mithilfe des Features **Schnelltest** des Custom Vision Service-Portals getestet. Mit diesem Feature können Sie die Genauigkeit des Modells mit einigen Testbildern schnell überprüfen. Rufen Sie nun den Vorhersageendpunkt des Modells mehrmals über HTTP auf.

[!include[](../../../includes/azure-sandbox-activate.md)]

1. Wählen Sie anschließend in Ihrem *Artworks*-Projekt* im Custom Vision Service-Portal die Registerkarte **Leistung** aus.

    ![Auswählen der Registerkarte „Leistung“](../media/5-performance-tab.png)

1. Wählen Sie **Make default** (Als Standard festlegen), um sicherzustellen, dass es sich bei der aktuellen Iteration des Modells um die Standarditeration handelt.

1. Klicken Sie auf **Prediction URL** (Vorhersage-URL). Dadurch wird ein Dialogfeld mit den Informationen angezeigt, die für die Aufrufe erforderlich sind. 

    ![Anzeigen von Vorhersage-URL-Informationen](../media/5-portal-prediction-url.png)

    Wenn das Dialogfeld angezeigt wird, können Sie den Vorhersageendpunkt aufrufen und eine Bild-URL an ihn übergeben. Sie können im Anforderungstext auch ein unformatiertes Bild an den Endpunkt übergeben.

    Notieren Sie sich drei Informationen aus diesem Dialogfeld.
     - **Prediction-Key** (Vorhersageschlüssel): Dieser Schlüssel muss in allen Anforderungen als Header festgelegt werden. Damit erhalten Sie Zugriff auf den Endpunkt.
    - **Request URL** (Anforderungs-URL): Im Dialogfeld werden zwei verschiedene URLs angezeigt. Wenn Sie eine Bild-URL veröffentlichen, verwenden Sie die erste URL, die auf `/url` endet. Wenn Sie eine unformatierte Bilddatei im Anforderungstext bereitstellen möchten, verwenden Sie die zweite URL, die auf `/image` endet.
    - **Content-Type** (Inhaltstyp): Wenn Sie ein unformatiertes Bild veröffentlichen, legen Sie den Anforderungstext auf die binäre Darstellung des Bilds und den Inhaltstyp auf `application/octet-stream` fest. Wenn Sie eine Bild-URL veröffentlichen, fügen Sie sie als JSON-Code in den Anforderungstext ein, und legen Sie den Inhaltstyp auf `application/json` fest.
    

3. Kopieren und speichern Sie die erste URL und den `Prediction-Key`-Wert aus dem Dialogfeld **Verwenden der Vorhersage-API**. 

> [!TIP]
> **cURL** ist ein Befehlszeilentool, mit dem Dateien gesendet und empfangen werden können. Es ist in Linux, MacOS und Windows 10 enthalten und kann für die meisten anderen Betriebssysteme heruntergeladen werden. cURL unterstützt zahlreiche Protokolle wie HTTP, HTTPS, FTP, FTPS, SFTP, LDAP, TELNET, SMTP, POP3 usw. Weitere Informationen finden Sie unter den unten angegebenen Links:
>
>- <https://en.wikipedia.org/wiki/CURL>
>- <https://curl.haxx.se/docs/> 
> 
> cURL in der Sandbox von Azure Cloud Shell bereits installiert. Im nächsten Abschnitt dieser Übung werden Sie HTTP-Aufrufe an den Endpunkt senden.

2. Führen Sie den folgenden Befehl in Cloud Shell aus. Ersetzen Sie **[Endpunkt-URL]** durch die URL aus dem letzten Schritt. Ersetzen Sie **[Vorhersageschlüssel]** durch den Wert von `Prediction-Key`, den Sie im letzten Schritt gespeichert haben. 

    ```azurecli
    curl [endpoint-URL] \
    -H "Prediction-Key: [Prediction-Key]" \
    -H "Content-Type: application/json" \
    -d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/master/test-images/VanGoghTest_02.jpg'}" \
    | jq '.'
    ```

    Wenn der Befehl abgeschlossen ist, wird eine JSON-Antwort ähnlich der im folgenden Screenshot angezeigt. Die API gibt für jedes Tag im Modell eine Wahrscheinlichkeit zurück. Mit einer Wahrscheinlichkeit von fast 1 für den Wert `"painting"` **tagName** ist dieses Bild definitiv ein Gemälde. Es wurde jedoch von keinem der Künstler gemalt, mit denen Sie das Modell trainiert haben. 

    ![Miniaturansicht des Picasso-Testbilds](../media/5-prediction-json.png) 

3. Probieren Sie weitere Vorhersagen aus, indem Sie die URL im Anforderungstext durch die URLs in der folgenden Tabelle ersetzen. 

    |Bild  | URL  |
    |---------|---------|
    |![Miniaturansicht des Picasso-Testbilds](../media/picasso-test-02-thumb.jpg)     | `https://raw.githubusercontent.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/master/test-images/PicassoTest_02.jpg`        |
    |![Miniaturansicht des Rembrandt-Testbilds](../media/rembrandt-test-01-thumb.jpg)     |  `https://raw.githubusercontent.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/master/test-images/RembrandtTest_01.jpg`       |
    |![Miniaturansicht des Pollock-Testbilds](../media/pollock-test-01-thumb.jpg)  |   `https://raw.githubusercontent.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/master/test-images/PollockTest_01.jpg`     |
   

Der Vorhersageendpunkt funktioniert wie erwartet. Das Aufrufen der API ist so einfach wie das Senden einer HTTP-Anforderung an den Endpunkt mit einem Vorhersageschlüssel und einer Bild-URL.