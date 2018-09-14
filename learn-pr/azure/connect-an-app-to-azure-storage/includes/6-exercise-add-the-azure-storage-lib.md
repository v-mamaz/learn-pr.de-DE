::: zone pivot="csharp" integrieren wir die Azure Storage-Clientbibliothek in Ihrem .NET Core-Konsolenanwendung.

Die Azure-Speicher-Clientbibliothek für .NET wird mit NuGet verteilt. Sie werden die hinzufügen möchten die **WindowsAzure.Storage** Paket für Ihre .NET oder .NET Core-Anwendungen.

## <a name="add-the-azure-storage-nuget-package"></a>Hinzufügen des NuGet-Pakets für Azure Storage

1. In Cloud Shell `cd` in das Verzeichnis PhotoSharingApp, wenn Sie nicht bereits vorhanden sind.

1. Hinzufügen der **WindowsAzure.Storage** Paket in der Anwendung.

    ```bash
    dotnet add package WindowsAzure.Storage
    ```

1. Dies sollte in eine Konsole-Aktivität führen, während der Clientbibliothek und alle erforderlichen Abhängigkeiten heruntergeladen werden. Wenn dies abgeschlossen ist, fahren Sie fort, und erstellen Sie, und führen Sie die app erneut aus, um sicherzustellen, dass alles bereit ist.

    ```bash
    dotnet run
    ```

1. Wie zuvor sollten sie die "Hello World!" ausgeben.

::: zone-end

::: zone pivot="javascript"

Wir Integrieren der **Microsoft Azure Storage-Clientbibliothek für Node.js und JavaScript** in Ihre Anwendung.

Die Clientbibliothek für Node.js steht über den Node-Paket-Manager (NPM) zur Verfügung. Möchten Hinzufügen der **Azure Storage-** -Paket zu Ihrem **packages.json** Datei.

> [!NOTE]
> Die **Microsoft Azure Storage-Clientbibliothek für Node.js und JavaScript** ist für serveranwendungen vorgesehen. Wenn Sie clientseitige JavaScript-Code ausführen, sollten Sie verwenden die **Azure Storage Client Library für JavaScript**, was bietet dieselbe Funktionalität jedoch für die Ausführung in einem Browser zugeschnitten ist.

## <a name="add-the-azure-storage-package"></a>Fügen Sie das Azure Storage-Paket

1. In Cloud Shell `cd` in das Verzeichnis PhotoSharingApp, wenn Sie nicht bereits vorhanden sind.

1. Hinzufügen der **Azure Storage-** Paket in der Anwendung. Achten Sie darauf, geben Sie die `--save` option aus, damit er zum beibehalten **packages.json**.

    ```bash
    npm install azure-storage --save
    ```

1. Dies sollte in eine Konsole-Aktivität führen, während der Clientbibliothek und alle erforderlichen Abhängigkeiten heruntergeladen werden. Wenn dies abgeschlossen ist, fahren Sie fort, und erstellen Sie, und führen Sie die app erneut aus, um sicherzustellen, dass alles bereit ist.

    ```bash
    node index.js
    ```

1. Wie zuvor sollten sie "Hello, World!" ausgeben.

::: zone-end

Nun, da wir die erforderlichen Bibliotheken eingerichtet haben, sehen wir uns die allgemeinen Aufgaben, die Sie im Code, um mit Azure Storage Arbeiten erledigen.
