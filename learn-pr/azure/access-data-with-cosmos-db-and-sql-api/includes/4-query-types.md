Nachfolgend werden einige Grundlagen zu Abfragen erläutert. Die beiden Dokumente, die Sie der Datenbank hinzugefügt haben, sollen als Ziel für die Beispielabfragen dienen. Genauso wie SQL Server verwendet Azure Cosmos DB SQL-Abfragen, um Abfragevorgänge durchzuführen. Sämtliche Eigenschaften werden standardmäßig automatisch indiziert, sodass alle Daten in der Datenbank unmittelbar zur Abfrage zur Verfügung stehen.

## <a name="sql-query-basics"></a>Grundlagen zu SQL-Abfragen
Jede SQL-Abfrage besteht aus einer SELECT-Klausel und optionalen FROM- und WHERE-Klauseln. Außerdem können Sie andere Klauseln wie ORDER BY und JOIN hinzufügen, um die erforderlichen Informationen abzufragen.

SQL-Abfragen haben das folgende Format:

    SELECT <select_list>
    [FROM <optional_from_specification>]
    [WHERE <optional_filter_condition>]
    [ORDER BY <optional_sort_specification>]
    [JOIN <optional_join_specification>]

## <a name="select-clause"></a>SELECT-Klausel

Die SELECT-Klausel bestimmt den Typ der Werte, die erstellt werden, wenn die Abfrage ausgeführt wird. Bei einem Wert vom Typ `SELECT *` wird das gesamte JSON-Dokument zurückgegeben.

**Abfrage**
```
SELECT *
FROM Products p
WHERE p.id ="1"
```

**Rückgaben**
```
[
    {
        "id": "1",
        "productId": "33218896",
        "category": "Women's Clothing",
        "manufacturer": "Contoso Sport",
        "description": "Quick dry crew neck t-shirt",
        "price": "14.99",
        "shipping": {
            "weight": 1,
            "dimensions": {
                "width": 6,
                "height": 8,
                "depth": 1
            }
        },
        "_rid": "iAEeANrzNAAJAAAAAAAAAA==",
        "_self": "dbs/iAEeAA==/colls/iAEeANrzNAA=/docs/iAEeANrzNAAJAAAAAAAAAA==/",
        "_etag": "\"00003a02-0000-0000-0000-5b9208440000\"",
        "_attachments": "attachments/",
        "_ts": 1536297028
    }
]
```

Stattdessen können Sie auch die Ausgabe einschränken, sodass nur bestimmte Eigenschaften angezeigt werden, indem Sie der SELECT-Klausel eine Liste mit Eigenschaften hinzufügen. In der folgenden Abfrage werden nur die ID, der Hersteller und die Produktbeschreibung hinzugefügt.

**Abfrage**
```
SELECT 
    p.id, 
    p.manufacturer, 
    p.description
FROM Products p
WHERE p.id ="1"
```

**Rückgaben**
```
[
    {
        "id": "1",
        "manufacturer": "Contoso Sport",
        "description": "Quick dry crew neck t-shirt"
    }
]
```

## <a name="from-clause"></a>FROM-Klausel

Die FROM-Klausel bestimmt die Datenquelle der Abfrage. Sie können sowohl die ganze Sammlung als auch ein Subnetz der Sammlung als Abfragequelle festlegen. Die FROM-Klausel ist optional, sofern die Quelle in der Abfrage später nicht gefiltert oder projiziert wird.

Bei einer Abfrage wie `SELECT * FROM Products` ist die gesamte Products-Sammlung die Quelle der Abfrage.

Eine Sammlung kann Aliase enthalten, z.B. `SELECT p.id FROM Products AS p` oder einfach `SELECT p.id FROM Products p`, wobei `p` `Products` entspricht. `AS` ist ein optionales Schlüsselwort, das als Alias für den Bezeichner fungiert.

Sobald ein Alias verwendet wird, kann die Originalquelle nicht mehr gebunden werden. `SELECT Products.id FROM Products p` ist beispielsweise syntaktisch ungültig, da der Bezeichner „Products“ nicht mehr aufgelöst werden kann.

Alle Eigenschaften, auf die verwiesen wird, müssen vollqualifiziert sein. Dies ist ohne strikte Schemaverwendung notwendig, um mehrdeutige Bindungen zu vermeiden. Daher ist `SELECT id FROM Products p` syntaktisch ungültig, weil die `id`-Eigenschaft nicht gebunden ist.

