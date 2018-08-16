## <a name="motivation"></a>Motivation

Als Nächstes betrachten wir die Daten in der gesamten für unsere Datenbank. Dies ist wichtig, um sicherzustellen, dass wir die Anzahl von Transaktionen für unsere Anforderungen verarbeiten kann. Durchsatzanforderungen sind nicht immer konsistenten, z. B. möglicherweise werden Erstellung einer Shoppping-Website, die während der Umsätze oder Feiertage skaliert. Beginnen wir schätzen der durchsatzanforderungen Ihrer Datenbank.

## <a name="what-is-database-throughput"></a>Was ist datenbankdurchsatzes? 

Datenbankdurchsatz ist die Anzahl der Lesevorgänge, und schreibt, dass Ihre Datenbank in einer einzigen Sekunde ausführen kann. 

Um die Skalierung des Durchsatzes strategisch, müssen Sie schätzen Sie der Durchsatz benötigt, indem die Schätzung der Anzahl der Lesevorgänge, und schreibt, müssen Sie die zu unterschiedlichen Zeiten und für die unterschiedlichen Dokumentgrößen unterstützen. Wenn Sie richtig zu schätzen, halten Sie Ihre Benutzer viel Spaß beim bei Bedarf Spitzen. Wenn Sie nicht ordnungsgemäß zu schätzen, können Ihre Anforderungen Rate begrenzt, und Vorgänge müssen Sie warten, und wiederholen, wahrscheinlich verursachen hohe Latenz und nicht zufrieden Kunden.

## <a name="what-is-a-request-unit"></a>Was ist eine Anforderungseinheit?

Azure Cosmos DB misst den Durchsatz, die mit dem Namen einer **Anforderungseinheiten**. Fordern Sie die Auslastung wird pro Sekunde gemessen, also die Maßeinheit **Anforderungseinheiten pro Sekunde (RU/s)**. Reservieren Sie die Anzahl von Anforderungseinheiten pro Sekunde, die Sie Azure Cosmos DB im Voraus bereitstellen möchten, daher wird die Last zu verarbeiten, die Sie geschätzte haben, und Sie können Ihre RU/Sek. zentral, hoch- oder Herunterskalieren jederzeit an aktuelle Anforderungen zu erfüllen.

## <a name="request-unit-basics"></a>Grundlagen der Einheit anfordern

Eine einzelne Anforderungseinheit 1 RU, entspricht der ungefähren Kosten der Ausführung einer einzelnen GET-Anforderung in einem 1-KB-Dokument mithilfe eines Dokuments-ID. Durch das Ausführen eines GET mithilfe eines Dokument ID ist eine effiziente Möglichkeit zum Abrufen eines Dokuments, und somit die Kosten ist klein. Erstellen, ersetzen oder löschen das gleiche Element erfordert eine zusätzliche Verarbeitung durch den Dienst, und benötigt daher mehr anforderungseinheiten.

Die Anzahl der anforderungseinheiten für einen Vorgang ändert sich je nach die Dokumentgröße, die Anzahl der Eigenschaften in das Dokument, der Vorgang ausgeführt wird und einige zusätzliche komplexe Konzepte wie Konsistenz und die indizierungsrichtlinie verwendet.

Die folgende Tabelle zeigt die Anzahl von anforderungseinheiten, die erforderlich sind, für die Elemente der drei unterschiedlichen Größen (1 KB, 4 KB und 64 KB) und bei zwei unterschiedlichen Leistungsebenen (500 Lesevorgänge/Sekunde + 100 Schreibvorgänge/Sekunde und 500 Lesevorgänge/Sekunde + 500 Schreibvorgänge/Sekunde). In diesem Beispiel wurde die Datenkonsistenz auf **Sitzung** und die Indizierungsrichtlinie auf **Keine** festgelegt.

