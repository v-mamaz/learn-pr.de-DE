Als Nächstes betrachten wir den Datendurchsatz in unserer Datenbank. Dies ist wichtig, um sicherzustellen, dass wir die Anzahl von Transaktionen für unsere Geschäftsanforderungen verarbeiten können. Anforderungen an den Durchsatz sind nicht immer konsistent. Beispielsweise können Sie eine Einkaufswebsite erstellen, die während der Verkäufe oder Ferien skaliert werden muss. Zu Beginn schätzen wir die Anforderungen an den Datenbankdurchsatz.

## <a name="what-is-database-throughput"></a>Was ist der Datenbankdurchsatz? 

Der Datenbankdurchsatz ist die Anzahl der Lese- und Schreibvorgänge, die Ihre Datenbank in einer einzigen Sekunde durchführen kann. 

Um den Durchsatz strategisch zu skalieren, müssen Sie die Durchsatzanforderungen in Form der Lese- und Schreibvorgänge schätzen, die Sie zu unterschiedlichen Zeiten und für unterschiedliche Dokumentgrößen unterstützen müssen. Wenn Sie richtig schätzen, halten Sie Ihre Benutzer bei Bedarfsspitzen bei Laune. Wenn Sie falsch schätzen, können Ratenbegrenzungen auf Ihre Anforderungen angewandt werden, sodass Vorgänge von Wartezeiten und Wiederholungsversuchen betroffen sind, was zu hoher Latenz führt und zu Lasten der Kundenzufriedenheit geht.

## <a name="what-is-a-request-unit"></a>Was ist eine Anforderungseinheit?

Azure Cosmos DB misst den Durchsatz in **Anforderungseinheiten (Request Unit, RU)**. Die Nutzung von Anforderungseinheiten pro Sekunde wird gemessen, also ist die Maßeinheit **Anforderungseinheiten pro Sekunde (RU/s)**. Sie müssen die RU/s reservieren, die Azure Cosmos DB im Voraus für Sie bereitstellen soll, damit die von Ihnen geschätzte Last verarbeitet werden kann, und Sie können Ihre RU/s jederzeit nach oben oder unten skalieren, um die aktuellen Anforderungen zu erfüllen.

## <a name="request-unit-basics"></a>Grundlegendes zu Anforderungseinheiten

Eine einzelne Anforderungseinheit, 1 RU, entspricht den ungefähren Kosten der Ausführung einer einzelnen GET-Anforderung in einem 1-KB-Dokument mithilfe einer Dokument-ID. Das Ausführen einer GET mithilfe einer Dokument-ID ist eine effiziente Möglichkeit zum Abrufen eines Dokuments, und somit sind die Kosten niedrig. Erstellen, Ersetzen oder Löschen des gleichen Elements erfordern eine zusätzliche Verarbeitung durch den Dienst und daher mehr Anforderungseinheiten.

Die Anzahl der für einen Vorgang verwendeten Anforderungseinheiten ist abhängig von der Dokumentgröße, der Anzahl der Eigenschaften im Dokument, dem ausgeführten Vorgang und einiger zusätzlicher komplexer Konzepte wie Konsistenz und Indizierungsrichtlinie.

In der Tabelle unten ist die Anzahl der Anforderungseinheiten für Elemente drei unterschiedlicher Größen (1 KB, 4 KB und 64 KB) und bei zwei unterschiedlichen Leistungsebenen (500 Lesevorgänge/Sekunde + 100 Schreibvorgänge/Sekunde und 500 Lesevorgänge/Sekunde + 500 Schreibvorgänge/Sekunde) angegeben. In diesem Beispiel wurde die Datenkonsistenz auf **Sitzung** und die Indizierungsrichtlinie auf **Keine** festgelegt.

