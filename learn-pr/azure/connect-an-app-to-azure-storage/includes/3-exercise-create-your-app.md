Zur Erinnerung: Wir arbeiten an einer Anwendung zum Teilen von Fotos, die Azure Storage verwendet, um Bilder und andere Daten zu verwalten, die wir im Auftrag unserer Benutzer speichern.

[!include[](../../../includes/azure-sandbox-activate.md)]

::: zone pivot="csharp"

Um dieses Szenario zu vereinfachen und uns auf die Storage-APIs konzentrieren zu können, erstellen wir eine neue .NET Core-Konsolenanwendung. Außerdem wird davon ausgegangen, dass diese immer über Netzwerkkonnektivität verfügt. Sie sollten Ihre App allerdings immer härten, um sicherzustellen, dass Netzwerkausfälle keine Auswirkungen auf die Benutzer haben oder zu Anwendungsfehlern führen.

## <a name="create-a-net-core-application"></a>Erstellen einer .NET Core-Anwendung

.NET Core ist eine plattformübergreifende Version von .NET, die unter macOS, Windows und Linux verwendet werden kann. Sie können die Tools lokal installieren oder Cloud Shell auf der rechten Seite des Fensters verwenden, um die folgenden Schritte auszuführen.

1. Melden Sie sich bei Cloud Shell an, oder öffnen Sie eine Befehlszeilensitzung, und erstellen Sie eine neue .NET Core-Konsolenanwendung namens „PhotoSharingApp“. Sie können das Flag `-o` oder `--output` hinzufügen, um die App in einem bestimmten Ordner zu erstellen.

    ```bash
    dotnet new console --name PhotoSharingApp
    ```

1. Führen Sie die App aus, um sich zu vergewissern, dass sie ordnungsgemäß erstellt und ausgeführt wird. Es sollte „Hello, World!“ in der Konsole angezeigt werden.

    ```bash
    cd PhotoSharingApp
    
    dotnet run
    ```
::: zone-end

::: zone pivot="javascript"

Um dieses Szenario zu vereinfachen und uns auf die Storage-APIs konzentrieren zu können, erstellen wir eine neue Node.js-Anwendung, die über die Konsole ausgeführt werden kann. Außerdem setzen wir voraus, dass sie immer über Netzwerkkonnektivität verfügt. Sie sollten Ihre App allerdings immer härten, um sicherzustellen, dass Netzwerkausfälle keine Auswirkungen auf die Benutzer haben oder zu Anwendungsfehlern führen.

## <a name="create-a-nodejs-application"></a>Erstellen einer Node.js-Anwendung

Node.js ist ein beliebtes Framework zum Ausführen von JavaScript-Apps. Es wird üblicherweise für Web-Apps verwendet, ist aber auch geeignet, um Logik über die Befehlszeile auszuführen. Wenn Sie die Tools lokal installiert haben, können Sie die folgenden Schritte über eine Befehlszeile ausführen. Alternativ können Sie Cloud Shell auf der rechten Seite des Fensters verwenden, um die folgenden Schritte auszuführen.

1. Melden Sie sich bei Cloud Shell an, oder öffnen Sie eine Befehlszeilensitzung, und erstellen Sie einen neuen Ordner namens „PhotoSharingApp“.

    ```bash
    mkdir PhotoSharingApp
    ```

1. Wechseln Sie in den neuen Ordner, und verwenden Sie `npm` zum Initialisieren einer neuen Node.js-App. Dadurch wird eine **package.json**-Datei mit Metadaten erstellt, die die App beschreiben.

    ```bash
    cd PhotoSharingApp
    npm init -y
    ```

1. Erstellen Sie eine neue Quelldatei namens **index.js** für unseren Code.

    ```bash
    touch index.js
    ```

1. Öffnen Sie die Datei **index.js** mit einem Editor. Bei Verwendung von Cloud Shell können Sie `code .` eingeben, um einen Editor zu öffnen.

1. Fügen Sie das folgende Programm in die Datei **index.js** ein. Hierzu können Sie die Tastenkombination **STRG+V** verwenden oder mit der rechten Maustaste klicken und „Einfügen“ auswählen.

    ```javascript
    #!/usr/bin/env node
    
    function main() {
        console.log('Hello, World!');
    }
    
    main();
    ```
1. Speichern Sie die Datei. (Hierfür können Sie das Menü „...“ rechts oben im Cloud Shell-Editor verwenden.)

1. Führen Sie die App aus, um sich zu vergewissern, dass sie ordnungsgemäß ausgeführt wird. Sie sollte „Hello, World!“ in der Konsole anzeigen.

    ```bash
    node index.js
    ```

::: zone-end