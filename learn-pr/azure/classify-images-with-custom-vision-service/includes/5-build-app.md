Die wahre Leistungsstärke von Microsoft Custom Vision Service ist die Leichtigkeit, mit der Entwickler unter Verwendung der [Custom Vision Vorhersage-API](https://southcentralus.dev.cognitive.microsoft.com/docs/services/eb68250e4e954d9bae0c2650db79c653/operations/58acd3c1ef062f0344a42814) seine Intelligenz in ihre eigenen Anwendungen integrieren können. In dieser Einheit ändern Sie mit Visual Studio Code eine App namens „Artwork“, um das Modell zu verwenden, das Sie in vorhergehenden Übungen erstellt und trainiert haben.

1. Wenn Node.js nicht auf Ihrem System installiert ist, fahren Sie mit https://nodejs.org fort, und installieren Sie die neueste LTS-Version für Ihr Betriebssystem.

   > Wenn Sie nicht sicher sind, ob Node.js installiert ist, öffnen Sie eine Eingabeaufforderung oder ein Terminalfenster, und geben Sie **node -v** ein. Wenn Sie keine Node.js-Versionsnummer sehen, ist Node.js nicht installiert. Wenn eine ältere Version als 6.0 von Node.js installiert ist, sollten Sie unbedingt die neueste Version herunterladen und installieren.

1. Wenn Visual Studio Code nicht auf Ihrer Arbeitsstation installiert ist, fahren Sie mit http://code.visualstudio.com fort, und installieren Sie es jetzt.

1. Starten Sie Visual Studio Code, und wählen Sie **Ordner öffnen...** im Menü **Datei** aus. Wählen Sie im folgenden Dialogfeld den in den Modulressourcen enthaltenen Ordner „Client\Artworks“ aus.

    ![Auswahl des Ordners „Artworks“](../media-draft/5-fe-select-folder.png)

1. Öffnen Sie mit dem Befehl **Ansicht** > **Integriertes Terminal** in Visual Studio Code ein integriertes Terminalfenster. Führen Sie dann den folgenden Befehl in dem integrierten Terminal aus, um die von der App benötigten Pakete zu laden:

    ```
    npm install
    ```

1. Kehren Sie zum Projekt „Artwork“ im Custom Vision Service-Portal zurück, und klicken Sie auf **Leistung** und dann auf **Als Standard festlegen**, um sicherzustellen, dass die aktuelle Iteration des Modells die Standarditeration ist. 

    ![Angeben der Standarditeration](../media-draft/5-portal-make-default.png)

1. Bevor Sie die App ausführen und zum Aufrufen des Custom Vision Service verwenden können, muss sie geändert werden, um Endpunkt- und Autorisierungsschlüsselinformationen einzubeziehen. Zu diesem Zweck klicken Sie auf **Vorhersage-URL**.

    ![Anzeigen von Vorhersage-URL-Informationen](../media-draft/5-portal-prediction-url.png)

1. Im folgenden Dialogfeld werden zwei URLs aufgelistet: eine für das Hochladen von Bildern über die URL und eine weitere für das Hochladen lokaler Bilder. Kopieren Sie die Vorhersage-API-URL für Bilddateien in die Zwischenablage. 

    ![Kopieren der Vorhersage-API-URL](../media-draft/5-copy-prediction-url.png)

1. Kehren Sie zu Visual Studio Code zurück, und klicken Sie auf **predict.js**, um die Datei im Code-Editor zu öffnen.

    ![Öffnen von „predict.js“](../media-draft/5-vs-predict-file.png)

1. Ersetzen Sie „PREDICTION_ENDPOINT“ in Zeile 3 durch die URL in der Zwischenablage.

    ![Hinzufügen der Vorhersage-API-URL](../media-draft/5-vs-prediction-endpoint.png)

1. Kehren Sie zum Custom Vision Service-Portal zurück, und kopieren Sie den Vorhersage-API-Schlüssel in die Zwischenablage. 

    ![Kopieren des Vorhersage-API-Schlüssels](../media-draft/5-copy-prediction-key.png)

1. Kehren Sie zu Visual Studio Code zurück, und ersetzen Sie „PREDICTION_KEY“ in Zeile 4 von **predict.js** durch den API-Schlüssel in der Zwischenablage.

    ![Hinzufügen des Vorhersage-API-Schlüssels](../media-draft/5-vs-prediction-key.png)

1. Scrollen Sie in **predict.js** nach unten, und untersuchen Sie den Codeblock, der in Zeile 34 beginnt. Dies ist der Code, der mithilfe von AJAX den Custom Vision Service aufruft. Die Verwendung der Custom Vision-Vorhersage-API ist so einfach wie das Erstellen eines einfachen, authentifizierten POST an einem REST-Endpunkt.

    ![Aufruf einer Vorhersage-API](../media-draft/5-vs-code-block.png)

1. Kehren Sie zu dem integrierten Terminal in Visual Studio Code zurück, und führen Sie den folgenden Befehl zum Starten der App aus:

    ```
    npm start
    ```

1. Vergewissern Sie sich, dass die Artworks-App gestartet wird und ein Fenster wie dieses anzeigt:

    ![Die Artworks-App](../media-draft/5-app-startup.png)

„Artworks“ ist eine plattformübergreifende, in Node.js und [Electron](https://electron.atom.io/) geschriebene App. Daher kann sie unter Windows, macOS und Linux ausgeführt werden. In der nächsten Übung verwenden Sie sie, um Bilder nach den Künstlern zu klassifizieren, die sie gemalt haben.