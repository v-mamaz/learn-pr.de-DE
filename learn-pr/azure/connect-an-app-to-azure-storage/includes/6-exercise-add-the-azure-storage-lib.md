::: zone pivot="csharp" Lassen Sie uns die Azure Storage-Clientbibliothek in Ihre .NET Core-Konsolenanwendung integrieren.

Die Azure Storage-Clientbibliothek für .NET wird mit NuGet verteilt. Nach Wunsch können Sie das Paket **WindowsAzure.Storage** Ihren .NET- oder .NET Core-Anwendungen hinzufügen.

## <a name="add-the-azure-storage-nuget-package"></a>Hinzufügen des NuGet-Pakets für Azure Storage

1. Wechseln Sie bei Verwenden von Cloud Shell zum richtigen Ordner.

1. Fügen Sie das Paket **WindowsAzure.Storage** der Anwendung hinzu.

    ```bash
    dotnet add package WindowsAzure.Storage
    ```

1. Dies sollte zu Konsolenaktivität führen, während die Clientbibliothek und alle erforderlichen Abhängigkeiten heruntergeladen werden. Sobald dies erledigt ist, können Sie einen Build für die App erstellen und sie erneut ausführen, um sicherzustellen, dass alles betriebsbereit ist.

    ```bash
    dotnet run
    ```

1. Wie zuvor sollte „Hello, World!“ ausgegeben werden.

::: zone-end

::: zone-pivot="javascript"

Nun wollen wir die **Microsoft Azure Storage-Clientbibliothek für Node.js und JavaScript** in Ihre Anwendung integrieren.

Die Clientbibliothek für Node.js steht über den Node Package Manager (npm) zur Verfügung. Fügen Sie das Paket **azure-storage** Ihrer Datei **packages.json** hinzu.

> [!NOTE]
> Die **Microsoft Azure Storage-Clientbibliothek für Node.js und JavaScript** ist für Serveranwendungen vorgesehen. Wenn Sie clientseitiges JavaScript verwenden, sollten Sie die **Azure Storage-Clientbibliothek für JavaScript** verwenden, die die gleiche Funktionalität bietet, aber auf die Ausführung in einem Browser ausgelegt ist.

## <a name="add-the-azure-storage-package"></a>Hinzufügen des Azure Storage-Pakets

1. Wechseln Sie bei Verwenden von Cloud Shell zum richtigen Ordner.

1. Fügen Sie das Paket **azure-storage** der Anwendung hinzu. Geben Sie unbedingt die Option `--save` an, damit ein Speichern in **packages.json** erfolgt.

    ```bash
    npm install azure-storage --save
    ```

1. Dies sollte zu Konsolenaktivität führen, während die Clientbibliothek und alle erforderlichen Abhängigkeiten heruntergeladen werden. Sobald dies erledigt ist, können Sie einen Build für die App erstellen und sie erneut ausführen, um sicherzustellen, dass alles betriebsbereit ist.

    ```bash
    node index.js
    ```

1. Wie zuvor sollte „Hello, World!“ ausgegeben werden.

::: zone-end

Nun, da wir über die notwendigen Bibliotheken verfügen, lassen Sie uns einen Blick auf die allgemeinen Aufgaben werfen, die Sie in Ihrem Code erledigen müssen, um mit Azure Storage zu arbeiten.
