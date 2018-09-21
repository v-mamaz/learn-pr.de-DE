Um eine Verbindung mit einer Datenquelle herzustellen, muss eine *Eingabebindung* konfiguriert werden. Durch diese Bindung können Sie mit minimalem Programmieraufwand eine Nachricht erstellen. Sie müssen keinen Code für Aufgaben wie das Öffnen einer Speicherverbindung schreiben. Die Azure Functions-Laufzeit und -Bindung nehmen Ihnen diese Aufgaben ab.

## <a name="input-binding-types"></a>Eingabebindungstypen

Es gibt mehrere Arten von Eingaben. Allerdings unterstützen nicht alle Typen sowohl Ein- als auch Ausgaben. Sie können sie immer dann verwenden, wenn Sie Daten dieses Typs erfassen möchten. Hier untersuchen wir die Typen, die Eingabebindungen unterstützen, und klären die Frage, wann sie verwendet werden.

- **Blobspeicher:** Blobspeicherbindungen ermöglichen es Ihnen, aus einem Blob zu lesen.

- **Azure Cosmos DB:** Die Azure Cosmos DB-Eingabebindung verwendet die SQL-API, um mindestens ein Azure Cosmos DB-Dokument abzurufen und an den Eingabeparameter der Funktion zu übergeben. Die Dokument-ID oder die Abfrageparameter können basierend auf dem Trigger, der die Funktion aufruft, ermittelt werden.

- **Microsoft Graph:** Microsoft Graph-Eingabebindungen ermöglichen es Ihnen, Dateien aus OneDrive und Daten aus Excel zu lesen und Authentifizierungstoken abzurufen, damit Sie mit jeder Microsoft Graph-API interagieren können.

- **Mobile Apps:** Die Eingabebindung für mobile Apps lädt einen Datensatz aus einem mobilen Tabellenendpunkt und übergibt ihn an die Funktion.

- **Table Storage:** Sie können Daten lesen und mit Azure Table Storage arbeiten.

Um eine Bindung als Eingabe zu erstellen, müssen Sie `direction` als `in` definieren.
Die Parameter für die unterschiedlichen Bindungstypen können variieren.

## <a name="what-is-a-binding-expression"></a>Was ist ein Bindungsausdruck?

Ein Bindungsausdruck stellt spezialisierten Text in **function.json**, Funktionsparametern oder Code dar. Diese Elemente werden beim Aufruf der Funktion ausgewertet, um einen Wert zu erhalten. Wenn Sie über eine Service Bus-Warteschlangenbindung verfügen, können Sie einen Bindungsausdruck verwenden, um den Namen der Warteschlange der App-Einstellungen abzurufen.

### <a name="types-of-binding-expressions"></a>Typen von Bindungsausdrücken

- App-Einstellungen
- Name der Triggerdatei
- Metadaten für Trigger
- JSON-Nutzlasten
- Neue GUID
- Aktuelles Datum und Uhrzeit

Die meisten Ausdrücke werden identifiziert, indem sie in geschweifte Klammern eingeschlossen werden. Allerdings werden Bindungsausdrücke der App-Einstellungen eher in Prozentzeichen anstatt in geschweiften Klammern eingeschlossen. Wenn der Pfad der Blobausgabebindung z.B. `%Environment%/newblob.txt` ist und die App-Einstellung „Environment“ den Wert „Development“ aufweist, wird ein Blob im Container „Development“ erstellt.

## <a name="summary"></a>Zusammenfassung

Über Eingabebindungen können wir unsere Funktion mit einer Datenquelle verbinden. Es können Verbindungen zu verschiedenen Datenquellentypen hergestellt werden, und die Parameter für jeden einzelnen Typ sind unterschiedlich. Um Werte aus verschiedenen Quellen aufzulösen, können Sie Bindungsausdrücke in der *function.json*-Datei, in Funktionsparametern oder im Code verwenden.