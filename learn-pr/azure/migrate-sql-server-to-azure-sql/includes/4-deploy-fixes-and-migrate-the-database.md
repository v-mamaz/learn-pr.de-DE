Sie haben Ihre lokale Datenbank bewertet, um ihre Kompatibilität und Featureparität mit der Azure SQL-Datenbank zu überprüfen. Da die Kundenbasis Ihres Onlinefahrradhandels auf einen einzelnen geografischen Standort beschränkt ist, können Sie es sich leisten, die Datenbank zu Nebenzeiten (etwa in den frühen Morgenstunden) offline zu schalten.

In diesem Szenario empfiehlt es sich, die Datenbankmigration mithilfe des Datenmigrations-Assistenten durchzuführen, der Sie durch die Migrationsschritte führt. In dieser Einheit erfahren Sie, wie der Datenmigrations-Assistent die eigentliche Migration durchführt.

## <a name="migrate-the-database-using-data-migration-assistant"></a>Migrieren der Datenbank mithilfe des Datenmigrations-Assistenten

Wenn Sie Ihre Datenbank mithilfe des Datenmigrations-Assistenten migrieren möchten, wählen Sie einen Zeitrahmen, in dem in Ihrer Datenbank möglichst wenige Transaktionen stattfinden.

Beheben Sie vor Beginn des Migrationsprozesses alle Fehler, die während der Bewertungsphase gefunden wurden. Der Bewertungsbericht gibt Aufschluss über die Korrekturen, die vor der Durchführung der tatsächlichen Migration vorgenommen werden müssen.

Zur Beschleunigung der Migration können Sie die Leistungsstufe der Azure SQL-Zieldatenbank für den Zeitraum der Migration ändern. Sie können die Leistung auf eine höhere Stufe festlegen (etwa P15), um migrationsbedingte Ausfallzeiten zu verringern. Aus Kostengründen sollten Sie die Leistungsstufe nach der Migration allerdings wieder auf den ursprünglichen Wert zurücksetzen.

Der eigentliche Migrationsprozess umfasst folgende Schritte:

1. Erstellen einer Azure SQL-Datenbank.

1. Erstellen eines neuen Migrationsprojekts.

1. Definieren der Quell- und Zielserver/-datenbanken.

1. Auswählen der zu migrierenden Objekte. Sie müssen nicht alle Objekte migrieren. Achten Sie jedoch darauf, alle abhängigen Objekte einzuschließen. Wenn Sie also beispielsweise eine Ansicht migrieren, die auf eine Tabelle zugreift, müssen Sie auch die Tabelle migrieren.

1. Bereitstellen des Schemas. Dieser Schritt dient zum Migrieren der Datenbankstruktur (nicht der Daten).

1. Migrieren der Daten. In diesem Schritt wird der Inhalt der Tabellen in die Datenbank migriert. Dies ist der zeitaufwendigste Schritt.
