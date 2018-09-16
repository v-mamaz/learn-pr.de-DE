Um eine Verbindung mit einer Datenquelle herzustellen, müssen wir eine *Eingabebindung* konfigurieren. Durch diese Bindung können Sie mit minimalem Programmieraufwand eine Nachricht erstellen. Sie müssen keinen Code für Aufgaben wie das Öffnen einer Speicherverbindung schreiben. Die Azure Functions-Laufzeit und -Bindung nehmen Ihnen diese Aufgaben ab.

## <a name="input-binding-types"></a>Eingabebindungstypen

Es gibt mehrere Eingabetypen, jedoch nicht alle Typen unterstützen sowohl Ein- als auch Ausgabe. Sie können sie immer dann verwenden, wenn Sie Daten dieses Typs erfassen möchten. Hier untersuchen wir die Typen, die Eingabebindungen unterstützen, und die Frage, wann sie verwendet werden.

- **Blobspeicher**: Die Blobspeicherbindungen ermöglichen es Ihnen, aus einem Blob zu lesen.

- **Azure Cosmos DB**: Die Azure Cosmos DB-Eingabebindung verwendet die SQL-API, um mindestens ein Azure Cosmos DB-Dokument abzurufen und an den Eingabeparameter der Funktion zu übergeben. Die Dokument-ID oder die Abfrageparameter können basierend auf dem Trigger, der die Funktion aufruft, ermittelt werden.

- **Microsoft Graph**: Microsoft Graph-Eingabebindungen ermöglichen es Ihnen, Dateien aus OneDrive und Daten aus Excel zu lesen und Authentifizierungstoken abzurufen, damit Sie mit jeder Microsoft Graph-API interagieren können.
- **Mobile Apps**: Die Mobile Apps-Eingabebindung lädt einen Datensatz aus einem mobilen Tabellenendpunkt und übergibt ihn an die Funktion.

- **Table Storage**: Sie können Daten lesen und mit Azure Table Storage arbeiten.

## <a name="how-to-create-an-input-binding"></a>Wie wird eine Eingabebindung erstellt?

Um eine Bindung als eine Eingabe zu definieren, müssen Sie die `direction` als `in` definieren.
Die Parameter für jeden Typ von Bindung können unterschiedlich sein. Diese sind in der [Dokumentation von Microsoft](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings#supported-bindings?azure-portal=true) gut dokumentiert.

## <a name="what-is-a-binding-expression"></a>Was ist ein Bindungsausdruck?

Ein Bindungsausdruck stellt spezialisierten Text in „function.json“, Funktionsparameter oder Code dar. Diese Elemente werden beim Aufruf der Funktion ausgewertet, um einen Wert zu erhalten. Beispielsweise können Sie einen Bindungsausdruck verwenden, um die aktuelle Uhrzeit oder einen Wert aus den App-Einstellungen abzurufen.

### <a name="types-of-binding-expressions"></a>Typen von Bindungsausdrücken

- App-Einstellungen
- Name der Triggerdatei
- Metadaten für Trigger
- JSON-Nutzlasten
- Neue GUID
- Aktuelles Datum und Uhrzeit
- Bindungsausdrücke

Die meisten Ausdrücke werden identifiziert, indem sie in geschweifte Klammern eingeschlossen werden. Bindungsausdrücke für App-Einstellungen werden jedoch anders dargestellt als andere Bindungsausdrücke: Sie werden in Prozentzeichen anstatt in geschweifte Klammern eingeschlossen. Wenn der Pfad der Blobausgabebindung z.B. `%Environment%/newblob.txt` ist und die App-Einstellung „Environment“ den Wert „Development“ aufweist, wird ein Blob im Container „Development“ erstellt.

Über Eingabebindungen können wir unsere-Funktion mit einer Datenquelle verbinden. Es gibt verschiedene Typen von Datenquellen, mit denen wir eine Verbindung herstellen können, und die Parameter für jeden einzelnen Typ sind unterschiedlich. Wir können Bindungsausdrücke in der Datei „function.json“, in Funktionsparametern oder im Code verwenden, um Werte aus verschiedenen Quellen aufzulösen.