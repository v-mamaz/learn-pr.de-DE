In unserem letzten Übung implementiert haben wir ein Szenario zum Nachschlagen von Lesezeichen in einer Azure Cosmos DB-Datenbank. Wir konfiguriert eine eingabebindung zum Lesen von Daten in die Auflistung von Lesezeichen. Aber bloße Lesen von Daten ist langweilig, lassen Sie uns mehr tun. Erweitern wir das Szenario aus, um das Schreiben von aufzunehmen. Betrachten Sie das folgende Flussdiagramm.

![Flussdiagramm der Prozess des Hinzufügens eines Lesezeichens in unsere Cosmos DB Back-end](../media-draft/add-bookmark-flow-small.png)

In diesem Szenario erhalten Sie Anforderungen zum Hinzufügen von Lesezeichen unserer Liste. Die Anforderungen in den gewünschten Schlüssel oder eine ID zusammen mit der Lesezeichen-URL zu übergeben. Wie Sie im Flussdiagramm sehen können, werden wir mit einem Fehler reagieren, wenn der Schlüssel bereits in unserem Back-End vorhanden ist.

Wenn der Schlüssel, der uns übergeben wurde *nicht* gefunden wird, werden wir das neue Lesezeichen mit unserer Datenbank hinzufügen. Wir können hier aufhören, sondern führen wir ein wenig mehr.

Beachten Sie, dass ein weiterer Schritt im Flussdiagramm? Bisher nicht getan haben wir viel mit den Daten durchgeführt, die wir im Hinblick auf die Verarbeitung zu erhalten. Wir verschieben, was wir in einer Datenbank erhalten. In einer realen Lösung ist es jedoch möglich, dass wir wahrscheinlich die Daten auf irgendeine Weise verarbeitet. Wir können Sie die gesamte Verarbeitung in die gleiche Funktion, aber in dieser Übungseinheit, die wir ein Muster zeigen werde, die lagert der weiteren Verarbeitung in eine andere Komponente oder Teil der Geschäftslogik.

Was könnte ein gutes Beispiel für diese Abladung der Arbeit in unserem Szenario Lesezeichen sein? Und was geschieht, wenn wir das neue Lesezeichen an einen QR-Code generieren-Dienst senden? Diesen Dienst würde, wiederum einen QR-Code für die URL zu generieren, speichern Sie das Abbild im Blob-Speicher und die Adresse des QR-Images wieder auf den Eintrag in der Sammlung von Lesezeichen hinzufügen. Aufrufen eines Diensts, um ein QR-Image zu generieren ist zeitaufwändig also stattdessen als das Ergebnis zu warten, wir an eine Funktion übergeben, und sie diese asynchron Probleme zu umgehen.

Genau, wie Sie Azure Functions eingabebindungen für die Integration mit anderen Datenquellen unterstützt, hat es auch einen Satz von Ausgabe Bindungen Vorlagen, die Ihnen das Schreiben von Daten zu anderen Datenquellen erleichtern. Ausgabebindungen konfigurierte sind auch in der *"Function.JSON"* Datei.  In dieser Übung sehen, können wir unsere-Funktion zum Arbeiten mit mehreren Datenquellen und -Dienste konfigurieren.

> [!IMPORTANT]
> In dieser Übung erstellt, in der Übung in der letzten Einheit, d. h., sie verwendet dieselbe Azure Cosmos DB-Datenbank und -eingabebindung. Wenn Sie über diese Einheit gearbeitet haben, wird empfohlen, auf diese Weise vor dem Fortfahren mit dieser Übung.

## <a name="create-an-httptriggered-function"></a>Erstellen einer HTTP_triggered-Funktion

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/?azure-portal=true) an.

2. Navigieren Sie im Azure-Portal zur Funktions-app, die Sie in diesem Modul erstellt haben.

3. Erweitern Sie Ihre Funktionen-app dann zeigen Sie auf die Auflistung von Funktionen aus, und aktivieren Sie das Hinzufügen (**+**) neben **Funktionen**. Diese Aktion wird der Prozess der Funktion gestartet. Die folgende Animation veranschaulicht dieses Aktion.

![Die Animation von dem Pluszeichen (+) angezeigt wird, wenn der Benutzer auf das Menüelement Funktionen zeigt.](../media-draft/func-app-plus-hover-small.gif)

4. Die Seite zeigt uns, den aktuellen Satz von unterstützten Trigger. Wählen Sie **HTTP-Trigger**, dies ist der erste Eintrag im folgenden Screenshot.

