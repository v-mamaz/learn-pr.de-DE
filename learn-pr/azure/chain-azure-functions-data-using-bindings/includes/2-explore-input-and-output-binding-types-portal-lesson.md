Das Zugreifen auf und Verarbeiten von Daten sind wichtige Aufgaben in vielen Softwarelösungen. Betrachten Sie einige dieser Szenarien:

* Sie wurden gebeten, eine Möglichkeit zu implementieren, eingehende Daten aus dem Blobspeicher in Azure Cosmos DB zu verschieben.
* Sie möchten eingehende Nachrichten in einer Warteschlange zur Verarbeitung durch eine andere Komponente in Ihrem Unternehmen speichern.
* Der Dienst muss Spielergebnisse aus einer Warteschlange abrufen und eine Onlineanzeigetafel aktualisieren.

Alle diese Beispiele beschäftigen sich mit dem Verschieben von Daten. Die Datenquelle und die Ziele unterscheiden sich von Szenario zu Szenario, aber das Muster ist ähnlich. Sie stellen eine Verbindung mit einer Datenquelle her, Sie lesen und schreiben Daten. Azure Functions unterstützt Sie bei der Integration von Daten und Diensten über Bindungen. 

## <a name="what-is-a-binding"></a>Was ist eine Bindung?

In Funktionen bieten Bindungen eine deklarative Möglichkeit, eine Verbindung mit Daten über Ihren Code herzustellen. Sie erleichtern die konsistente Integration von Datenströmen in eine Funktion. Ein Trigger definiert, wie eine Funktion aufgerufen wird. Sie können nur einen Trigger verwenden, aber Sie können mehrere Bindungen in einer Funktion haben. Dies ist leistungsfähig, da Sie sich mit Ihren Datenquellen verbinden können, ohne die Werte hartcodieren zu müssen, z.B. die *Verbindungszeichenfolge*.

### <a name="two-kinds-of-bindings"></a>Zwei Arten von Bindungen

Es gibt zwei Arten von Bindungen, die Sie für Ihre Funktionen verwenden können:

1. **Eingabebindung**: Eine Eingabebindung ist eine Verbindung mit einer **Datenquelle**. Unsere Funktion liest Daten aus dieser Quelle.

1. **Ausgabebindung**: Eine Ausgabebindung ist eine Verbindung mit einem **Datenziel**. Unsere Funktion schreibt Daten in dieses Ziel.

### <a name="types-of-supported-bindings"></a>Typen von unterstützten Bindungen

Der *Typ* der Bindung definiert, woraus wir Daten lesen oder wohin wir Daten senden. Es gibt eine Bindung zur Beantwortung von Webanforderungen und eine große Auswahl an Bindungen für die Interaktion mit dem Speicher.

Die folgende Liste führt häufig verwendete Bindungen auf:
- Blob
- Warteschlange
- Cosmos DB
- Event Hubs
- Externe Dateien
- Externe Tabellen
- HTTP

### <a name="binding-properties"></a>Bindungseigenschaften

Es gibt vier Eigenschaften, die in allen Bindungen erforderlich sind. Sie müssen möglicherweise zusätzliche Eigenschaften basierend auf dem Typ der verwendeten Bindung und/oder des Speichers angeben.

- **Name**: Die `name`-Eigenschaft definiert den Funktionsparameter, über den Sie auf die Daten zugreifen. In einer Warteschlangen-Eingabebindung ist dies z.B. der Name des Funktionsparameters, der den Inhalt der Warteschlangennachricht empfängt. 

- **Typ**: Die `type`-Eigenschaft identifiziert den Typ der Bindung, d.h. den Typ der Daten oder des Diensts, mit denen bzw. dem die Interaktion erfolgen soll.

- **Richtung**: Die `direction`-Eigenschaft identifiziert die Richtung, in die Daten fließen. Sie gibt also an, ob es sich um eine Eingabe- oder Ausgabebindung handelt.

- **Verbindung**: Bei der `connection`-Eigenschaft handelt es sich nicht um die Verbindungszeichenfolge selbst, sondern um den Namen einer App-Einstellung, die die Verbindungszeichenfolge enthält. Bindungen verwenden Verbindungszeichenfolgen, die in den App-Einstellungen gespeichert sind, um die bewährte Methode durchzusetzen, dass „function.json“ keine Dienstgeheimnisse enthält.

## <a name="create-a-binding"></a>Erstellen einer Bindung

Bindungen werden in JSON definiert. Eine Bindung wird in der Konfigurationsdatei Ihrer Funktion konfiguriert, die den Namen `function.json` trägt und sich im gleichen Ordner wie Ihr Funktionscode befindet.

 Sehen wir uns ein Beispiel für eine *Eingabebindung* an:

```json
    ...
    {
      "name": "headshotBlob",
      "type": "blob",
      "path": "thumbnail-images/{filename}",
      "connection": "HeadshotStorageConnection",
      "direction": "in"
    },
    ...
```

Zum Erstellen dieser Bindung gehen Sie folgendermaßen vor:

1. Erstellen Sie eine Bindung in der Datei `function.json`.

1. Geben Sie den Wert für die Variable `name` an. In diesem Beispiel enthält die Variable die Blobdaten.

1. Geben Sie den Speicher `type` an. Im vorherigen Beispiel verwenden wir Blobspeicher.

1. Geben Sie den `path` an, der den Container und den Elementnamen angibt, der in ihm gespeichert wird. Die `path`-Eigenschaft ist für Blobs erforderlich.

1. Geben Sie den Namen der `connection`-Zeichenfolgeneinstellung an, der in der Datei mit den Einstellungen der Anwendung definiert wurde. Er wird als Suche verwendet, um die Verbindungszeichenfolge für die Verbindung mit Ihrem Speicher zu ermitteln.

1. Definieren Sie die `direction` als `in`, damit Daten aus dem Blob gelesen werden.

Bindungen werden verwendet, um Daten mit Ihrer Funktion zu verbinden. In dem Beispiel, das wir uns angesehen haben, haben wir eine Eingabebindung verwendet, um Benutzerbilder zu verbinden, die von unserer Funktion als Miniaturansichten verarbeitet werden.