In dieser Einheit erfahren Sie, wie Sie eine Azure-Funktion erstellen, die den Namen und die Größe eines Blobs beim Erstellen oder Aktualisieren anzeigt.

## <a name="create-a-blob-trigger"></a>Erstellen eines Blobtriggers

Verwenden Sie wieder Ihre vorhandene Azure Functions-Anwendung und fügen Sie einen Blobtrigger hinzu.

1. Melden Sie sich im [Azure-Portal](https://portal.azure.com?azure-portal=true) an.

1. Zeigen Sie auf **Funktionen**, und klicken Sie auf das Pluszeichen (+).

1. Klicken Sie auf **Benutzerdefinierte Funktion** und anschließend auf **Blobtrigger**.

1. Wählen Sie **C#** als Sprache aus.

1. Behalten Sie für **Name** den Standardwert bei.

1. Behalten Sie für **Pfad** den Standardwert bei.

1. Wählen Sie ein vorhandenes Azure Storage-Konto aus, oder klicken Sie auf **Erstellen**, wenn Azure ein neues Konto für Sie erstellen soll.

## <a name="create-a-blob-container"></a>Erstellen eines Blobcontainers

Nun, da wir einen Blobtrigger erstellt haben, verwenden wir den Storage-Explorer, um ein Blob zu erstellen und die Funktion auszulösen.

1. Öffnen Sie das verwendete (oder erstellte) Speicherkonto auf einer neuen Registerkarte. Eine einfache Möglichkeit hierzu besteht darin, eine neue Registerkarte im Azure-Portal zu öffnen und auf der Seitenleiste auf **Speicherkonten** zu klicken. Alternativ können Sie in der Seitenleiste auf **Alle Dienste** klicken und dann nach Namen filtern. Wir verwenden in diesem Fall eine neue Registerkarte, damit wir während der Arbeit zwischen den zwei Diensten wechseln können.

1. Klicken Sie auf den Abschnitt **Storage-Explorer (Vorschau)**, um ein neues Blatt zu öffnen, in dem Sie mit Blobs und Dateien arbeiten können.

Beachten Sie, dass der Blobtrigger nur den Speicherort überwacht, der im Feld **Pfad** angegeben ist. Standardmäßig sollte der Pfad so aussehen:

> samples-workitems/{name}

Wir müssen einen Container mit dem Namen **samples-workitems** erstellen.

1. Klicken Sie mit der rechten Maustaste auf **BLOBCONTAINER**, und wählen Sie **Blobcontainer erstellen** aus.

1. Geben Sie als Name **samples-workitems** ein, und behalten Sie für die Zugriffsebene die Standardeinstellung **Privat** bei.

## <a name="turn-on-your-blob-trigger"></a>Aktivieren Ihres Blobtriggers

Nachdem wir einen Container zum Überwachen erstellt haben, führen wir jetzt Ihre Funktion aus, um beim Erstellen eines Blobs eine Ausgabe anzuzeigen.

1. Wechseln Sie zurück zur Registerkarte der Azure-Funktion (um sie erneut zu öffnen).

1. Wählen Sie Ihren Blobtrigger aus, um den Codebildschirm zu öffnen.

1. Klicken Sie auf **Ausführen** – dadurch wird das Ausgabefenster angezeigt.

## <a name="create-a-blob"></a>Erstellen eines Blobs

Der Blobtrigger ist nun aktiviert und wartet auf Aktivität. Erstellen Sie ein Blob, um zu überprüfen, ob Sie eine Protokollmeldung erhalten.

1. Wählen Sie im Storage-Explorer den Container **samples-workitems** aus.

1. Klicken Sie auf der Symbolleiste auf **Hochladen**.

1. Wählen Sie eine beliebige Datei auf Ihrem Computer aus.

1. Klicken Sie auf **Hochladen**.

1. Wechseln Sie zurück zur Registerkarte der Azure-Funktion, und suchen Sie in den Ausgabeprotokollen nach einer Meldung, die anzeigt, dass die Datei hochgeladen wurde.