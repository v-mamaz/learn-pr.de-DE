Wenn Sie Ihre SQL Server-Datenbanken zu Azure SQL-Datenbank migrieren, können Sie von der Skalierbarkeit und Verfügbarkeit von Azure profitieren. Dabei ist es wichtig, dass Azure SQL Server alle Funktionen umfasst, die Sie aktuell in Ihrer lokalen SQL Server-Instanz verwenden.

Verwenden Sie daher ein Tool namens Datenmigrations-Assistent (DMA), um die Kompatibilität Ihrer vorhandenen Datenbank mit Azure SQL Server zu bewerten.

## <a name="what-is-the-data-migration-assistant-dma"></a>Was ist der Datenmigrations-Assistent (DMA)?

Der DMA wurde speziell für die Analyse lokaler SQL Server-Instanzen entwickelt. Er erkennt und meldet allgemeine Probleme, die die Migration von Datenbanken mit SQL-Datenbank zu Azure SQL Server beeinträchtigen können.

Er erkennt Kompatibilitätsprobleme, die eine Migration verhindern können, sowie verwendete Features Ihres lokalen Servers, die nur teilweise oder gar nicht unterstützt werden.

Darüber hinaus liefert er umfassende Empfehlungen für Schritte, die vor der Migration auf Ihrem lokalen Server ausgeführt werden sollten.

### <a name="why-do-you-need-data-migration-assistant"></a>Welche Vorteile bietet der Datenmigrations-Assistent?

Azure SQL-Datenbank wird kontinuierlich weiterentwickelt und unterstützt derzeit noch nicht alle Features von SQL Server.

Aktuelle Angaben hierzu finden Sie in der [Featureliste für Azure SQL-Datenbank](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-features).

## <a name="how-to-assess-your-database-using-data-migration-assistant"></a>Wie kann ich meine Datenbank mithilfe des Datenmigrations-Assistenten bewerten?

Die Bewertung einer Datenbank mit dem Datenmigrations-Assistenten umfasst in der Regel folgende Schritte:

- **Installieren des Datenmigrations-Assistenten:** Laden Sie den DMA unter https://www.microsoft.com/en-us/download/details.aspx?id=53595 herunter. Azure SQL-Datenbank wird regelmäßig aktualisiert, und auch der DMA wird aktualisiert, um neue Funktionen zu berücksichtigen. Es wird empfohlen, das Installationsprogramm auszuführen, um sicherzustellen, dass die neueste Version installiert ist.
- **Erstellen einer Bewertung:** Sie erstellen eine neue Bewertung, die Ihre lokale Datenbank und die Zieldatenbank definiert. Sie können auch ein weiteres Ziel von SQL Server für Azure Virtual Machines prüfen, um Alternativmigrationen zu vergleichen.
- **Auswählen von Optionen zur Prüfung und für Datenbankquellen:** Treffen Sie eine Auswahl aus den unterschiedlichen Optionen. Entscheiden Sie z.B., ob Sie die Kompatibilität oder die Featureparität für die beiden Datenbanken überprüfen möchten. Wählen Sie danach Ihre Quelldatenbank aus. Sie können mehrere Quellen auswählen.
- **Überprüfen der Ergebnisse:** Anhand der ausführlichen Ergebnisse können Sie Fehler überprüfen und entsprechende Maßnahmen ergreifen. Die Ergebnisse zeigen nicht unterstützte Features mit datenbankübergreifenden Verweisen und dem SQL Server-Agent auf. Darüber hinaus erhalten sie eine Liste teilweise unterstützter Features mit Volltextsuche und Überprüfung. Das Ergebnis gibt Aufschluss über mögliche Fehler und enthält Empfehlungen zur Behebung. Sie können DMA-Ergebnisse in einer JSON-Datei exportieren.
