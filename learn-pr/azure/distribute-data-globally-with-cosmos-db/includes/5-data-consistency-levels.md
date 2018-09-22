Azure Cosmos DB bietet Entwicklern die Auswahl zwischen fünf klar definierten Konsistenzmodellen aus dem gesamten Konsistenzspektrum: starke Konsistenz, Konsistenz mit begrenzter Veraltung, Sitzungskonsistenz, Präfixkonsistenz und letztliche Konsistenz. Diese Konsistenzebenen ermöglichen es Ihnen, die Verfügbarkeit und Leistung Ihrer Datenbank je nach Ihren Anforderungen zu maximieren. In Fällen, in denen Daten in einer bestimmten Reihenfolge verarbeitet werden müssen, kann starke Konsistenz die richtige Wahl sein. Für Fälle, in denen die Daten nicht sofort konsistent sein müssen, könnte letztliche Konsistenz die richtige Wahl sein. 

In dieser Einheit machen Sie sich mit den verfügbaren Konsistenzebenen in Azure Cosmos DB vertraut und bestimmen die richtige Konsistenzebene für Ihre Online-Bekleidungswebsite.

## <a name="consistency-basics"></a>Grundlagen der Konsistenz

Jedes Datenbankkonto verfügt über eine Standardkonsistenzebene, die die Konsistenz der Daten innerhalb des Kontos bestimmt. An einem Ende des Spektrums befindet sich starke Konsistenz, die eine Linearisierungsgarantie bietet, bei der die Lesezugriffe garantiert die neueste Version eines Elements zurückgeben. Am anderen Ende des Spektrums befindet sich letztliche Konsistenz, die garantiert, dass in Abwesenheit weiterer Schreibvorgänge die Replikate innerhalb der Gruppe schließlich konvergieren. In der Mitte befindet sich die Sitzungskonsistenz, die am häufigsten verwendet wird, weil sie monotone Lesevorgänge, monotone Schreibvorgänge und das Lesen eigener Schreibvorgänge (RYW) garantiert.

![Die fünf Konsistenzebenen in Azure Cosmos DB](../media/5-change-consistency/five-consistency-levels.png)

Die Garantien für jede Konsistenzebene werden in der folgenden Tabelle aufgeführt.
 
**Konsistenzebenen und Garantien**

| Konsistenzebene | Garantien |
| --- | --- |
| Stark | Linearisierbarkeit. Lesevorgänge geben garantiert die neueste Version eines Elements zurück.|
| Begrenzte Veraltung | Präfixkonsistenz. Lesevorgänge bleiben hinter Schreibvorgängen höchstens um Präfix k oder Intervall t zurück. |
| Sitzung   | Präfixkonsistenz. Monotone Lesevorgänge, monotone Schreibvorgänge, Lesen der eigenen Schreibvorgänge, Schreibvorgänge folgen Lesevorgängen. |
| Präfixkonsistenz | Die zurückgegebenen Aktualisierungen sind ein bestimmtes Präfix aller Aktualisierungen ohne Lücken. |
| Letztlich  | Lesevorgänge in falscher Reihenfolge. |

Sie können die Standardkonsistenzebene für Ihr Azure Cosmos DB-Konto im Azure-Portal konfigurieren (und die Konsistenz später für eine bestimmte Leseanforderung außer Kraft setzen). Intern gilt die Standardkonsistenzebene für Daten innerhalb der Partitionssätze, die sich über mehrere Regionen erstrecken können.

In Azure Cosmos DB sind Lesevorgänge mit Sitzungs-, Präfix- und letztlicher Konsistenz zweimal günstiger (was die Nutzung von Anforderungseinheiten betrifft) als Lesevorgänge mit starker Konsistenz oder begrenzter Veraltung.

### <a name="use-of-consistency-levels"></a>Verwenden der Konsistenzebenen

