In dieser Übung erstellen Sie eine Azure-Funktion, die den Namen und die Größe eines Blobs beim Erstellen oder Aktualisieren anzeigt. 

> [!NOTE]
> Um diese Übung zu absolvieren, stellen Sie sicher, dass Sie im [Azure-Portal](https://portal.azure.com?azure-portal=true) mit einem gültigen Konto angemeldet sind.

## <a name="create-a-blob-trigger"></a>Erstellen eines Blobtriggers

Verwenden Sie wieder Ihre vorhandene Azure Functions-Anwendung und fügen Sie einen Blobtrigger hinzu.

1. Zeigen Sie auf **Funktionen**, und wählen Sie das Pluszeichen (+) aus.

    ![Auf „Funktionen“ zeigen und Pluszeichen auswählen](../media-drafts/4-hover-function.png)

2. Klicken Sie auf **Benutzerdefinierte Funktion** und anschließend auf **Blobtrigger**.

3. Wählen Sie **C#** als Sprache aus. 

4. Behalten Sie für **Name** den Standardwert bei.

5. Behalten Sie für **Pfad** den Standardwert bei.

6. Wählen Sie ein vorhandenes Azure Storage-Konto aus, oder klicken Sie auf **Erstellen**, wenn Azure ein neues Konto für Sie erstellen soll.

## <a name="create-a-blob-container"></a>Erstellen eines Blobcontainers

Nun, da wir einen Blobtrigger erstellt haben, verwenden wir den Storage-Explorer, um ein Blob zu erstellen und die Funktion auszulösen.

1. Öffnen Sie das verwendete (oder erstellte) Speicherkonto auf einer neuen Registerkarte. Eine einfache Möglichkeit hierzu besteht darin, eine neue Registerkarte im Azure-Portal zu öffnen und auf der Seitenleiste auf **Speicherkonten** zu klicken. Alternativ können Sie in der Seitenleiste auf **Alle Dienste** klicken und dann nach Namen filtern. Wir verwenden in diesem Fall eine neue Registerkarte, damit wir während der Arbeit zwischen den zwei Diensten wechseln können.

2. Klicken Sie auf den Abschnitt **Storage-Explorer (Vorschau)**, um ein neues Blatt zu öffnen, in dem Sie mit Blobs und Dateien arbeiten können.

Beachten Sie, dass der Blobtrigger nur den Speicherort überwacht, der im Feld **Pfad** angegeben ist. Standardmäßig sollte der Pfad so aussehen:

> samples-workitems/{name}

Wir müssen einen Container mit dem Namen **samples-workitems** erstellen.

3. Klicken Sie mit der rechten Maustaste auf **BLOBCONTAINER**, und wählen Sie **Blobcontainer erstellen** aus.

4. Geben Sie als Name **samples-workitems** ein, und behalten Sie für die Zugriffsebene die Standardeinstellung **Privat** bei.

## <a name="turn-on-your-blob-trigger"></a>Aktivieren Ihres Blobtriggers

Nachdem wir einen Container zum Überwachen erstellt haben, führen wir jetzt Ihre Funktion aus, um beim Erstellen eines Blobs eine Ausgabe anzuzeigen.

1. Wechseln Sie zurück zur Registerkarte der Azure-Funktion (um sie erneut zu öffnen).

2. Wählen Sie Ihren Blobtrigger aus, um den Codebildschirm zu öffnen.

3. Klicken Sie auf **Ausführen** – dadurch wird das Ausgabefenster angezeigt.

## <a name="create-a-blob"></a>Erstellen eines Blobs

Der Blobtrigger ist nun aktiviert und wartet auf Aktivität. Erstellen Sie ein Blob, um zu überprüfen, ob Sie eine Protokollmeldung erhalten.

1. Wählen Sie im Storage-Explorer den Container **samples-workitems** aus.

2. Klicken Sie auf der Symbolleiste auf **Hochladen**.

3. Wählen Sie eine beliebige Datei auf Ihrem Computer aus.

4. Klicken Sie auf **Hochladen**.

5. Wechseln Sie zurück zur Registerkarte der Azure-Funktion, und suchen Sie in den Ausgabeprotokollen nach einer Meldung, die anzeigt, dass die Datei hochgeladen wurde.

## <a name="pause-the-function"></a>Anhalten der Funktion

Um sicherzustellen, dass keine Gebühren für zusätzliche Anforderungen anfallen, können Sie über dem Protokollfenster auf **Anhalten** klicken.

![Anhalten der Funktion](../media-drafts/4-pause-timer.png)