![Screenshot des Teils der Trigger Vorlagenauswahl-Benutzeroberfläche mit dem TTP-Trigger zuerst angezeigt, in der oberen linken Seite des Bilds.](../media-draft/trigger-templates-small.PNG)

5. Füllen Sie die **neue Funktion** mithilfe der folgenden Werte rechts angezeigten Dialogfeld.

|Feld  |Wert  |
|---------|---------|
|Sprache     | **JavaScript**        |
|Name     |   [!INCLUDE [func-name-add](./func-name-add.md)]     |
| Autorisierungsstufe | **Function** |

5. Wählen Sie **erstellen** unserer Funktion zu erstellen, die der Datei "Index.js" im Code-Editor geöffnet und zeigt eine Standardimplementierung der per HTTP ausgelöste Funktion.

In dieser Übung werden beschleunigen wir Dinge unter Verwendung der *Code* und *Konfiguration* aus der vorherigen Einheit als Ausgangspunkt.

6. Ersetzen Sie alle Code in "Index.js", mit dem Code aus den folgenden Codeausschnitt und auf **speichern** um diese Änderung zu speichern. 

[!code-javascript[](../code/find-bookmark-single.js)]

Wenn dieser Code vertraut aussieht, das ist, da es sich um die Implementierung ist unsere [!INCLUDE [func-name-find](./func-name-find.md)] Funktion. Wie zu erwarten ist, funktioniert die Funktion nicht, bis wir die gleichen Bindungen definieren.  

7. Öffnen der *"Function.JSON"* -Datei aus dem [!INCLUDE [func-name-find](./func-name-find.md)] Funktion. Sie finden es durch Öffnen der **Ansichtsdateien** Menü auf der rechten Seite im Code-Editor.

8. Kopieren Sie den gesamten Inhalt dieser Datei.

9. Öffnen der *"Function.JSON"* -Datei aus dem [!INCLUDE [func-name-add](./func-name-add.md)] Funktion.

10. Ersetzen Sie den Inhalt dieser Datei mit dem Inhalt, die Sie kopiert haben, aus der *"Function.JSON"* gleichnamige Datei aus der [!INCLUDE [func-name-find](./func-name-find.md)] Funktion. Wenn Sie fertig sind, sollte Ihre "Function.JSON" den folgenden JSON-Code enthalten.

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

11. Stellen Sie sicher, dass **speichern** alle Änderungen.

In den vorherigen Schritten konfiguriert wir für unsere neue Funktion Bindungen durch Bindungsdefinitionen von einem anderen kopieren. Wir könnten natürlich erstellt eine neue Bindung über die Benutzeroberfläche, aber es ist gut zu wissen, dass diese Alternative für Sie verfügbar ist.

## <a name="try-it-out"></a>Ausprobieren

1. Wie üblich, klicken Sie auf **<> / Get Funktions-URL** wählen Sie oben rechts, **Standard (Funktionstaste)**, und klicken Sie dann auf **Kopie** , kopieren Sie die Funktion der URL.

2. Fügen Sie die Funktions-URL, die Sie in der Adressleiste des Browsers kopiert haben. Fügen Sie den Wert der Abfragezeichenfolge `&id=docs` am Ende der URL hinzu, und drücken Sie die Taste `Enter` auf Ihrer Tastatur, um die Anforderung auszuführen. Alle hier auch eine Antwort angezeigt werden soll, die eine URL für diese Ressource enthält.

Sind, in dem wir bei? Nun, haben bisher wir eigentlich nur repliziert, was wir in der vorherigen Lektion haben. Aber das ist in Ordnung. Wir sind kopieren, was wir im letzten dienen als Ausgangspunkt für dieses Lab getan haben. Wir arbeiten auf die neue Dinge dann nämlich in unserer Datenbank geschrieben. Dafür müssen wir eine *ausgabebindung*.

## <a name="define-azure-cosmos-db-output-binding"></a>Definieren Sie Azure Cosmos DB-ausgabebindung

Stattdessen als eine neue ausgabebindung mithilfe der Benutzeroberfläche zu definieren, erstellen wir diese Bindung durch die XML-Konfigurationsdatei aktualisieren *"Function.JSON"*, manuell. 

1. Öffnen der **"Function.JSON"** -Datei für diese Funktion im Editor, indem Sie ihn im Auswählen der **Ansichtsdateien** Liste.

2. Kopieren Sie die Bindung mit dem Namen `bookmark` in dieser Datei.

3. Platzieren Sie den Cursor direkt nach der schließenden geschweiften Klammer unmittelbar vor das schließende eckige Klammer ein. Fügen Sie ein Komma `,` und fügen Sie die Kopie der Bindung hier. Ihre *"Function.JSON"* Konfiguration sollte nun wie folgt aussehen.

