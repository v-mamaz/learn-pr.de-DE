Um eine großartige Benutzererfahrung in einem E-Commerce-Szenario wie dem Ihren zu gewährleisten, sind eine hohe Verfügbarkeit und geringe Latenzzeiten erforderlich.

Durch die Aktivierung der Multimasterunterstützung für das soeben von Ihnen erstellte Azure Cosmos DB-Konto ergeben sich für beide Leistungsaspekte mehrere Vorteile, und alle Vorteile werden durch die von Azure Cosmos DB bereitgestellten finanziell gesicherten SLAs (Vereinbarungen zum Servicelevel) garantiert.

## <a name="what-is-multi-master-support"></a>Was ist Multimasterunterstützung?

Multimasterunterstützung ist eine Option, die für neue Azure Cosmos DB-Konten aktiviert werden kann. Sobald das Konto in mehrere Regionen repliziert wurde, ist jede Region eine Masterregion, die gleichermaßen an einem Write-anywhere-Modell teilnimmt, das auch als Aktiv/Aktiv-Muster bezeichnet wird.

In Azure Cosmos DB-Regionen, die als Masterregionen in einer Multimasterkonfiguration fungieren, werden Daten, die in alle Replikate geschrieben werden, automatisch konvergiert. Zudem wird die globale Konsistenz und Datenintegrität sichergestellt.

Mit der Multimasterunterstützung von Azure Cosmos DB können Sie Schreibvorgänge für jeden Container in einer schreibaktivierten Region weltweit durchführen. Geschriebene Daten werden sofort in alle anderen Regionen übertragen.  

## <a name="what-are-the-benefits-of-multi-master-support"></a>Was sind die Vorteile von Multimasterunterstützung?

Multimasterunterstützung bietet die folgenden Vorteile:

* Schreiblatenz im einstelligen Bereich: Multimasterkonten weisen eine verbesserte Schreiblatenz von < 10 ms für 99 % der Schreibvorgänge auf (gegenüber < 15 ms für Nicht-Multimasterkonten).
* 99,999 % Lese-/Schreibverfügbarkeit: Die Schreibverfügbarkeit von Multimasterkonten steigt auf 99,999 % (gegenüber 99,99 % bei Nicht-Multimasterkonten).
* Unbegrenzte Schreibskalierbarkeit und Durchsatz: Mit Multimasterkonten können Sie in jede Region schreiben und unbegrenzte Schreibskalierbarkeit und Durchsatz für die Unterstützung von Milliarden von Geräten bereitstellen.
* Integrierte Konfliktlösung: Multimasterkonten verfügen über drei Methoden zur Konfliktlösung, um die globale Datenintegrität und Konsistenz zu gewährleisten. 

## <a name="conflict-resolution"></a>Konfliktlösung

Mit dem Hinzufügen von Multimasterunterstützung ergibt sich die Möglichkeit, Konflikte bei Schreibvorgängen in verschiedenen Regionen zu lösen. Konflikte sind in der Azure Cosmos DB extrem selten und können nur auftreten, wenn ein Element gleichzeitig in mehreren Regionen geändert wird, bevor die Weitergabe zwischen den Regionen stattgefunden hat. Angesichts der Geschwindigkeit, mit der die Replikation global erfolgt, sollten Sie dies gar nicht oder nur selten erleben. Azure Cosmos DB bietet jedoch Konfliktlösungsmodi, die es den Benutzern ermöglichen, zu entscheiden, wie sie mit Szenarien umgehen, in denen derselbe Datensatz gleichzeitig von verschiedenen Schreibvorgängen in zwei oder mehr Regionen aktualisiert wird.  

Azure Cosmos DB bietet drei Konfliktlösungsmodi an. 
* **Last-Writer-Wins (LWW)**: Konflikte werden basierend auf dem Wert einer benutzerdefinierten ganzzahligen Eigenschaft im Dokument gelöst. Standardmäßig wird „_ts“ verwendet, um das zuletzt geschriebene Dokument zu bestimmen. Last-Writer-Wins ist der Standardmechanismus für die Konfliktbehandlung.
* **Benutzerdefiniert – Benutzerdefinierte Prozedur**: Sie können die Konfliktlösung vollständig steuern, indem Sie eine benutzerdefinierte Prozedur bei der Sammlung registrieren. Eine benutzerdefinierte Prozedur ist eine besondere Art von gespeicherter Prozedur mit einer ganz bestimmten Signatur. Wenn die benutzerdefinierte Prozedur fehlschlägt oder nicht vorhanden ist, fügt Azure Cosmos DB alle Konflikte dem schreibgeschützten Konfliktfeed hinzu, damit sie asynchron verarbeitet werden können.  
* **Benutzerdefiniert – Asynchron**: Azure Cosmos DB schließt alle Konflikte vom Commitvorgang aus und registriert sie im schreibgeschützten Konfliktfeed zur verzögerten Lösung durch die Anwendung des Benutzers. Die Anwendung kann die Konfliktlösung asynchron ausführen und jede Logik verwenden oder auf eine externe Quelle, eine Anwendung oder einen externen Dienst verweisen, um den Konflikt zu lösen.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie sich mit Multimasterkonten vertraut gemacht, die es Ihnen ermöglichen, Daten in mehrere Regionen zu schreiben, um die Verfügbarkeit und Leistung zu verbessern.