| Elementgröße | Lesevorgänge/Sekunde | Schreibvorgänge/Sekunde | Anforderungseinheiten
| --- | --- | --- | --- |
| 1 KB | 500 | 100 | (500 * 1) + (100 * 5) = 1.000 RU/s
| 1 KB | 500 | 500 | (500 * 1) + (500 * 5) = 3.000 RU/s
| 4 KB | 500 | 100 | (500 * 1,3) + (100 * 7) = 1.350 RU/s
| 4 KB | 500 | 500 | (500 * 1,3) + (500 * 7) = 4.150 RU/s
| 64 KB | 500 | 100 | (500 * 10) + (100 * 48) = 9.800 RU/s
| 64 KB | 500 | 500 | (500 * 10) + (500 * 48) = 29.000 RU/s
 
Wie Sie sehen: Je größer das Element ist, und je mehr Lese- und Schreibvorgänge erforderlich sind, desto mehr Anforderungseinheiten müssen Sie reservieren. Wenn Sie die Durchsatzanforderungen einer Anwendung schätzen müssen, nutzen Sie den [Capacity Planner](https://www.documentdb.com/capacityplanner) von Azure Cosmos DB, ein Onlinetool, das Ihnen ermöglicht, ein JSON-Beispieldokument hochzuladen und die Anzahl der Vorgänge festzulegen, die Sie pro Sekunde ausführen müssen. Dann wird Ihnen eine geschätzte zu reservierende Gesamtsumme mitgeteilt.

## <a name="exceeding-throughput-limits"></a>Überschreiten von Durchsatzlimits

Wenn Sie nicht genügend Anforderungseinheiten reservieren und versuchen, mehr Daten zu lesen oder zu schreiben, als der bereitgestellte Durchsatz ermöglicht, wird eine Ratenbegrenzung auf Ihre Anforderung angewandt. Wenn eine Ratenbegrenzung auf eine Anforderung angewandt wird, muss die Anforderung nach einem angegebenen Intervall wiederholt werden. Wenn Sie das .NET SDK verwenden, wird die Anforderung automatisch nach Verstreichen der im Retry-After-Header angegebenen Zeitspanne wiederholt.

## <a name="creating-an-account-built-to-scale"></a>Erstellen eines skalierbaren Kontos

Sie können die Anzahl der für eine Datenbank bereitgestellten Anforderungseinheiten jederzeit ändern. In Zeiten mit hohem Volumen können Sie also zentral hochskalieren, um diese hohen Anforderungen zu berücksichtigen, und außerhalb der Spitzenzeiten den bereitgestellten Durchsatz verringern, um Kosten zu senken.

Wenn Sie ein Konto erstellen, können Sie ein Minimum von 400 RU/s oder ein Maximum von 250.000 400 RU/s im Portal bereitstellen. Wenn Sie noch mehr Durchsatz benötigen, füllen Sie ein Ticket im Azure-Portal aus. Für fast alle Konten sollte ein anfänglicher Durchsatz von 1.000 RU/s festgelegt werden, da dies der kleinste Wert ist, bei dem Ihre Datenbank automatisch skaliert, wenn Sie mehr als 10 GB Speicher benötigen sollten. Wenn Sie den anfänglichen Durchsatz auf einen beliebigen Wert unter 1.000 RU/s festlegen, kann Ihre Datenbank nicht auf mehr als 10 GB skalieren, es sei denn, Sie stellen die Datenbank erneut bereit und geben einen Partitionsschlüssel aus. Partitionsschlüssel ermöglichen die schnelle Suche nach Daten in Azure Cosmos DB und ermöglichen Azure Cosmos DB, Ihre Datenbank bei Bedarf automatisch zu skalieren. Partitionsschlüssel werden in der nächsten Einheit behandelt.

## <a name="summary"></a>Zusammenfassung

Sie wissen nun, wie Sie den Durchsatz für Azure Cosmos DB mithilfe von Anforderungseinheiten einschätzen und festlegen. Anforderungseinheiten können jederzeit geändert werden, und die Einstellung auf 1.000 RU/s bei der Erstellung eines Kontos stellt sicher, dass Ihre Datenbank später skaliert werden kann.