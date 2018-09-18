In der letzten Übung haben Sie ein Szenario implementiert, in dem es darum ging, Lesezeichen in einer Azure Cosmos DB-Datenbank nachzuschlagen. Dabei haben Sie eine Eingabebindung konfiguriert, um Daten aus der Lesezeichensammlung zu lesen. Dieses Szenario erweitern Sie nun, damit Sie auch Daten schreiben können. Betrachten Sie das folgende Flussdiagramm.

![Flussdiagramm zum Hinzufügen eines Lesezeichens zum Cosmos DB-Back-End](../media-draft/add-bookmark-flow-small.png)

In diesem Szenario empfangen Sie Anforderungen, um Ihrer Liste Lesezeichen hinzuzufügen. Die Anforderungen enthalten den gewünschten Schlüssel oder die gewünschte ID und die Lesezeichen-URL. Wie Sie auf dem Flussdiagramm sehen können, wird ein Fehler ausgegeben, wenn der Schlüssel bereits im Back-End vorhanden ist.

Wenn der übergebene Schlüssel *nicht* gefunden wird, wird das neue Lesezeichen der Datenbank hinzugefügt. Dabei könnten es Sie es an dieser Stelle theoretisch belassen, doch im Folgenden führen Sie noch einige zusätzliche Schritte aus.

Vielleicht ist Ihnen ein weiterer Prozess im Flussdiagramm aufgefallen. Bisher haben Sie Daten zwar empfangen, aber noch nicht verarbeitet. Die empfangenen Daten werden einfach in die Datenbank geschrieben. In einer echten Lösung würden Sie die Daten jedoch vermutlich verarbeiten. Diesen Vorgang könnten Sie in ein und derselben Funktion ausführen. In dieser Aufgabe wird jedoch ein Muster vorgestellt, mit dem der weitere Verarbeitungsprozess in eine andere Komponente bzw. Geschäftslogikeinheit ausgelagert wird.

Vermutlich fragen Sie sich, an welcher Stelle in Ihrem Lesezeichenszenario eine solche Auslagerung Sinn ergibt. Ein gutes Beispiel hierfür ist das Senden eines Lesezeichens an einen Erstellungsdienst für einen QR-Code. Dieser Dienst erstellt dann einen QR-Code für die URL, speichert das Bild im Blobspeicher und fügt die Adresse des Bilds in den Eintrag Ihrer Lesezeichensammlung ein. Der Aufruf eines Diensts zum Erstellen eines QR-Bilds ist zeitaufwendig. Anstatt also auf das Ergebnis zu warten, lagern Sie diesen Aufruf an eine Funktion aus, die asynchron arbeitet.

Azure Functions unterstützt nicht nur Eingabebindungen für verschiedene Integrationsquellen, sondern verfügt auch über mehrere Vorlagen für Ausgabebindungen, mit denen Sie Daten problemlos in Datenquellen schreiben können. Ausgabebindungen können auch in der Datei *function.json* konfiguriert werden.  Wie in dieser Übung noch deutlich wird, können Sie eine Funktion so konfigurieren, dass diese mit mehreren Datenquellen und Diensten zusammenarbeitet.


> [!IMPORTANT]
> Diese Übung baut auf der derjenigen der letzten Einheit auf. Das bedeutet, dass dieselbe Azure Cosmos DB-Datenbank und Eingabebindung verwendet werden. Wenn Sie die letzte Einheit nicht bearbeitet haben, wird empfohlen, dass Sie diese nachholen, bevor Sie mit der Aufgabe fortfahren.

## <a name="create-an-httptriggered-function"></a>Erstellen einer durch HTTP ausgelösten Funktion

