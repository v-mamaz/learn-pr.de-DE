Verbindungsherstellung mit einer Datenquelle, wir haben so konfigurieren Sie, eine *eingabebindung*. Diese Bindung wird minimale Code zum Erstellen einer Nachricht schreiben können. Sie müssen keinen Code für Aufgaben wie das Öffnen einer speicherverbindung zu schreiben. Die Azure Functions-Laufzeit und die Bindung sorgt diese Aufgaben für Sie.

## <a name="input-binding-types"></a>Typen der eingabebindung

Es gibt mehrere Arten von Eingaben, jedoch nicht alle Typen unterstützt sowohl ein- und Ausgabe. Sie verwenden diese, wann immer Sie zum Erfassen von Daten dieses Typs möchten. Hier ist betrachten die Typen wir, die eingabebindungen und deren Verwendung unterstützen.

- **BLOB-Speicher** Blob Storage-Bindungen ermöglichen es Ihnen, die aus einem Blob zu lesen.

- **COSMOS DB** der Azure Cosmos DB-eingabebindung verwendet die SQL-API, eine oder mehrere Azure Cosmos DB-Dokumente und übergibt sie an den Eingabeparameter der Funktion. Die Dokument-ID oder die Abfrageparameter können basierend auf dem Trigger, der die Funktion aufruft, ermittelt werden.

- **Microsoft Graph** Eingabe Microsoft Graph-Bindungen ermöglichen es Ihnen, Dateien aus OneDrive zu lesen, Lesen von Daten aus Excel und Authentifizierungstoken zu erhalten, damit Sie mit jeder Microsoft Graph-API interagieren können.
- **Mobile Apps** das Mobile Apps-eingabebindung lädt einen Datensatz aus einem mobilen tabellenendpunkt und übergibt ihn an Ihre Funktion.

- **Tabellenspeicher** können Sie Daten lesen und mit Azure Table Storage arbeiten.

## <a name="how-to-create-an-input-binding"></a>Vorgehensweise: erstellen eine eingabebindung?

Um eine Bindung definieren eine Eingabe, müssen Sie definieren die `direction` als `in`.
Die Parameter für jeden Typ der Bindung können abweichen, diese sind gut dokumentiert [Microsoft Dokumentation](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings#supported-bindings?azure-portal=true)

## <a name="what-is-a-binding-expression"></a>Was ist einem Bindungsausdruck?

Ein Bindungsausdruck ist spezialisierte Textvorlagen in "Function.JSON", Parameter oder Code, der ausgewertet wird, wenn die Funktion aufgerufen wird, um einen Wert zu ergeben. Beispielsweise können Sie einen Bindungsausdruck, der die aktuelle Uhrzeit abzurufen oder einen Wert aus der app-Einstellungen abrufen.

### <a name="types-of-binding-expressions"></a>Arten von Bindungsausdrücken

- App-Einstellungen
- Name der triggerdatei
- Metadaten für Trigger
- JSON-Nutzlasten
- Neue GUID
- Aktuelles Datum und Uhrzeit
- Bindungsausdrücke

Die meisten Ausdrücke sind von geschweiften Klammern umschlossen. Allerdings Bindungsausdrücke für app-Einstellung werden anders dargestellt als andere Bindungsausdrücke: sie werden in Prozentzeichen anstatt von geschweiften Klammern umschlossen. Beispielsweise ist der Pfad der blobausgabebindung `%Environment%/newblob.txt` und die Umgebung app-Einstellungswert ist die Entwicklung, ein Blob im Container Entwicklung erstellt werden.

Eingabebindungen können wir unsere-Funktion mit einer Datenquelle verbinden. Es gibt verschiedene Typen von Datenquellen, die, denen wir auf eine Verbindung herstellen können, und die Parameter für jedes aus. Wir können Bindungsausdrücke in "Function.JSON", Parameter oder Code verwenden, um Werte aus verschiedenen Quellen zu beheben.