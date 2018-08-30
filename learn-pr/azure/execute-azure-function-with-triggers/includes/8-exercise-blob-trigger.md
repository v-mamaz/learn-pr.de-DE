In dieser Übung erstellen Sie eine Azure-Funktion, die den Namen und die Größe eines Blobs beim Erstellen oder Aktualisieren anzeigt. 

> [!NOTE]
> Um diese Übung zu absolvieren, stellen Sie sicher, dass Sie im [Azure-Portal](https://portal.azure.com/) mit einem gültigen Konto angemeldet sind.

## <a name="create-a-blob-trigger"></a>Erstellen eines Blobtriggers

Verwenden Sie wieder Ihre vorhandene Azure Functions-Anwendung und fügen Sie einen Blobtrigger hinzu.

1. Zeigen Sie auf **Funktionen**, und wählen Sie das Pluszeichen (+) aus.

    ![Zeigen auf „Funktionen“ und Auswählen des Pluszeichens](../media-drafts/4-hover-function.png)

1. Wählen Sie **Blobtrigger** aus.

1. Wählen Sie **C#** als Sprache aus. 

1. Behalten Sie für **Name** den Standardwert bei.

1. Behalten Sie für **Pfad** den Standardwert bei.

1. Wählen Sie ein vorhandenes Azure Storage-Konto aus, oder wählen Sie **Erstellen** aus, wenn Azure ein neues Konto für Sie erstellen soll.

## <a name="download-storage-explorer"></a>Herunterladen des Storage-Explorers

Nun, da Sie einen Blobtrigger erstellt haben, laden Sie den Storage-Explorer herunter, mit dem Sie einfach ein Blob erstellen können.

- Laden Sie den [Storage-Explorer](http://storageexplorer.com) herunter.

## <a name="connect-to-your-azure-storage-account"></a>Verbinden mit dem Azure Storage-Konto

Der Storage-Explorer wurde heruntergeladen. Melden Sie sich mit den bereitgestellten Anmeldeinformationen an.

1. Wähen Sie im Storage-Explorer links das Pluszeichen (+) aus.

1. Wählen Sie **Speicherkontonamen und -schlüssel verwenden** aus.

1. Klicken Sie auf **Weiter**.

1. Wählen Sie in Azure unter Ihrem Blobtrigger **Integrieren** aus.

1. Wählen Sie **Dokumentation** aus, um die Ansicht zu erweitern.

1. Kopieren Sie den **Kontonamen** und den **Kontoschlüssel**.

1. Fügen Sie dann im Storage-Explorer den **Kontonamen** und den **Kontoschlüssel** ein.

1. Geben Sie einen **Anzeigenamen** ein. Dieser Wert ist der Name der Verbindung im Storage-Explorer.

1. Klicken Sie auf **Weiter**.

1. Wählen Sie **Verbinden**aus. 

## <a name="create-a-blob-container"></a>Erstellen eines Blobcontainers

Sie sind nicht mit Ihrem Azure Storage-Konto verbunden. Beachten Sie, dass der Blobtrigger nur den Speicherort überwacht, der im Feld **Pfad** beschrieben ist. Standardmäßig sollte der Pfad so aussehen:

> samples-workitems/{name}

Erstellen Sie einen Container mit dem Namen **samples-workitems**.

1. Erweitern Sie Ihr Speicherkonto im Storage Explorer. Der Name muss der **Anzeigename** sein, den Sie beim Verbinden angegeben haben.

1. Klicken Sie mit der rechten Maustaste auf **Blobcontainer** und wählen Sie **Blobcontainer erstellen** aus.

1. Geben Sie **samples-workitems** ein.

## <a name="turn-on-your-blob-trigger"></a>Aktivieren des Blobtriggers

Nachdem Sie einen Container zum Überwachen erstellt haben, führen Sie Ihre Funktion aus, um beim Erstellen eines Blobs die Ausgabe zu sehen.

1. Wählen Sie Ihren Blobtrigger aus, um den Codebildschirm zu öffnen.

1. Klicken Sie auf **Run** (Ausführen).

## <a name="create-a-blob"></a>Erstellen eines Blobs

Der Blobtrigger ist nun aktiviert und wartet auf Aktivität. Erstellen Sie ein Blob, um zu überprüfen, ob Sie eine Protokollmeldung erhalten.

1. Wählen Sie im Storage-Explorer den Container **samples-workitems** aus.

1. Wählen Sie die Option **Hochladen**. 

1. Wählen Sie **Dateien hochladen** aus.

1. Wählen Sie eine beliebige Datei auf Ihrem Computer aus.

1. Wählen Sie die Option **Hochladen**.

1. Kehren Sie zurück zu Azure. Überprüfen Sie Ihre Protokolle auf eine Meldung, die anzeigt, welche Datei hochgeladen wurde.

## <a name="clean-up"></a>Bereinigen

Um sicherzustellen, dass für diese Funktion keine Gebühren anfallen, wählen Sie über dem Protokollfenster **Anhalten** aus.

![Pause](../media-drafts/4-pause-timer.png)


