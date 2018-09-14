Schließlich müssen wir unser Code an einer beliebigen Stelle in der Cloud zu hosten. Die Azure-Technologie, die an zu diesem Zweck verwenden, ist Azure Functions.

In diesem Vortrag lernen Sie Folgendes:

- Vorgehensweise: Erstellen einer Azure-Funktionen-App und `JavaScript` Http-Trigger.
- Informationen zum Ausführen und Debuggen einer Azure-Funktion lokal.

## <a name="create-an-azure-function-project"></a>Erstellen eines Azure Functions-Projekts

Ein Azure Functions-Projekt ist ein Container für mehrere Funktionen. Funktionen werden auf unterschiedliche Weise ausgelöst; Wir werden unsere Funktionen Auslösen von werden durch eine HTTP-Anforderung.

Es gibt viele Möglichkeiten zum Erstellen von Azure Functions. Wir werden die Verwendung von Visual Studio Code mit der Azure Functions-Erweiterung, die wir vorhin in diesem Modul installiert.

Zunächst erstellen wir unser Projekt-Funktion.

1. Typ <kbd>STRG</kbd>+<kbd>P</kbd> , öffnen Sie die befehlspalette, und klicken Sie dann zu suchen und auswählen `Azure Functions: Create New Project...`

   > **HINWEIS**
   >
   > Sie möglicherweise aufgefordert, wenn einige Dateien wie z. B. überschreiben möchten `.gitignore`, Antwort **keine** für alle!

   ![Erstellen eines neuen Projekts](/media-drafts/7.create-new-project.png)

2. Wählen Sie den Ordner, in dem die Funktions-app erstellen (die erste Option ist für den aktuellen Ordner) werden soll.

   ![Ordner auswählen](/media-drafts/7.select-folder.png)

3. Wählen Sie `JavaScript` als die gewünschte Sprache.

   ![Sprache auswählen](/media-drafts/7.select-language.png)

4. Wenn die oben genannten erfolgreich sollten Sie sehen die folgenden Dateien im Ordner erstellt

   ![Erstellten App](/media-drafts/7.app-created.png)

## <a name="create-an-azure-function"></a>Erstellen einer Azure Function

Nächster Schritt wir erstellen die Azure-Funktion selbst den Codeabschnitt, der auf eine HTTP-Anforderung reagiert.

Es werden wir der Visual Studio Code-Erweiterung verwenden.

1.  Typ <kbd>STRG</kbd>+<kbd>P</kbd> , öffnen Sie die befehlspalette, und klicken Sie dann zu suchen und auswählen `Azure Functions: Create Function...`

    ![Erstellen Sie neue Funktion](/media-drafts/7.create-function.png)

2.  Wählen Sie den Ordner, in dem Sie zuvor erstellt haben die Functions-Projekt (die erste Option ist für den aktuellen Ordner)

    ![Ordner auswählen](/media-drafts/7.select-current-project.png)

3.  Wir erstellen eine _HTTP-Trigger_, also wählen Sie diese Option.

    ![Ordner auswählen](/media-drafts/7.select-trigger.png)

4.  Geben Sie in `MojifyImage` als Namen für die Funktion, die Sie erstellen möchten

    ![Wählen Sie Namen](/media-drafts/7.choose-function-name.png)

5.  Wählen Sie `Anonymous` als die Authentifizierungsebene

    > Hinweis: durch Auswahl `Anonymous` die Funktion ist, öffnen Sie auf der ganzen Welt und unsichere.

    ![Wählen Sie Namen](/media-drafts/7.choose-auth-level.png)

## <a name="run-the-function-locally"></a>Lokales Ausführen der Funktion

Nachdem Sie diese Befehle erfolgreich abgeschlossen haben Sie das Startprojekt in ein funktionsprojekt mit konvertiert eine _HTTP-Trigger_ Funktion mit dem Namen `MojifyImage`.

Um sicherzustellen, dass alles funktioniert Sie können die Funktionen-app ausführen lokal wie folgt:

```bash
func host start
```

Dadurch wird die Funktion die Runtime lokal gestartet; Wenn alles richtig schließlich funktioniert sollte etwa wie der unten auf der Konsole ausgegeben:

```
Http Functions:

        MojifyImage: http://localhost:7071/api/MojifyImage
```

> **Hinweis**
>
> Dies ist einer der Vorteile bei der Installation von Azure Functions-Laufzeit, ermöglicht Sie uns, führen Sie die Funktion, die lokal mithilfe der gleichen zugrunde liegenden Technologie, die zum Ausführen der Funktion in der Produktion verwendet werden.

Um sicherzustellen, dass die Funktion ordnungsgemäß arbeitet, die URL, die in der Konsole ausgegeben, die dies ausgibt, in dem Browserfenster finden Sie unter:

![Funktionierende Funktionen-App](/media-drafts/7.default-function-app-working.png)

## <a name="debug-the-function-locally"></a>Die Funktion lokal Debuggen

> **Wichtig**
>
> Stellen Sie sicher, dass Sie beenden die `func host start` Befehl Sie gerade ausgeführt haben, bevor Sie versuchen, mithilfe von Visual Studio-Code debuggen.

Darüber hinaus können wir ausführen _und Debuggen von_ die Anwendung in visual Studio-Code.

Fügen Sie einen Haltepunkt auf der `index.js` -Datei am oberen Rand der JavaScript-Funktion wie folgt:

![Haltepunkt hinzufügen](/media-drafts/7.add-breakpoint.png)

Um die Funktion in der Debug-Modus zum ersten Mal besuchen auszuführen, klicken Sie im Menü Debuggen <kbd>Cmd<kbd> + <kbd>UMSCHALT<kbd> + <kbd>D<kbd>.

Wählen Sie dann `Attach to JavaScript Functions` aus der Debug-Konfiguration, bevor Sie schließlich auf das grüne Dreieck für die Debugsitzung zu starten.

> **Hinweis**
>
> Die `Attach to JavaScript Functions` Debug-Konfiguration wurde automatisch hinzugefügt, wenn Sie die Functions-Projekt erstellt haben.

Sie können alternativ drücken <kbd>F5<kbd> von an einer beliebigen Stelle in der Anwendung; dies ausgeführt wird die letzte Debug-Konfiguration.

Die `func host start` für Sie ausgeführt wird, ein Terminal sollten mit öffnen, schließlich dieselbe Ausgabe wie oben beschrieben:

```
Http Functions:

        MojifyImage: http://localhost:7071/api/MojifyImage
```

Da wir Debuggen Sie auch das Debuggen im Menü anzuzeigen, sehen wie folgt:

![Menüleiste "Debuggen"](/media-drafts/7.debug-menu-bar.png)

Nun, wenn Sie die obige URL finden Sie auf diese am Haltepunkt unterbrochen Sie angegeben haben, und Sie können über die Funktion.

<!-- TODO Find Link -->

Sie können [erfahren Sie mehr](https://code.visualstudio.com/docs/editor/debugging) zum Debuggen in Visual Studio Code