Etwa 73 Prozent der Azure Cosmos DB-Mandanten arbeiten mit Sitzungskonsistenz. 20 Prozent bevorzugen die begrenzte Veraltung. Etwa drei Prozent der Azure Cosmos DB-Kunden experimentieren zunächst mit verschiedenen Konsistenzebenen, ehe sie sich für eine bestimmte Konsistenzoption für ihre Anwendung entscheiden. Nur zwei Prozent der Azure Cosmos DB-Mandanten überschreiben Konsistenzebenen auf der Grundlage individueller Anforderungen.

## <a name="consistency-levels-in-detail"></a>Konsistenzebenen im Detail

Um mehr über die Konsistenzebenen zu erfahren, untersuchen Sie die Konsistenzbeispiele auf Musiknotenbasis im Azure-Portal, und lesen Sie dann die folgenden Informationen zu den einzelnen Ebenen.

1. Klicken Sie im Azure-Portal auf **Standardkonsistenz**.
2. Klicken Sie auf jedes der verschiedenen Konsistenzmodelle, und sehen Sie sich die musikalischen Beispiele an. Sehen Sie sich an, wie Daten in die verschiedenen Regionen geschrieben werden und wie sich die Wahl der Konsistenz auf das Schreiben der Notendaten auswirkt. Beachten Sie, dass die starke Konsistenz ausgegraut ist, da sie nur für Daten verfügbar ist, die in eine Region geschrieben werden.

    ![Erfahren Sie mehr über die Konsistenzeinstellungen im Portal](../media/5-change-consistency/consistency.gif)

Beschäftigen wir uns ausführlicher mit den Konsistenzebenen. Denken Sie darüber nach, wie jede dieser Konsistenzebenen für Ihre Produkt- und Benutzerdaten für Ihre Bekleidungswebsite funktionieren könnte.

### <a name="strong-consistency"></a>Starke Konsistenz