| Elementgröße | Lesevorgänge/Sekunde | Schreibvorgänge/Sekunde | Anforderungseinheiten
| --- | --- | --- | --- |
| 1 KB | 500 | 100 | (500 * 1) + (100 * 5) = 1.000 RU/s
| 1 KB | 500 | 500 | (500 * 1) + (500 * 5) = 3.000 RU/s
| 4 KB | 500 | 100 | (500 * 1,3) + (100 * 7) = 1.350 RU/s
| 4 KB | 500 | 500 | (500 * 1,3) + (500 * 7) = 4.150 RU/s
| 64 KB | 500 | 100 | (500 * 10) + (100 * 48) = 9.800 RU/s
| 64 KB | 500 | 500 | (500 * 10) + (500 * 48) = 29.000 RU/s
 
Wie Sie sehen können, desto größer wird das Element, und die weitere Lese- und Schreibvorgänge erforderlich sind, desto mehr Einheiten, die Sie reservieren möchten anfordern. Wenn Sie zum Schätzen der durchsatzanforderungen einer Anwendung, die Azure Cosmos DB müssen [Capacity Planner](https://www.documentdb.com/capacityplanner) ist ein online-Tool, mit dem Sie ein JSON-Beispieldokument hochladen, legen Sie die Anzahl von Vorgängen pro Sekunde abgeschlossen werden sollen, und Klicken Sie dann bietet eine geschätzte Gesamtsumme, zu reservieren.

## <a name="exceeding-throughput-limits"></a>Größer als durchsatzlimits

Wenn Sie nicht genügend anforderungseinheiten reservieren und Sie versuchen, zu lesen oder Schreiben von mehr Daten als der bereitgestellte Durchsatz ermöglicht, wird Ihre Anforderung begrenzt werden. Wenn eine Anforderung begrenzt ist, muss die Anforderung erneut nach einem angegebenen Intervall wiederholt werden. Wenn Sie das .NET SDK verwenden, wird die Anforderung automatisch wiederholt werden, nach einer Wartezeit auf die Zeitspanne, die in der Retry-after-Header angegeben.

## <a name="creating-an-account-built-to-scale"></a>Erstellen eines Kontos zur Skala erstellt

Sie können die Anzahl der anforderungseinheiten für eine Datenbank bereitgestellt wird, jederzeit ändern. Daher können während des Zeitraums hoher Volume Sie zentral hochskalieren, berücksichtigen diese High-Anforderungen, und verringern Sie bereitgestellten Durchsatz während der nicht-Spitzenzeiten Kosten senken.

Wenn Sie ein Konto erstellen, können Sie ein Minimum von 400 RU/s "oder" maximal 250.000 Anforderungseinheiten pro Sekunde in das Portal bereitstellen. Wenn Sie noch mehr Durchsatz benötigen, füllen Sie Sie ein Ticket im Azure-Portal. Festlegen des anfänglichen Durchsatzes auf 1000 RU/s empfiehlt sich für fast alle Konten, wie es der minimale Wert beträgt in dem Ihre Datenbank automatisch werden Sie mehr als 10 GB Speicher benötigen. Wenn Sie dem anfänglichen Durchsatz weniger als 1000 RU/s auf einen beliebigen Wert festlegen, wird Ihre Datenbank werden keine Skalierung auf mehr als 10 GB, es sei denn, Sie die Datenbank erneut, und geben Sie einen Partitionsschlüssel. Partitionsschlüssel ermöglichen die schnelle Suche von Daten in Azure Cosmos DB, und aktivieren sie automatische Skalierung Ihrer Datenbank bei Bedarf. Partitionsschlüssel werden in die nächste Einheit behandelt.

## <a name="summary"></a>Zusammenfassung

Sie kennen, wissen, wie zum schätzen und Bereich Durchsatz für Azure Cosmos DB mithilfe von Anforderungseinheiten. Anforderungseinheiten können jederzeit geändert werden und über die Einstellungen 1000 RU/Sek., wenn Sie ein Konto erstellen hilft stellen Sie sicher, dass Ihre Datenbank später skalieren kann.