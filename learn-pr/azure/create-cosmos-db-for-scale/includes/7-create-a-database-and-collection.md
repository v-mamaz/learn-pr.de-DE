## <a name="motivation"></a>Motivation
Nun, dass Sie verstehen, wie Einheiten verwendet werden, um Datenbankdurchsatz zu ermitteln, und wie der Partitionsschlüssel der Strategie für horizontales Skalieren für Ihre Datenbank erstellt, können Sie Ihre Datenbank und Sammlung zu erstellen.

## <a name="creating-your-database-and-collection"></a>Erstellen Ihre Datenbank und Sammlung

1. Klicken Sie im Azure-Portal auf **Daten-Explorer** > **neue Sammlung**.
    
    Der Bereich **Sammlung hinzufügen** wird ganz rechts angezeigt. Möglicherweise müssen Sie nach rechts scrollen, damit Sie ihn sehen.

    ![Daten-Explorer im Azure-Portal, Blatt „Sammlung hinzufügen“](../media/5-create-a-database-and-collection/azure-cosmosdb-data-explorer.png)

2. Geben Sie auf der Seite **Sammlung hinzufügen** die Einstellungen für die neue Sammlung ein.

    Einstellung|Empfohlener Wert|BESCHREIBUNG
    ---|---|---
    Datenbank-ID|Benutzer|Geben Sie *Benutzer* als Namen für die neue Datenbank. Datenbanknamen müssen zwischen 1 und 255 Zeichen lang sein und dürfen weder /, \\, #, ? noch nachgestellte Leerzeichen enthalten.
    Sammlungs-ID|WebCustomers|Geben Sie *WebCustomers* als Namen für die neue Sammlung. Für Sammlungs-IDs gelten dieselben Zeichenanforderungen wie für Datenbanknamen.
    Speicherkapazität| Unbegrenzt |Verwenden Sie den Standardwert **unbegrenzt**. Dieser Wert ist die Speicherkapazität der Datenbank und Ihrer Datenbank, um nach Bedarf skalieren kann.
    Partitionsschlüssel|/UserId|"UserID" wird einen guten Partitionsschlüssel für ein Szenario für die online-Einzelhandel, da so viele Abfragen, um die Kunden-ID basieren
    Throughput|1000 RU|Ändern Sie den Durchsatz auf 1000 anforderungseinheiten pro Sekunde (RU/s). 1000 ist der Mindestwert RU/s, die, den Sie festlegen können, um die automatische Skalierung zu aktivieren.
    
    Vorerst überprüfen Sie nicht die Datenbankoption Durchsatz bereitstellen, und fügen Sie keine eindeutigen Schlüssel der Auflistung hinzu. 
    
3. Klicken Sie auf **OK**.

    Im Daten-Explorer werden die neue Datenbank und die neue Sammlung angezeigt.

    ![Daten-Explorer mit der neuen Datenbank und der neuen Sammlung](../media/5-create-a-database-and-collection/azure-cosmos-db-new-collection.png)

## <a name="summary"></a>Zusammenfassung

In dieser Einheit verwendet Sie Sie zum Erstellen von einer Datenbank und-Sammlung mit Durchsatz und Skalierung für Ihre geschäftsanforderungen geeigneten Einstellungen Kenntnisse von partitionsschlüsseln und anforderungseinheiten.