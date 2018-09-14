Zugreifen auf und Verarbeiten von Daten sind wichtige Aufgaben viele softwarelösungen. Betrachten Sie einige dieser Szenarien:

* Sie haben eine Möglichkeit zum Verschieben von eingehenden Daten aus Blob Storage mit Azure Cosmos DB implementiert aufgefordert wurde.
* Eingehende Nachrichten an eine Warteschlange für die Verarbeitung von einer anderen Komponente in Ihrem Unternehmen bereitstellen möchten.
* Der Dienst muss Spieler Ergebnisse aus einer Warteschlange abrufen und aktualisieren Sie ein online Anzeigetafel.

Alle diese Beispiele sind Informationen zum Verschieben von Daten. Die Datenquelle und die Ziele unterscheiden sich von Szenario zum Szenario, aber das Muster ist ähnlich. Sie eine Verbindung mit einer Datenquelle herstellen, Sie lesen und Schreiben von Daten. Azure Functions können Sie mit Daten und Diensten, die mit Bindungen zu integrieren. 

## <a name="what-is-a-binding"></a>Was ist eine Bindung?

In Funktionen stellen Bindungen eine deklarative Möglichkeit zum Verbinden mit Daten aus dem Code heraus. Sie erleichtern die Integration von Datenströmen konsistent in eine Funktion. Ein Trigger definiert, wie eine Funktion aufgerufen wird. Sie können nur einen Trigger haben, aber Sie haben mehrere Bindungen in einer Funktion. Dies ist effektiv, da Sie mit den Datenquellen verbinden können, ohne dass die Werte, wie z. B. hartcodieren der *Verbindungszeichenfolge*.

### <a name="two-kinds-of-bindings"></a>Zwei Arten von Bindungen

Es gibt zwei Arten von Bindungen, die Sie für Ihre Funktionen verwenden können:

1. **Eingabebindung** eingabebindung wird eine Verbindung mit einer Datenquelle **Quelle**. Unsere Funktion liest Daten aus dieser Quelle.

1. **Ausgabebindung** eine ausgabebindung ist eine Verbindung mit einer Datenquelle **Ziel**. Unsere Funktion schreibt die Daten an dieses Ziel.

### <a name="types-of-supported-bindings"></a>Typen von unterstützten Bindungen.

Die *Typ* Bindung definiert, in dem wir lesen oder Senden von Daten. Eine Bindung zur Beantwortung von webanforderungen und einer großen Anzahl von Bindungen für die Interaktion mit Speicher ist vorhanden.

Hier ist eine Liste der häufig verwendeten Bindungen:
- Blob
- Warteschlange
- Cosmos DB
- Event Hubs
- Externe Dateien
- Externe Tabellen
- HTTP

### <a name="binding-properties"></a>Bindungseigenschaften

Es gibt vier Eigenschaften, die in allen Bindungen erforderlich sind. Sie müssen möglicherweise zusätzliche Eigenschaften, die basierend auf den Typ der Bindung bzw. Speicher verwendeten angeben.

- **Namen** der `name` Eigenschaft definiert den Funktionsparameter, die über die Sie auf die Daten zugreifen. In eine warteschlangeneingabebindung ist dies z. B. den Namen des Parameters der Funktion, die den Inhalt der warteschlangennachricht empfängt. 

- **Typ** der `type` Eigenschaft identifiziert den Typ der Bindung, d. h., die den Typ der Daten oder des Diensts für die Interaktion mit werden sollten.

- **Richtung** der `direction` Eigenschaft identifiziert, der die Richtung, die Daten ie fließen. ist es eine Eingabe- oder ausgabeadapter-Bindung?

- **Verbindung** der `connection` Eigenschaft ist der Name des app-Einstellung, die die Verbindungszeichenfolge und nicht die Verbindungszeichenfolge selbst enthält. Bindungen nutzen in der app-Einstellungen erzwingen die bewährte Methode gespeichert, "Function.JSON" enthält keine Geheimnisse eines Diensts.

## <a name="create-a-binding"></a>Erstellen Sie eine Bindung

Bindungen werden im JSON-Format definiert. Eine Bindung wird in die Funktions XML-Konfigurationsdatei mit dem Namen konfiguriert `function.json` und befindet sich im gleichen Ordner wie Ihrem Funktionscode.

 Sehen wir uns ein Beispiel für eine *eingabebindung*:

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

Erstellen Sie diese Bindung wir:

1. Erstellen Sie eine Bindung in unserer `function.json` Datei.

1. Geben Sie den Wert für die `name` Variable. In diesem Beispiel wird die Variable, die Blob-Daten enthalten.

1. Geben Sie den Speicher `type`, verwenden wir im vorherigen Beispiel-BLOB-Speicher.

1. Geben Sie die `path`, der angibt, den Container und die Elementnamen, der bei der es gesendet wird. Die `path` Eigenschaft ist erforderlich für Blobs.

1. Geben Sie die `connection` Zeichenfolgenname der Einstellung in der Datei mit der Anwendung definiert. Es wird als eine Suche verwendet, finden Sie die Verbindungszeichenfolge zur Verbindung mit Ihren Speicher.

1. Definieren der `direction` als `in`, Daten aus dem Blob gelesen wird.

Bindungen werden zum Verbinden mit Daten in Ihre Funktion. In dem Beispiel, dem wir uns angesehen haben, verwendet haben wir eine eingabebindung benutzerimages von unserer Funktion verarbeitet werden, als Miniaturansichten Verbindung.