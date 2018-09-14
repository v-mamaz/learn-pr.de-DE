Sie haben beschlossen, Ihre SQL Server-Datenbanken nach Azure SQL-Datenbank zu migrieren, um von der Skalierbarkeit und Verfügbarkeit von Azure zu profitieren. Sie möchten allerdings sichergehen, dass Azure SQL Server alle Funktionen bietet, die Sie aktuell in Ihrer lokalen SQL Server-Instanz verwenden.

Daher verwenden Sie ein Tool namens Datenmigrations-Assistent, um die Kompatibilität Ihrer vorhandenen Datenbank mit Azure SQL Server zu bewerten.

## <a name="what-is-the-data-migration-assistant-dma"></a>Was ist der Datenmigrations-Assistent (DMA)?

Der Datenmigrations-Assistent wurde speziell für die Analyse lokaler SQL Server-Instanzen entwickelt. Er erkennt und meldet allgemeine Probleme, die die Migration von SQL-Datenbanken nach Azure SQL Server beeinträchtigen können.

Er erkennt Kompatibilitätsprobleme, die eine Migration verhindern können, sowie verwendete Features Ihres lokalen Servers, die nur teilweise oder gar nicht unterstützt werden.

Darüber hinaus liefert er umfassende Empfehlungen für Schritte, die vor der Migration auf Ihrem lokalen Server ausgeführt werden sollten.

### <a name="why-do-you-need-data-migration-assistant"></a>Welche Vorteile bietet der Datenmigrations-Assistent?

Azure SQL-Datenbank wird kontinuierlich weiterentwickelt und unterstützt derzeit noch nicht alle Features von SQL Server.

Aktuelle Angaben hierzu finden Sie in der [Featureliste für Azure SQL-Datenbank](https://docs.microsoft.com/azure/sql-database/sql-database-features).

## <a name="how-to-assess-your-database-using-data-migration-assistant"></a>Wie kann ich meine Datenbank mithilfe des Datenmigrations-Assistenten bewerten?

Die Bewertung einer Datenbank mit dem Datenmigrations-Assistenten umfasst in der Regel folgende Schritte:

- **Installieren des Datenmigrations-Assistenten:** Laden Sie den Datenmigrations-Assistenten unter https://www.microsoft.com/download/details.aspx?id=53595 herunter, und installieren Sie ihn. Azure SQL-Datenbank wird regelmäßig aktualisiert, und auch der Datenmigrations-Assistent wird aktualisiert, um neue Funktionen zu berücksichtigen. Es empfiehlt sich, das Installationsprogramm auszuführen, um sicherzustellen, dass die neueste Version installiert ist.
- **Erstellen einer Bewertung:** Sie erstellen eine neue Bewertung, die Ihre lokale Datenbank und die Zieldatenbank definiert. Sie können auch ein weiteres Ziel von SQL Server für Azure Virtual Machines bewerten, um Alternativmigrationen zu vergleichen.
- **Auswählen von Optionen für Bewertung und Datenbankquellen:** Sie wählen die gewünschten Optionen aus – beispielsweise, ob Sie die Kompatibilität oder die Featureparität zwischen den beiden Datenbanken überprüfen möchten. Danach wählen Sie Ihre Quelldatenbank aus. Sie können mehrere Quellen auswählen.
- **Überprüfen der Ergebnisse:** Anhand der ausführlichen Ergebnisse können Sie Fehler überprüfen und Korrekturmaßnahmen ergreifen. Die Ergebnisse zeigen nicht unterstützte Features mit datenbankübergreifenden Verweisen und SQL Server-Agent. Darüber hinaus erhalten sie eine Liste teilweise unterstützter Features mit Volltextsuche und Überprüfung. Das Ergebnis gibt Aufschluss über mögliche Fehler und enthält Empfehlungen zur Behebung. Die Ergebnisse des Datenmigrations-Assistenten können als JSON-Datei exportiert werden.