### <a name="subdocuments-in-a-from-clause"></a>Unterdokumente in einer FROM-Klausel
Die Quelle kann auch auf eine kleinere Teilmenge reduziert werden. Wenn Sie beispielsweise nur eine Unterstruktur in jedem Dokument auflisten möchten, kann deren Unterstamm wie im folgenden Beispiel gezeigt als Quelle fungieren:

**Abfrage**
```
SELECT * 
FROM Products.shipping
```

**Ergebnisse**  

```
[
    {
        "weight": 1,
        "dimensions": {
            "width": 6,
            "height": 8,
            "depth": 1
        }
    },
    {
        "weight": 2,
        "dimensions": {
            "width": 8,
            "height": 11,
            "depth": 3
        }
    }
]
```

Im obigen Beispiel wird zwar ein Array als Quelle verwendet, aber Sie können dafür auch wie im folgenden Beispiel ein Objekt verwenden: Jeder gültige JSON-Wert (mit Ausnahme von „Undefined“), der in der Quelle gefunden werden kann, wird für die Integration in das Abfrageergebnis herangezogen. Produkte ohne `shipping.weight`-Wert werden aus dem Abfrageergebnis ausgeschlossen.

**Abfrage**

    SELECT * 
    FROM Products.shipping.weight

**Ergebnisse**

    [
        1,
        2
    ]

## <a name="where-clause"></a>WHERE-Klausel
Die WHERE-Klausel gibt die Bedingungen an, die die in der Quelle angegebenen JSON-Dokumente erfüllen müssen, um als Teil des Ergebnisses zurückgegeben zu werden. Jedes JSON-Dokument muss die angegebenen Bedingungen erfüllen (**true**), um in das Ergebnis einbezogen zu werden. Die WHERE-Klausel ist optional.

Mit der folgenden Abfrage werden Dokumente angefordert, die eine ID mit dem Wert „1“ enthalten:

**Abfrage**

    SELECT p.description
    FROM Products p 
    WHERE p.id = "1"

**Ergebnisse**

    [
        {
            "description": "Quick dry crew neck t-shirt"
        }
    ]

## <a name="order-by-clause"></a>ORDER BY-Klausel

Mit der ORDER BY-Klausel können Sie die Ergebnisse in aufsteigender oder absteigender Reihenfolge sortieren.

Die folgende ORDER BY-Abfrage gibt in aufsteigender Reihenfolge der Preise den Preis, die Beschreibung und die Produkt-ID für alle Produkte zurück:

**Abfrage**

    SELECT p.price, p.description, p.productId
    FROM Products p
    ORDER BY p.price ASC

**Ergebnisse**

```
[
    {
        "price": "14.99",
        "description": "Quick dry crew neck t-shirt",
        "productId": "33218896"
    },
    {
        "price": "49.99",
        "description": "Black wool pea-coat",
        "productId": "33218897"
    }
]
```

## <a name="join-clause"></a>JOIN-Klausel

Mit der JOIN-Klausel können Sie innere Joins für das Dokument und dessen Unterstämme ausführen. Sie können also beispielsweise in der Produktdatenbank Dokumente mit den Versanddaten verknüpfen.  

In der folgenden Abfrage werden die Produkt-IDs der einzelnen Produkte zurückgegeben, für die eine Versandmethode angegeben ist. Wenn Sie ein drittes Produkt ohne Versandeigenschaft hinzufügen, wird dasselbe Ergebnis zurückgegeben, da es aufgrund fehlender Versandeigenschaften ausgeschlossen wird.

**Abfrage**

    SELECT p.productId
    FROM Products p
    JOIN p.shipping

**Ergebnisse**

    [
        {
            "productId": "33218896"
        },
        {
            "productId": "33218897"
        }
    ]

## <a name="geospatial-queries"></a>Geoabfragen

Sie können Geoabfragen mithilfe von GeoJSON-Punkten ausführen. Wenn Sie die Koordinaten in der Datenbank verwenden, können Sie die Entfernung zwischen zwei Punkten berechnen und ermitteln, ob sich ein Punkt, ein Polygon oder ein LineString-Element innerhalb eines anderen Punkts, Polygons oder LineString-Elements befindet.

Hierdurch kann der Benutzer für Produktkatalogdaten seine Standortinformationen eingeben und prüfen, ob es innerhalb eines Radius von 80 Kilometern ein Geschäft gibt, in dem der gesuchte Artikel verfügbar ist. 

## <a name="summary"></a>Zusammenfassung

Wenn Sie in der Lage sind, Ihre gesamten Daten schnell abzufragen, nachdem Sie sie Azure Cosmos DB hinzugefügt haben, und bekannte SQL-Abfragetechniken zu verwenden, können Sie und Ihre Kunden Einblicke in gespeicherte Daten gewinnen.