[!code-json[](../code/config-new-entry.json?highlight=22-31)]

4. Bearbeiten Sie die Bindung, die wir eingefügt, mit den folgenden Änderungen haben an.


|Eigenschaft   |Alter Wert  |Neuer Wert  |
|---------|---------|---------|
|name     |   Lesezeichen      |  **newbookmark**       |
|direction     |   in      |   **out**      |
|id     |      {id}   |   **Löschen Sie diese Eigenschaft an. Es ist nicht für die ausgabebindung vorhanden.**      |

Wenn Sie diese Änderungen vornehmen, erhalten Sie eine Datei, die den folgenden JSON-Code aussieht.

[!code-json[](../code/config-q-complete.json?highlight=22-30)]

Das war nur eine Demo, wie Sie Bindungen auch direkt in der Konfigurationsdatei erstellen können. In diesem Beispiel ist es sinnvoll, da wir die Eigenschaften aus einer anderen Bindung, nämlich Wiederverwenden der `databaseName`, `collectionName` und `connection` , dass wir bereits konfiguriert haben, für unsere Cosmos DB-eingabebindung.

> [!NOTE]
> Der tatsächliche Wert der `connection` in der obigen JSON-Datei, einen beliebigen Namen, die die Verbindung wurde bei der Erstellung angegeben werden.

Bevor wir den Code aktualisieren, fügen Sie eine weitere Bindung, mit denen Nachrichten an eine Warteschlange veröffentlichen kann.

## <a name="define-azure-queue-storage-output-binding"></a>Definieren Sie Azure Queue Storage-ausgabebindung

Azure Queue Storage ist ein Dienst zum Speichern von Nachrichten, die von überall auf der Welt zugegriffen werden können. Eine einzelne Nachricht kann bis zu 64 KB sein und eine Warteschlange kann Millionen von Nachrichten bis zur Kapazitätsgrenze des Speicherkontos, in dem sie definiert ist, insgesamt enthalten. Das folgende Diagramm zeigt auf hoher Ebene, wie eine Warteschlange in diesem Szenario verwendet werden.

![Das Diagramm zeigt Konzept einer Speicherwarteschlange und zwei Funktionen mithilfe von Push übertragen und Nachrichten in der Warteschlange entfernt.](../media-draft/q-logical-small.png)

Hier sehen wir, dass unsere neue Funktion [!INCLUDE [func-name-add](./func-name-add.md)], einer Warteschlange Nachrichten hinzugefügt. Wird aufgerufen, eine andere Funktion, z. B. eine fiktive Funktion *Gen-qr-Code*, pop-Nachrichten aus derselben Warteschlange und die Anforderung verarbeitet wird.  Da wir schreiben, oder *Push*, Nachrichten an die Warteschlange von [!INCLUDE [func-name-add](./func-name-add.md)], unsere Lösung eine neue ausgabebindung hinzugefügt. Erstellen wir die Bindung über die Benutzeroberfläche dieser Zeit.

1. Wählen Sie **integrieren** in der Funktion im Menü auf der linken Seite auf die Registerkarte "Integration" zu öffnen.

2. Wählen Sie **+ neue Ausgabe** unter der **Ausgaben** Spalte. Eine Liste von allen Bindungstypen für mögliche Ausgabe wird angezeigt.

3. Klicken Sie auf **Azure Queue Storage** aus der Liste und klicken Sie dann die **wählen** Schaltfläche. Diese Aktion öffnet die Konfigurationsseite für Azure Queue Storage-Ausgabe.

Als Nächstes müssen wir eine speicherkontoverbindung einrichten. Dies ist, in dem unsere Warteschlange gehostet wird.

4. Im Feld mit dem Namen **speicherkontoverbindung** klicken Sie auf dieser Seite auf *neue* rechts neben das Feld leer. Diese Aktion öffnet den **Speicherkonto** Dialogfeld "Auswahl". 

5. Wenn wir dieses Modul gestartet und unsere Funktions-app erstellt, wurde ein Speicherkonto auch zu diesem Zeitpunkt erstellt. In diesem Dialogfeld aufgeführt, also fahren Sie fort und wählen Sie ihn. Die **speicherkontoverbindung** Feld wird aufgefüllt, mit dem Namen der Verbindung. Wenn der Wert der Verbindungszeichenfolge angezeigt werden sollen, klicken Sie auf **Wert anzeigen**.

