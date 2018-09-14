Denken Sie daran, dass wir eine Anwendung Fotos, die Azure-Speicher verwendet arbeiten, um Bilder und andere Teile der Daten für unsere Benutzer zu verwalten.

::: zone pivot="csharp"

Um dieses Szenario zu vereinfachen, damit wir uns auf die Storage-APIs konzentrieren können, erstellen wir eine neue .NET Core-Konsolenanwendung. Außerdem wird davon ausgegangen, dass sie immer über eine Netzwerkverbindung verfügt. Allerdings sollten Sie immer Absichern Ihrer app, um sicherzustellen, dass Netzwerkfehler keine Auswirkungen auf die Benutzeroberfläche oder zu einem Fehler der Anwendung selbst führt.

## <a name="create-a-net-core-application"></a>Erstellen einer .NET Core-Anwendung

.NET Core ist eine plattformübergreifende-Version von .NET, die unter MacOS, Windows und Linux ausgeführt wird. Sie können die Tools lokal installieren oder der Cloud Shell auf der rechten Seite des Fensters zum Ausführen der unten aufgeführten Schritte unten.

1. Melden Sie sich bei Cloud Shell ein, oder öffnen Sie eine Sitzung über die Befehlszeile, und erstellen Sie eine neue .NET Core-Konsolenanwendung mit dem Namen "PhotoSharingApp". Sie können hinzufügen, die `-o` oder `--output` Flag, um die app in einem bestimmten Ordner zu erstellen.

    ```bash
    dotnet new console --name PhotoSharingApp
    ```

1. Führen Sie die app aus, um sicherzustellen, dass es erstellt und ordnungsgemäß ausgeführt wird. Es sollte "Hello, World!" angezeigt. in der Konsole.

    ```bash
    cd PhotoSharingApp
    
    dotnet run
    ```
::: zone-end

::: zone pivot="javascript"

Um dieses Szenario zu vereinfachen, damit wir uns auf die Storage-APIs konzentrieren können, erstellen wir eine neue Node.js-Anwendung, die über die Konsole ausführen können. Außerdem wird davon ausgegangen, dass sie immer über eine Netzwerkverbindung verfügt. Allerdings sollten Sie immer Absichern Ihrer app, um sicherzustellen, dass Netzwerkfehler keine Auswirkungen auf die benutzerfreundlichkeit, oder führen zu einem Fehler der Anwendung selbst.

## <a name="create-a-nodejs-application"></a>Erstellen einer Node.js-Anwendung

Node.js ist ein beliebtes Framework für die Ausführung von JavaScript-apps. Es wird am häufigsten für Web-apps verwendet, jedoch können Sie es über die Befehlszeile sowie die Logik ausgeführt. Wenn Sie die Tools, die lokal installiert haben, können Sie die folgenden Schritte über die Befehlszeile ausführen. Alternativ können Sie Cloud Shell auch auf der rechten Seite des Fensters verwenden, zum Ausführen der folgenden Schritte aus.

1. Melden Sie sich bei Cloud Shell ein, oder öffnen Sie eine Sitzung über die Befehlszeile, und erstellen Sie einen neuen Ordner namens "PhotoSharingApp".

    ```bash
    mkdir PhotoSharingApp
    ```

1. Wechseln Sie in den neuen Ordner, und erstellen Sie eine **"Package.JSON"** Datei mit den Node Package Manager (NPM), die die neue app beschreiben.
    - Nennen Sie ihn "PhotoSharingApp".
    - Sie können die Standardwerte für alle weiteren aufforderungen nutzen.

    ```bash
    cd PhotoSharingApp
    npm init
    ```

1. Erstellen Sie eine neue Quelldatei **"Index.js"**, d.h., in unserem Code geht.

    ```bash
    touch index.js
    ```

1. Öffnen der **"Index.js"** -Datei mit einem Editor. Wenn Sie Cloud Shell verwenden, können Sie eingeben `code .` zum Öffnen eines Editors.

1. Fügen das folgende Programm in der **"Index.js"** Datei.

    ```javascript
    #!/usr/bin/env node
    
    function main() {
        console.log('Hello, World!');
    }
    
    main();
    ```
1. Speichern Sie die Datei&mdash;können Sie im Menü "..." auf der oberen rechten Ecke des Editors Cloud Shell.

1. Führen Sie die app aus, um sicherzustellen, dass sie ordnungsgemäß ausgeführt wird. Es sollte "Hello, World!" angezeigt. in der Konsole.

    ```bash
    node index.js
    ```

::: zone-end