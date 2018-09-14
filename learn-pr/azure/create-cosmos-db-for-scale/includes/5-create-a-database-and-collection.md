Da Sie nun wissen, wie mit Anforderungseinheiten der Datenbankdurchsatz ermittelt wird und wie mit dem Partitionsschlüssel die Strategie für horizontales Skalieren Ihrer Datenbank erstellt wird, können Sie Ihre Datenbank und Ihre Sammlung erstellen. Durchsatz und Partition Key, die Werte beim Erstellen der Sammlung festgelegt werden müssen, empfiehlt sich daher diese Konzepte verstehen, vor dem Erstellen einer Datenbank.

## <a name="creating-your-database-and-collection"></a>Erstellen der Datenbank und der Sammlung

1. Wählen Sie im Azure-Portal in Ihrer Cosmos DB-Ressource **Daten-Explorer** aus, und klicken Sie auf der Symbolleiste auf die Schaltfläche **Neue Sammlung**.
    
    Der Bereich **Sammlung hinzufügen** wird ganz rechts angezeigt. Sie müssen möglicherweise nach rechts scrollen, um ihn zu sehen.

    ![Daten-Explorer im Azure-Portal, Blatt „Sammlung hinzufügen“](../media-draft/5-azure-cosmosdb-data-explorer.png)

1. Geben Sie auf der Seite **Sammlung hinzufügen** die Einstellungen für die neue Sammlung ein.

    Einstellung | Empfohlener Wert | Beschreibung
    --------|-----------------|-------------
    Datenbank-ID      | Produkte         | Geben Sie *Produkte* als Namen für die neue Datenbank. Datenbanknamen müssen zwischen 1 und 255 Zeichen lang sein und dürfen weder /, \\, #, ? noch nachgestellte Leerzeichen enthalten.
    Sammlungs-ID    | Kleidung  | Geben Sie *Clothing* als Namen für die neue Sammlung. Für Sammlungs-IDs gelten dieselben Zeichenanforderungen wie für Datenbanknamen.
    Speicherkapazität | Unbegrenzt     | Übernehmen Sie den Standardwert **Unbegrenzt**. Dieser Wert ist die Speicherkapazität der Datenbank, und damit kann Ihre Datenbank nach Bedarf horizontal skaliert werden.
    Partitionsschlüssel    | productId        | ProductId ist einen guten Partitionsschlüssel für ein online-Einzelhandel-Szenario, da so viele Abfragen für die Produkt-ID basieren
    Throughput       |1000 RU        | Ändern Sie den Durchsatz in 1000 Anforderungseinheiten pro Sekunde (RU/s). 1000 ist der Mindestwert für RU/s, den Sie festlegen können, um die automatische Skalierung zu aktivieren.
    
    Aktivieren Sie erst einmal nicht die Option für den **Durchsatz der Bereitstellungsdatenbank**, und fügen Sie der Sammlung keine eindeutigen Schlüssel hinzu.
    
1. Klicken Sie auf **OK**. Im Daten-Explorer zeigt die neue Datenbank und Sammlung.

    ![Daten-Explorer mit der neuen Datenbank und der neuen Sammlung](../media-draft/5-azure-cosmos-db-new-collection.png)

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie Ihre Kenntnisse im Hinblick auf Partitionsschlüssel und Anforderungseinheiten genutzt, um eine Datenbank und eine Sammlung mit Durchsatz- und Skalierungseinstellungen zu erstellen, die für Ihre Geschäftsanforderungen geeignet sind.