6. Obwohl wir alle anderen Felder auf dieser Seite mit ihren Standardwerten lassen kann, ändern wir Folgendes ein, um weitere Bedeutung für die Eigenschaften zu verleihen.


|Eigenschaft  |Alter Wert  |Neuer Wert  | Beschreibung |
|---------|---------|---------|---------|
|Warteschlangenname     |    outqueue     |  **bookmarks-post-process**      | Dies ist der Name der Warteschlange platziert verwenden wir Lesezeichen, damit sie verarbeitet werden können weiter von einer anderen Funktion. |
| Name des Meldungsparameters    |  outputQueueItem       |   **newmessage**      | Dies ist die Binding-Eigenschaft, die wir in Code verwenden. |


7. Klicken Sie auf **speichern** zum Speichern der Änderungen.

## <a name="update-function-implementation"></a>Implementierung der Update-Funktion

Wir haben jetzt alle unsere Bindungen festgelegt wird, für die [!INCLUDE [func-name-add](./func-name-add.md)] Funktion. Es ist Zeit, die sie in unserer Funktion zu verwenden.

1.  Klicken Sie auf unserer Funktion [!INCLUDE [func-name-add](./func-name-add.md)], öffnen Sie *"Index.js"* im Code-Editor.

2. Ersetzen Sie alle Code in "Index.js", mit dem Code aus den folgenden Codeausschnitt:

[!code-javascript[](../code/add-bookmark.js)]

Lassen Sie uns Aufschlüsselung der Funktionsweise dieses Codes.

* Da diese Funktion auf unsere Daten ändert, erwarten wir einen Beitrag und die Lesezeichen-Daten als Teil der Anforderungstext ist die HTTP-Anforderung.
* Unsere Cosmos DB-eingabebindung wird versucht, ein Dokument oder Lesezeichen abzurufen mithilfe der `id` , die wir erhalten. Wenn es sich um einen Eintrag, findet die `bookmark` Objekt festgelegt. Die `if(bookmark)` Bedingung überprüft, ob ein Eintrag gefunden wurde.
* Das Hinzufügen von in die Datenbank ist einfach wie das Festlegen der `context.bindings.newbookmark` bindenden Parameter auf den neuen Lesezeicheneintrag, das wir als JSON-Zeichenfolge erstellt haben.
* Veröffentlichen einer Nachricht an unsere Warteschlange ist so einfach wie das Festlegen der `context.bindings.newmessage parameter`.

> [!NOTE]
> Die einzige Aufgabe, die wir durchgeführt wurde, eine Bindung für die Warteschlange zu erstellen. Wir haben nie explizit die Warteschlange. Sie werden die Leistungsfähigkeit von Bindungen unmittelbare! Wie die folgende Legende angezeigt wird, wird die Warteschlange automatisch für Sie erstellt, wenn er nicht vorhanden ist!

![Bildschirmabbildung von Aufrufen von darauf hin, dass die Warteschlange wird automatisch-erstellt.](../media-draft/q-auto-create-small.png)

Also das ist schon alles – sehen wir uns unsere Arbeit in Aktion im nächsten Abschnitt.

## <a name="try-it-out"></a>Ausprobieren

Nun, wir mehrere ausgabebindungen haben, wird die für unsere Tests ein wenig schwieriger. Während in vorherigen Labs wir Inhalt Waren durch Senden einer HTTP-Anforderung und eine Abfragezeichenfolge getestet, sollten wir dieses Mal führen Sie eine HTTP-Post. Wir müssen auch überprüfen, ob Nachrichten es in eine Warteschlange machen.

1.  Mit unserer Funktion [!INCLUDE [func-name-add](./func-name-add.md)], klicken Sie mit der im Portal Funktions-Apps aktiviert ist, auf das Menüelement "Test" ganz links um ihn zu erweitern.

2. Wählen Sie die **testen** Menü Element aus, und überprüfen Sie, ob Sie den Testbereich zu öffnen. Der folgende Screenshot zeigt, wie es aussehen sollte. 

![Screenshot mit der Funktion Testbereich erweitert.](../media-draft/test-panel-open-small.png)

> [!IMPORTANT]
> Stellen Sie sicher, dass **POST** in der Dropdownliste "HTTP-Methode" ausgewählt ist.

3. Ersetzen Sie den Inhalt des Anforderungstexts mit der folgenden JSON-Nutzlast ein.

```json
  {
      "id": "docs",
      "url": "https://docs.microsoft.com/azure"
  }
  ```

4. Klicken Sie auf **ausführen** am unteren Rand der Testbereich. 

5. Überprüfen Sie, ob die *Ausgabe* Fenster wird angezeigt, die "Lesezeichen ist bereits vorhanden." Meldung wie im folgenden Diagramm dargestellt. 

