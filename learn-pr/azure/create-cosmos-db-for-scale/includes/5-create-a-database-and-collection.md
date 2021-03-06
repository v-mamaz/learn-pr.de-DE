Da Sie nun wissen, wie mit Anforderungseinheiten der Datenbankdurchsatz ermittelt wird und wie mit dem Partitionsschlüssel die Strategie für horizontales Skalieren Ihrer Datenbank erstellt wird, können Sie Ihre Datenbank und Ihre Sammlung erstellen. Die Durchsatz- und Partitionsschlüsselwerte müssen bei der Erstellung der Sammlung festgelegt werden. Daher wird empfohlen, diese Konzepte vor der Erstellung einer Datenbank zu verstehen.

## <a name="creating-your-database-and-collection"></a>Erstellen der Datenbank und der Sammlung

1. Wählen Sie im Azure-Portal in Ihrer Cosmos DB-Ressource **Daten-Explorer** aus, und klicken Sie auf der Symbolleiste auf die Schaltfläche **Neue Sammlung**.
    
    Der Bereich **Sammlung hinzufügen** wird ganz rechts angezeigt. Sie müssen möglicherweise nach rechts scrollen, um ihn zu sehen.

    ![Daten-Explorer im Azure-Portal, Blatt „Sammlung hinzufügen“](../media/5-azure-cosmosdb-data-explorer.png)

1. Geben Sie auf der Seite **Sammlung hinzufügen** die Einstellungen für die neue Sammlung ein.

    Einstellung | Empfohlener Wert | BESCHREIBUNG
    --------|-----------------|-------------
    Datenbank-ID      | Produkte         | Geben Sie *Products* als Namen für die neue Datenbank ein. Datenbanknamen müssen zwischen 1 und 255 Zeichen lang sein und dürfen weder /, \\, #, ? noch nachgestellte Leerzeichen enthalten.
    Sammlungs-ID    | Kleidung  | Geben Sie *Kleidung* als Namen für die neue Sammlung ein. Für Sammlungs-IDs gelten dieselben Zeichenanforderungen wie für Datenbanknamen.
    Speicherkapazität | Unbegrenzt     | Übernehmen Sie den Standardwert **Unbegrenzt**. Dieser Wert ist die Speicherkapazität der Datenbank, und damit kann Ihre Datenbank nach Bedarf horizontal skaliert werden.
    Partitionsschlüssel    | productId        | „productId“ ist ein guter Partitionsschlüssel für ein Onlinehändlerszenario, da sich viele Abfragen auf die Produkt-ID beziehen.
    Durchsatz       |1000 RU        | Ändern Sie den Durchsatz in 1000 Anforderungseinheiten pro Sekunde (RU/s). 1000 ist der Mindestwert für RU/s, den Sie festlegen können, um die automatische Skalierung zu aktivieren.
    
    Aktivieren Sie erst einmal nicht die Option für den **Durchsatz der Bereitstellungsdatenbank**, und fügen Sie der Sammlung keine eindeutigen Schlüssel hinzu.
    
1. Klicken Sie auf **OK**. Im Daten-Explorer werden die neue Datenbank und die neue Sammlung angezeigt.

    ![Daten-Explorer mit der neuen Datenbank und der neuen Sammlung](../media/5-azure-cosmos-db-new-collection.png)

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie Ihre Kenntnisse im Hinblick auf Partitionsschlüssel und Anforderungseinheiten genutzt, um eine Datenbank und eine Sammlung mit Durchsatz- und Skalierungseinstellungen zu erstellen, die für Ihre Geschäftsanforderungen geeignet sind.