* „Starke Konsistenz“ bietet garantierte [Linearisierbarkeit](https://aphyr.com/posts/313-strong-consistency-models). Dies bedeutet, dass die Lesevorgänge auf jeden Fall die neueste Version eines Elements zurückgeben.
* Mit der Konsistenzebene STARK wird gewährleistet, dass ein Schreibvorgang erst sichtbar ist, nachdem er dauerhaft vom Mehrheitsquorum der Replikate bestätigt wurde. Ein Schreibvorgang wird entweder synchron dauerhaft sowohl vom primären Replikat als auch vom Quorum der sekundären Replikate bestätigt oder abgebrochen. Ein Lesevorgang wird immer von dem Mehrheitslesequorum bestätigt. Ein Client kann niemals einen unbestätigten oder unvollständigen Schreibvorgang sehen, wodurch gewährleistet wird, dass er immer auf die neuesten bestätigten Schreibvorgänge zugreift. 
* Azure Cosmos DB-Konten, die mit dem Modell „Starke Konsistenz“ konfiguriert sind, kann nur eine Azure-Region zugeordnet werden.  
* Die Kosten eines Lesevorgangs (im Sinne genutzter Anforderungseinheiten) mit der Konsistenzebene „Stark“ sind höher als bei „Sitzung“ und „Letztlich“, jedoch identisch mit „Begrenzte Veraltung“.

### <a name="bounded-staleness-consistency"></a>Konsistenzebene „Begrenzte Veraltung“

* Die Konsistenzebene „Begrenzte Veraltung“ garantiert, dass Lesevorgänge hinter Schreibvorgängen höchstens *K* Versionen oder Präfixe eines Elements oder mit dem Zeitintervall *t* zurückbleiben.
* Bei Wahl von „Begrenzte Veraltung“ kann die „Veraltung“ auf zwei Weisen konfiguriert werden: Anzahl der *K*-Versionen des Elements, um das die Lesevorgänge den Schreibvorgängen hinterherhinken, und das Zeitintervall *t*.
* „Begrenzte Veraltung“ bietet eine vollständige globale Reihenfolge (nur nicht innerhalb des „Veraltungsfensters“). Die monotonen Lesegarantien bestehen innerhalb einer Region sowohl innerhalb als auch außerhalb des „Veraltungszeitfensters“.
* Die begrenzte Veraltung bietet eine höhere Konsistenzgarantie als die Konsistenzebenen „Sitzung“, „Präfixkonsistenz“ und „Letztlich“. Für global verteilte Anwendungen wird empfohlen, begrenzte Veraltung in Szenarien zu nutzen, in denen Sie eine hohe Konsistenz, aber auch eine Verfügbarkeit von 99,99 % und niedrige Latenz wünschen.
* Azure Cosmos DB-Konten, die mit der Konsistenz „Begrenzte Veraltung“ konfiguriert sind, kann eine beliebige Anzahl von Azure-Regionen zugeordnet werden. 
* Die Kosten eines Lesevorgangs (im Sinne genutzter Anforderungseinheiten) mit der Konsistenzebene „Begrenzte Veraltung“ sind höher als bei „Sitzung“ und „Letztlich“, jedoch identisch mit „Starke Konsistenz“.

### <a name="session-consistency"></a>Sitzungskonsistenz

* Anders als die globalen Konsistenzmodelle, die von den Konsistenzebenen „Stark“ und „Begrenzte Veraltung“ geboten werden, ist die Konsistenzebene „Sitzung“ auf eine bestimmte Clientsitzung beschränkt.
* Die Konsistenzebene SITZUNG ist ideal für alle Szenarien, an denen eine Geräte- oder Benutzersitzung beteiligt ist, da sie monotone Lese- und Schreibvorgänge garantiert und RYW-Garantien bietet (Read Your Own Writes, eigene Schreibvorgänge lesen).
* Die Konsistenzebene SITZUNG bietet vorhersagbare Konsistenz für eine Sitzung, einen maximalen Lesedurchsatz und Lese- und Schreibvorgänge mit niedrigster Latenz.
* Azure Cosmos DB-Konten, die mit „Sitzungskonsistenz“ konfiguriert sind, kann eine beliebige Anzahl von Azure-Regionen zugeordnet werden.
* Die Kosten für einen Lesevorgang (hinsichtlich genutzter Anforderungseinheiten) mit der Konsistenzebene „Sitzung“ sind geringer als bei „Stark“ und „Begrenzte Veraltung“, aber höher als bei „Letztlich“.

### <a name="consistent-prefix-consistency"></a>Präfixkonsistenz

* Die Präfixkonsistenz garantiert bei Fehlen weiterer Schreibvorgänge, dass es bei den Replikaten innerhalb der Gruppe letztendlich zur Konvergenz kommt. 
* Präfixkonsistenz stellt sicher, dass Lesevorgänge keine Schreibvorgänge außerhalb der Reihenfolge angezeigt werden. Wenn Schreibvorgänge in der Reihenfolge `A, B, C` erfolgen, wird einem Client entweder `A`, `A,B` oder `A,B,C`, aber niemals eine falsche Reihenfolge wie `A,C` oder `B,A,C` angezeigt.
* Azure Cosmos DB-Konten, die mit Präfixkonsistenz konfiguriert sind, kann eine beliebige Anzahl von Azure-Regionen zugeordnet werden. 

### <a name="eventual-consistency"></a>Letztliche Konsistenz

* „Letztliche Konsistenz“ garantiert bei Fehlen weiterer Schreibvorgänge, dass es bei den Replikaten innerhalb der Gruppe letztendlich zur Konvergenz kommt.
* Die Konsistenzebene LETZTLICH stellt die schwächste Form von Konsistenz dar, bei der ein Client ggf. ältere Werte als die ihm zuvor angezeigten abruft.
* Die Konsistenzebene „Letztlich“ bietet die schwächste Lesekonsistenz, jedoch die niedrigste Latenz für Lese- und Schreibvorgänge.
* Azure Cosmos DB-Konten, die mit „Letztliche Konsistenz“ konfiguriert sind, kann eine beliebige Anzahl von Azure-Regionen zugeordnet werden. 
* Die Kosten eines Lesevorgangs (hinsichtlich genutzter Anforderungseinheiten) mit der Ebene „Letztliche Konsistenz“ sind die niedrigsten aller Konsistenzebenen von Azure Cosmos DB.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie gelernt, wie Konsistenzebenen verwendet werden können, um die Hochverfügbarkeit zu maximieren und die Latenzzeit zu minimieren.