![Screenshot der Bereich zu testen und das Ergebnis eines fehlgeschlagenen Tests.](../media-draft/test-exists-small.png)

6. Ersetzen Sie jetzt den Anforderungstext mit der folgenden Nutzlast. 

```json
  {
      "id": "github",
      "URL": "https://www.github.com"
  }
  ```
7. Klicken Sie auf **ausführen** am unteren Rand der Testbereich.

8. Stellen Sie sicher, dass *Ausgabe* im werden die Meldung "Lesezeichen hinzugefügt" angezeigt, wie im folgenden Diagramm dargestellt.

![Screenshot der Bereich zu testen und das Ergebnis der Test erfolgreich war.](../media-draft/test-success-small.png)

Herzlichen Glückwunsch! Die [!INCLUDE [func-name-add](./func-name-add.md)] funktioniert wie vorgesehen, aber wie sieht es mit dieser Warteschlangenvorgang im Code werden musste? Gut, sehen wir, wenn etwas in eine Warteschlange geschrieben wurde.

### <a name="verify-that-a-message-is-written-to-our-queue"></a>Stellen Sie sicher, dass eine Nachricht an unsere Warteschlange geschrieben wird

Azure Queue Storage-Warteschlangen werden in einem Speicherkonto gehostet. Auswahl der Storage-Konto in dieser Übung bereits beim Erstellen der ausgabebindung. 

1. Geben Sie im Hauptmenü Search im Azure-Portal *Speicherkonten* wird daraufhin in die Suche auf **Speicherkonten** unter der *Services* Kategorie. Dies wird im folgenden Screenshot veranschaulicht. 

![Screenshot mit der Suchergebnisse für Storage-Konto in das Suchfeld für die wichtigsten.](../media-draft/search-for-sa-small.png)

2. Wählen Sie in der Liste der Speicherkonten, die zurückgegeben werden, die Storage-Konto, das Sie zum Erstellen der **Newmessage** ausgabebindung. Die Einstellungen des Storage-Kontos werden im Hauptfenster angezeigt im Portal.

3. Wählen Sie die **Warteschlangen** Element aus der Liste der Dienste. Dies zeigt eine Liste der Warteschlangen, die von diesem Storage-Konto gehostet wird. Überprüfen Sie, ob die **Lesezeichen-Post-Process** Warteschlange vorhanden ist, wie im folgenden Screenshot gezeigt.

![Screenshot mit unserer Warteschlange in der Liste der Warteschlangen, die von diesem Storage-Konto gehostet wird](../media-draft/q-in-list-small.png)

4. Klicken Sie auf **Lesezeichen-Post-Process** zum Öffnen der Warteschlange. Die Nachrichten, die in der Warteschlange befinden, werden in einer Liste angezeigt. Wenn alle plangemäß verlaufen ist, sollte die Meldung, die wir veröffentlicht, wenn wir ein Lesezeichen mit unserer Datenbank hinzugefügt in der Warteschlange und sieht wie der folgende Eintrag. 

![Screenshot mit der Nachricht in der Warteschlange](../media-draft/message-in-q-small.png)

In diesem Beispiel können Sie sehen, dass die Nachricht eine eindeutige ID zugewiesen wurde und die **MELDUNGSTEXT** Feld wird unsere Lesezeichen in einem JSON-Format angezeigt.

5. Sie können weiter die Funktion testen, ändern den Text der Anforderung im Bereich "Tests" mit neuen Id-Url und die Funktion ausführen. Sehen Sie sich diese Warteschlange, um weitere Nachrichten eintreffen anzuzeigen. Sie können auch suchen in der Datenbank überprüfen wurden neue Einträge hinzugefügt. 

In dieser Übungseinheit erhalten erweitert wir unseren Erkenntnissen der Bindungen auf ausgabebindungen Schreiben von Daten in Azure Cosmos DB-. Ging noch weiter, und wir hinzugefügt, eine andere Ausgabe Binden an die Nachrichten an eine Azure-Warteschlange zu senden. Dieses Beispiel veranschaulicht die wahre Leistungsstärke von Bindungen können Sie die Form, und Verschieben von Daten aus der eingehenden Quellen mit einer Vielzahl von Zielen. Wir noch nicht geschriebene Datenbankcode oder Verbindungszeichenfolgen selbst verwalten mussten. Stattdessen wir Bindungen konfiguriert deklarativ und die Plattform kümmert sich Sichern der Verbindungen, skalieren unsere-Funktion und unsere Verbindungen skalieren lassen.