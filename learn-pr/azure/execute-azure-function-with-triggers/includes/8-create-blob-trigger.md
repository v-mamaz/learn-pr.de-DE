In dieser Einheit erfahren Sie, wie Sie eine Azure-Funktion erstellen, die den Namen und die Größe eines Blobs beim Erstellen oder Aktualisieren anzeigt.

## <a name="create-a-blob-trigger"></a>Erstellen eines Blobtriggers

Verwenden Sie wieder Ihre vorhandene Azure Functions-Anwendung, und fügen Sie einen Blobtrigger hinzu.

1. Stellen Sie sicher, dass Sie beim [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) mit dem gleichen Konto angemeldet sind, über das Sie die Sandbox aktiviert haben.

1. Navigieren Sie zur Anzeige **Alle Ressourcen**, und wählen Sie Ihre Funktions-App aus.

1. Zeigen Sie auf **Funktionen**, und klicken Sie auf das Pluszeichen (+).

1. Wählen Sie **Blobtrigger** aus.

1. Behalten Sie für **Name** den Standardwert bei.

1. Behalten Sie für **Pfad** den Standardwert bei.

1. Klicken Sie auf den _neuen_ Link neben dem Dropdownmenü **Speicherkontoverbindung**. Klicken Sie auf dem Blatt, das geöffnet wird, auf **Neu erstellen**. Geben Sie einen eindeutigen Namen für das neue Speicherkonto ein, und klicken Sie auf **OK**, um das Speicherkonto zu erstellen und den Bereich zu schließen.

1. Klicken Sie auf dem Bildschirm „Neue Funktion“ auf **Erstellen**, um die Funktion zu erstellen.

## <a name="create-a-blob-container"></a>Erstellen eines Blobcontainers

Nun, da wir einen Blobtrigger erstellt haben, verwenden wir den Storage-Explorer, um ein Blob zu erstellen und die Funktion auszulösen.

1. Öffnen Sie das verwendete (oder erstellte) Speicherkonto auf einer neuen Registerkarte.

    > [!TIP]
    > Sie können eine Registerkarte in den meisten Browsern duplizieren, indem Sie mit der rechten Maustaste auf sie klicken und aus dem Menü **Duplizieren** oder eine gleichwertige Option auswählen. Sie verwenden in diesem Fall eine neue Registerkarte, um während der Arbeit zwischen den beiden Diensten wechseln zu können.

1. Klicken Sie in der Randleiste auf **Speicherkonten**, oder klicken Sie dort alternativ auf **Alle Ressourcen**, und filtern Sie anschließend nach Name.

1. Klicken Sie auf den Abschnitt **Storage-Explorer (Vorschau)**, um ein neues Panel zu öffnen, in dem Sie mit Blobs und Dateien arbeiten können.

Beachten Sie, dass der Blobtrigger nur den Speicherort überwacht, der im Feld **Pfad** angegeben ist. Standardmäßig sollte der Pfad so aussehen:

> samples-workitems/{name}

Erstellen Sie nun einen Container mit dem Namen **samples-workitems**.

1. Klicken Sie mit der rechten Maustaste auf **BLOBCONTAINER** und anschließend auf **BLOB-Container erstellen**.

1. Geben Sie als Name **samples-workitems** ein, und behalten Sie für die Zugriffsebene die Standardeinstellung **Privat** bei. Klicken Sie anschließend auf **OK**.

## <a name="turn-on-your-blob-trigger"></a>Aktivieren des Blobtriggers

Nachdem Sie einen Container zum Überwachen erstellt haben, führen Sie nun Ihre Funktion aus, um beim Erstellen eines Blobs eine Ausgabe anzuzeigen.

1. Wechseln Sie zurück zur Browserregisterkarte mit Ihrer Azure-Funktion, oder öffnen Sie diese erneut.

1. Wählen Sie Ihren Blobtrigger aus, um den Codebildschirm zu öffnen.

1. Öffnen Sie im unteren Bildschirmbereich die Registerkarte **Protokolle**.

## <a name="create-a-blob"></a>Erstellen eines Blobs

Der Blobtrigger ist nun aktiviert und wartet auf Aktivität. Erstellen Sie ein Blob, um zu überprüfen, ob Sie eine Protokollmeldung erhalten.

1. Wechseln Sie zurück zur Browserregisterkarte mit dem Storage-Explorer.

1. Wählen Sie im Storage-Explorer den Container **samples-workitems** aus der Liste **BLOBCONTAINER** aus.

1. Klicken Sie in der Symbolleiste auf **Hochladen**.

1. Wählen Sie eine beliebige Datei auf Ihrem Computer aus.

1. Wählen Sie unter **Authentifizierungstyp** die Option **SAS** aus.

1. Klicken Sie auf **Hochladen**.

1. Wechseln Sie zurück zur Registerkarte „Azure-Funktion“, und suchen Sie in den Ausgabeprotokollen nach einer Meldung, die angibt, welche Datei hochgeladen wurde.