1. Stellen Sie sicher, dass Sie beim Azure-Portal unter [https://portal.azure.com](https://portal.azure.com?azure-portal=true) mit demselben Azure-Konto angemeldet sind, das Sie bereits zuvor für dieses Modul verwendet haben.

2. Navigieren Sie im Azure-Portal zur Funktions-App, die Sie in diesem Modul erstellt haben.

3. Erweitern Sie die Funktions-App, zeigen Sie auf die Funktionssammlung, und klicken Sie anschließend auf die Schaltfläche „Hinzufügen“ (**+**) neben **Funktionen**. Durch diese Aktion wird der Vorgang der Funktionserstellung gestartet. Die folgende Animation veranschaulicht diese Aktion.

![Animation des Pluszeichens, das angezeigt wird, wenn der Benutzer mit der Maus auf das Menüelement „Funktionen“ zeigt](../media-draft/func-app-plus-hover-small.gif)

4. Auf der Seite werden alle aktuell unterstützten Trigger angezeigt. Wählen Sie **HTTP-Trigger** aus. Dies ist der erste Eintrag auf dem folgenden Screenshot.

![Screenshot eines Teils der Benutzeroberfläche zur Auswahl der Triggervorlage, wobei der HTTP-Trigger zuerst angezeigt wird (oben links in der Abbildung)](../media-draft/trigger-templates-small.PNG)

5. Füllen Sie das auf der rechten Seite angezeigte Dialogfeld **Neue Funktion** mit den folgenden Werten aus.

|Feld  |Wert  |
|---------|---------|
|Sprache     | **JavaScript**        |
|Name     |   [!INCLUDE [func-name-add](./func-name-add.md)]     |
| Autorisierungsstufe | **Funktion** |

5. Klicken Sie auf **Erstellen**, um die Funktion zu erstellen. Die Datei „index.js“ wird im Code-Editor geöffnet und zeigt eine Standardimplementierung der durch HTTP ausgelösten Funktion an.

In dieser Übung nutzen Sie aus Zeitgründen den *Code* und die *Konfiguration* aus der letzten Einheit als Startpunkt.

6. Ersetzen Sie den gesamten Code in „index.js“ durch den Code im folgenden Codeausschnitt. Klicken Sie anschließend auf **Speichern**, um die Änderung zu speichern. 

[!code-javascript[](../code/find-bookmark-single.js)]

Dieser Code kommt Ihnen vermutlich vertraut vor, was daran liegt, dass es sich um die Implementierung der [!INCLUDE [func-name-find](./func-name-find.md)]-Funktion handelt. Wie zu erwarten, funktioniert die Funktion noch nicht, da die gleichen Bindungen erst noch definiert werden müssen.  

7. Öffnen Sie die Datei *function.json* über die [!INCLUDE [func-name-find](./func-name-find.md)]-Funktion. Öffnen Sie dazu das Menü **Dateien anzeigen** rechts neben dem Code-Editor.

8. Kopieren Sie den gesamten Inhalt dieser Datei.

9. Öffnen Sie die Datei *function.json* über die [!INCLUDE [func-name-add](./func-name-add.md)]-Funktion.

10. Ersetzen Sie den Inhalt dieser Datei durch den Inhalt, den Sie aus der Datei *function.json* kopiert haben, die der [!INCLUDE [func-name-find](./func-name-find.md)]-Funktion zugeordnet ist. Anschließend sollte „function.json“ den folgenden JSON-Code enthalten.

```json
{
  "bindings": [
    {
      "authLevel": "function",
      "type": "httpTrigger",
      "direction": "in",
      "name": "req"
    },
    {
      "type": "http",
      "direction": "out",
      "name": "res"
    },
    {
      "type": "documentDB",
      "name": "bookmark",
      "databaseName": "func-io-learn-db",
      "collectionName": "Bookmarks",
      "connection": "unit3test_DOCUMENTDB",
      "direction": "in",
      "id": "{id}"
    }
  ],
  "disabled": false
}
```

11. Achten Sie darauf, alle Änderungen mithilfe von **Speichern** zu speichern.

In den vorherigen Schritten haben Sie Bindungen für die neue Funktion konfiguriert, indem Sie Bindungsdefinitionen aus einer anderen Funktion kopiert haben. Sie könnten eine neue Bindung natürlich auch über die Benutzeroberfläche erstellen. Es ist jedoch sinnvoll, sich bewusst zu werden, dass eine Alternative zur Verfügung steht.

## <a name="try-it-out"></a>Testen

1. Klicken Sie wie üblich rechts oben auf **</> Funktions-URL abrufen**, wählen Sie **Standard (Funktionsschlüssel)** aus, und klicken Sie dann auf **Kopieren**, um die URL der Funktion zu kopieren.

2. Fügen Sie die kopierte Funktions-URL in die Adressleiste Ihres Browsers ein. Fügen Sie den Wert der Abfragezeichenfolge `&id=docs` am Ende der URL hinzu, und drücken Sie die Taste `Enter` auf Ihrer Tastatur, um die Anforderung auszuführen. Wenn keine Fehler auftreten, sollte eine Antwort angezeigt werden, die eine URL zu dieser Ressource enthält.

An dieser Stelle ist es Zeit für einen kurzen Rückblick. Bisher haben Sie im Wesentlichen die Schritte der letzten Übung wiederholt. Das ist allerdings kein Problem, da hierdurch die Voraussetzungen für diese Übung geschaffen werden. Im Folgenden beginnen Sie mit einem neuen Schritt, nämlich dem Schreiben von Daten in die Datenbank. Hierzu benötigen Sie eine *Ausgabebindung*.

## <a name="define-azure-cosmos-db-output-binding"></a>Definieren einer Azure Cosmos DB-Ausgabebindung

Als Nächstes definieren Sie eine neue Ausgabebindung nicht über die Benutzeroberfläche, sondern durch das manuelle Aktualisieren der Konfigurationsdatei *function.json*. 

1. Öffnen Sie zum Aufrufen der Funktion die Datei **function.json** im Editor, indem Sie diese aus der Liste **Dateien anzeigen** auswählen.

2. Kopieren Sie in dieser Datei die Bindung mit dem Namen `bookmark`.

3. Platzieren Sie den Cursor direkt nach der schließenden geschweiften Klammer, die sich unmittelbar vor der schließenden eckigen Klammer befindet. Fügen Sie ein Komma `,` hinzu, und fügen Sie die kopierte Bindung hier ein. Die Konfigurationsdatei *function.json* sollte nun wie folgt aussehen.

[!code-json[](../code/config-new-entry.json?highlight=22-31)]

4. Bearbeiten Sie die eingefügte Bindung, indem Sie die folgenden Änderungen vornehmen.


|Eigenschaft   |Alter Wert  |Neuer Wert  |
|---------|---------|---------|
|Name     |   Lesezeichen      |  **newbookmark**       |
|direction     |   in      |   **out**      |
|id     |      {id}   |   **Löschen Sie diese Eigenschaft. Sie ist nicht für die Ausgabebindung vorhanden.**      |

Nachdem Sie diese Änderungen vorgenommen haben, enthält die Datei folgenden JSON-Code.

[!code-json[](../code/config-q-complete.json?highlight=22-30)]

Anhand eines kurzen Beispiels haben Sie gesehen, wie Bindungen auch direkt in der Konfigurationsdatei erstellt werden können. Dies ist hier sinnvoll, da Sie die Eigenschaften `databaseName`, `collectionName` und `connection` einer anderen Bindung wiederverwenden. Diese Eigenschaften haben Sie bereits für die Cosmos DB-Eingabebindung konfiguriert.

> [!NOTE]
> Der tatsächliche Wert von `connection` in der obigen JSON-Datei entspricht dem Namen, der der Verbindung bei deren Erstellung zugewiesen wurde.

Bevor Sie ihren Code aktualisieren, fügen Sie eine weitere Bindung hinzu, mit der Sie Nachrichten an die Warteschlange senden können.

## <a name="define-azure-queue-storage-output-binding"></a>Definieren einer Azure Queue Storage-Ausgabebindung

Azure Queue Storage ist ein Dienst zur Speicherung von Nachrichten, auf die von jedem Ort der Welt aus zugegriffen werden kann. Eine einzelne Nachricht kann bis zu 64 KB groß sein, und eine Warteschlange kann Millionen von Nachrichten enthalten. Die maximale Anzahl ist nur durch die Kapazität des Speicherkontos begrenzt. Das folgende Diagramm enthält einen allgemeinen Überblick über die Verwendung der Warteschlange in Ihrem Szenario.

![Diagramm, auf dem das Konzept einer Warteschlange und zwei Funktionen dargestellt werden, die Nachrichten mithilfe von Push der Warteschlange hinzufügen und per Pop aus dieser entfernen](../media-draft/q-logical-small.png)

Deutlich wird hier, dass die neue Funktion [!INCLUDE [func-name-add](./func-name-add.md)] der Warteschlange Nachrichten hinzufügt. Eine weitere Funktion (beispielsweise eine fiktive Funktion mit dem Namen *gen-qr-code*) entfernt Nachrichten per Pop aus derselben Warteschlange und verarbeitet die Anforderung.  Da Nachrichten über [!INCLUDE [func-name-add](./func-name-add.md)] in die Warteschlange geschrieben (mithilfe von *Push* übertragen) werden, fügen Sie Ihrer Lösung eine neue Ausgabebindung hinzu. Dieses Mal erstellen Sie die Bindung über die Benutzeroberfläche.

1. Klicken Sie im Funktionsmenü auf der linken Seite auf **Integrieren**, um die Registerkarte „Integration“ zu öffnen.

2. Klicken Sie unter der Spalte **Ausgaben** auf die Option **+ New Output** (+ Neue Ausgabe). Eine Liste aller möglichen Ausgabebindungstypen wird angezeigt.

3. Klicken Sie in der Liste zuerst auf **Azure Queue Storage** und anschließend auf die Schaltfläche **Auswählen**. Hierdurch wird die Ausgabekonfigurationsseite für Azure Queue Storage geöffnet.

Als Nächstes richten Sie eine Verbindung mit dem Speicherkonto ein. Dort wird Ihre Warteschlange gehostet.

4. Klicken Sie im Feld mit dem Namen **Speicherkontoverbindung** auf dieser Seite rechts neben dem leeren Feld auf *Neu*. Dadurch wird das Auswahldialogfeld **Speicherkonto** geöffnet. 

5. Zu Beginn dieses Moduls wurde zusammen mit der Funktions-App ein Speicherkonto erstellt. Wählen Sie dieses nun im Dialogfeld aus. Das Feld **Speicherkontoverbindung** wird mit dem Namen der Verbindung aufgefüllt. Wenn Sie sich den Wert der Verbindungszeichenfolge ansehen möchten, klicken Sie auf **Wert anzeigen**.

6. Sie könnten zwar für alle anderen Felder auf dieser Seite die jeweiligen Standardwerte übernehmen, jedoch ergeben sich sinnvollere Eigenschaften, wenn Sie die folgenden Felder ändern.


|Eigenschaft  |Alter Wert  |Neuer Wert  | Beschreibung |
|---------|---------|---------|---------|
|Warteschlangenname     |    outqueue     |  **bookmarks-post-process**      | Hierbei handelt es sich um den Namen der Warteschlange, der Lesezeichen hinzugefügt werden. Diese können dann von einer anderen Funktion weiterverarbeitet werden. |
| Name des Nachrichtenparameters    |  outputQueueItem       |   **newmessage**      | Hierbei handelt es sich um die Bindungseigenschaft, die Sie im Code verwenden werden. |


7. Achten Sie darauf, Ihre Änderungen mit einem Klick auf **Speichern** zu speichern.

## <a name="update-function-implementation"></a>Aktualisieren der Funktionsimplementierung

Sie haben nun alle Bindungen für die [!INCLUDE [func-name-add](./func-name-add.md)]-Funktion eingerichtet. Als Nächstes verwenden Sie diese in Ihrer Funktion.

1.  Klicken Sie auf die Funktion ([!INCLUDE [func-name-add](./func-name-add.md)]), um *index.js* im Code-Editor zu öffnen.

2. Ersetzen Sie den gesamten Code in „index.js“ durch den Code im folgenden Codeausschnitt.

[!code-javascript[](../code/add-bookmark.js)]

Im Folgenden wird beschrieben, welchen Zweck der Code erfüllt.

* Da die Funktion Ihre Daten ändert, ist zu erwarten, dass es sich um eine HTTP-POST-Anforderung handelt und die Lesezeichendaten Teil des Anforderungstexts sind.
* Über die Cosmos DB-Eingabebindung wird versucht, ein Dokument oder Lesezeichen mithilfe der empfangenen `id` abzurufen. Wird ein Eintrag gefunden, wird das `bookmark`-Objekt festgelegt. Mit der Bedingung `if(bookmark)` wird überprüft, ob ein Eintrag gefunden wurde.
* Sie können der Datenbank ganz einfach ein Lesezeichen hinzufügen. Hierzu legen Sie nur den `context.bindings.newbookmark`-Bindungsparameter auf den neuen Lesezeicheneintrag fest, den Sie als JSON-Zeichenfolge erstellt haben.
* Wenn Sie den Parameter `context.bindings.newmessage parameter` festlegen, können Sie außerdem problemlos Nachrichten an Ihre Warteschlange übermitteln.

> [!NOTE]
> Diese Ergebnisse konnten Sie einfach durch das Erstellen einer Warteschlangenbindung erzielen. Die Warteschlange musste nicht explizit erstellt werden. Hieran wird erkennbar, wie leistungsfähig Bindungen sind. Anhand des folgenden Popups wird deutlich, dass die Warteschlange automatisch erstellt wird, fall sie noch nicht vorhanden ist.

![Screenshot mit Popup, in dem darauf hingewiesen wird, dass die Warteschlange automatisch erstellt wird](../media-draft/q-auto-create-small.png)

Im nächsten Abschnitt sehen Sie, wie das bisher Umgesetzte beim Testen aussieht.

## <a name="try-it-out"></a>Testen

Da nun mehrere Ausgabebindungen vorhanden sind, werden die Tests etwas komplizierter. Während in den vorherigen Aufgaben das Senden einer HTTP-Anforderung und einer Abfragezeichenfolge zum Testen ausreichend war, müssen Sie nun eine HTTP-POST-Anforderung senden. Außerdem müssen Sie überprüfen, ob Nachrichten tatsächlich der Warteschlange hinzugefügt werden.

1.  Klicken Sie bei ausgewählter Funktion [!INCLUDE [func-name-add](./func-name-add.md)] im Funktionen-App-Portal auf das ganz links angezeigte Menüelement für Tests, um es zu erweitern.

2. Klicken Sie auf das Menüelement **Test**, und überprüfen Sie, ob der Testbereich geöffnet ist. Der folgende Screenshot zeigt, wie der Bildschirm aussehen sollte. 

![Screenshot mit erweitertem Bereich für den Funktionstest](../media-draft/test-panel-open-small.png)

> [!IMPORTANT]
> Stellen Sie sicher, dass in der Dropdownliste für die HTTP-Methode **POST** ausgewählt ist.

3. Ersetzen Sie den Inhalt des Anforderungstexts durch die folgende JSON-Nutzlast.

```json
  {
      "id": "docs",
      "url": "https://docs.microsoft.com/azure"
  }
  ```

4. Klicken Sie unten im Testbereich auf **Ausführen**. 

5. Überprüfen Sie, ob im Fenster *Ausgabe* die Nachricht „Bookmark already exists.“ (Das Lesezeichen ist bereits vorhanden.) wie auf dem folgenden Diagramm dargestellt angezeigt wird. 

![Screenshot mit Anzeige des Testbereichs und dem Ergebnis eines fehlgeschlagenen Tests](../media-draft/test-exists-small.png)

6. Ersetzen Sie nun den Inhalt des Anforderungstexts durch die folgende JSON-Nutzlast. 

```json
  {
      "id": "github",
      "URL": "https://www.github.com"
  }
  ```
7. Klicken Sie unten im Testbereich auf **Ausführen**.

8. Stellen Sie sicher, dass im Fenster *Ausgabe* die Nachricht „bookmark added“ (Ein Lesezeichen wurde hinzugefügt.) wie auf dem folgenden Diagramm dargestellt angezeigt wird.

![Screenshot mit Anzeige des Testbereichs und dem Ergebnis eines erfolgreichen Tests](../media-draft/test-success-small.png)

Herzlichen Glückwunsch! [!INCLUDE [func-name-add](./func-name-add.md)] funktioniert wie vorgesehen. Wie sieht es aber mit dem Warteschlangenvorgang aus, der im Code festgelegt wurde? Als Nächstes überprüfen Sie, ob der Warteschlange Nachrichten hinzugefügt wurden.

### <a name="verify-that-a-message-is-written-to-our-queue"></a>Sicherstellen, dass der Warteschlange eine Nachricht hinzugefügt wird

Azure Queue Storage-Warteschlangen werden in einem Speicherkonto gehostet. Sie haben es in dieser Übung bereits beim Erstellen der Ausgabebindung ausgewählt. 

1. Geben Sie im Hauptsuchfeld im Azure-Portal *Speicherkonten* ein. Wählen Sie anschließend in den Suchergebnissen **Speicherkonten** unter der Kategorie *Dienste* aus. Dies wird auf dem folgenden Screenshot veranschaulicht. 

![Screenshot mit Suchergebnissen für das Speicherkonto im Hauptsuchfeld](../media-draft/search-for-sa-small.png)

2. Wählen Sie in der Liste der angezeigten Speicherkonten das Speicherkonto aus, das Sie zum Erstellen der Ausgabebindung **newmessage** verwendet haben. Die Einstellungen des Speicherkontos werden im Hauptfenster des Portals angezeigt.

3. Wählen Sie das Element **Warteschlangen** aus der Liste der Dienste aus. Dadurch wird eine Liste mit Warteschlangen angezeigt, die von diesem Speicherkonto gehostet werden. Überprüfen Sie, ob die Warteschlange **bookmarks-post-process** wie auf dem folgenden Screenshot dargestellt vorhanden ist.

![Screenshot mit Warteschlange in der Liste der Warteschlangen, die von diesem Speicherkonto gehostet werden](../media-draft/q-in-list-small.png)

4. Klicken Sie auf **bookmarks-post-process**, um die Warteschlange zu öffnen. Die Nachrichten, die sich in der Warteschlange befinden, werden in einer Liste angezeigt. Wenn keine Fehler auftreten, sollte sich die Nachricht, die beim Hinzufügen des Lesezeichens zur Datenbank übermittelt wurde, in der Warteschlange befinden und dem folgenden Eintrag entsprechen. 

![Screenshot mit Nachricht in der Warteschlange](../media-draft/message-in-q-small.png)

In diesem Beispiel wurde der Nachricht eine eindeutige ID zugewiesen, und das Feld **NACHRICHTENTEXT** enthält das Lesezeichen im JSON-Zeichenfolgenformat.

5. Sie können die Funktion noch weiter testen, indem Sie im Testbereich innerhalb des Anforderungstexts neue IDs und URLs festlegen und die Funktion ausführen. Beobachten Sie die Warteschlange eine Zeit lang, um zu sehen, wie neue Nachrichten eintreffen. Sie können außerdem einen Blick auf die Datenbank werfen, um zu überprüfen, ob neue Einträge hinzugefügt wurden. 

In dieser Aufgabe haben Sie mehr über Bindungen und Ausgabebindungen erfahren und Daten in Ihre Azure Cosmos DB-Datenbank geschrieben. Zusätzlich haben Sie eine weitere Ausgabebindung hinzugefügt und Nachrichten an eine Azure-Warteschlange übermittelt. Dadurch wurde deutlich, wie Sie mit Bindungen Daten von Eingangsquellen an unterschiedliche Ziele weiterleiten. Sie mussten weder Datenbankcode schreiben noch Verbindungszeichenfolgen selbst verwalten. Stattdessen haben Sie Bindungen deklarativ konfiguriert, wodurch die Absicherung der Verbindungen und die Skalierung der Funktion sowie der Verbindungen von der Plattform durchgeführt wurden.