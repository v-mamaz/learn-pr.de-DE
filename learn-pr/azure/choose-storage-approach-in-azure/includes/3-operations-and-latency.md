Wenn Sie die Art der Daten ermittelt haben, die Sie mit (strukturierten, teilweise strukturiert oder unstrukturiert) arbeiten, besteht der nächste Schritt, um zu bestimmen, wie Sie die Daten verwenden. Als ein Onlinehändler wissen Sie z. B. Kunden benötigten schnellen Zugriff auf die Produktdaten an, und Geschäftskunden benötigen, um komplexe analytische Abfragen auszuführen. Wie Sie diese Anforderungen arbeiten, können Ihre Klassifizierung von Daten berücksichtigt dass, Sie beginnen, Ihre speicherlösung planen.

Hier gehen Sie durch einige der Fragen beim bestimmen, was Sie mit Ihren Daten.

## <a name="operations-and-latency"></a>Vorgänge und Latenzen

Was sind die wichtigsten Vorgänge, die Sie für jeden Datentyp abgeschlossen werden müssen, und was die sind Erfüllung der leistungsanforderungen?

Stellen Sie sich diese Fragen:
* Werden Sie einfach mit einer ID-Suchvorgänge durchführen? 
* Müssen Sie ein oder mehrere Felder der Datenbank abfragen? 
* Wie viele Erstellungs-, Aktualisierungs- und Löschvorgänge werden Sie aller Voraussicht nach durchführen? 
* Müssen Sie außerdem komplexe Analyseabfragen ausführen? 
* Wie schnell müssen diese Vorgänge Sie ausführen?

Sehen wir uns die einzelnen der Datasets mit diesen Fragen, Bedenken Sie, und erläutert die Anforderungen.

## <a name="product-catalog-data"></a>Produktkatalogdaten

Für Produktkatalogdaten im online-Einzelhandel-Szenario werden Anforderungen des Kunden die höchste Priorität. Kunden sollten den Produktkatalog zu suchen, z. B. alle Männer-Schuhe, und klicken Sie dann Männer-Schuhe Verkauf von Karten und klicken Sie dann Männer-Schuhe Verkauf von Karten in einer bestimmten Größe Abfragen. Daher möglicherweise kundenanforderungen viele Lesevorgänge an, mit der Möglichkeit, um eine Abfrage auf bestimmte Felder erforderlich.

Wenn Kunden Bestellungen aufgeben, muss die Anwendung darüber hinaus Produktmengen aktualisieren. Die Updatevorgänge müssen nur so schnell wie die Lesevorgänge ausgeführt werden, sodass Benutzer ein Element in ihre Einkaufswagen ablegen, wenn dieses Element nur sich verkauft hat nicht. Es sind also nicht nur viele Lesevorgänge für Produktkatalogdaten erforderlich, sondern auch viele Schreibvorgänge. Ermitteln Sie in jedem Fall die Prioritäten aller Datenbankbenutzer, nicht nur die der primären Benutzer.

## <a name="photos-and-videos"></a>Fotos und Videos

Haben unterschiedliche Anforderungen, Fotos und Videos, die auf den Produktseiten angezeigt werden. Sie benötigen die schnellen Abrufzeiten, sodass sie auf der Website zur gleichen Zeit wie Produktkatalogdaten angezeigt werden, aber sie müssen nicht unabhängig voneinander abgefragt werden. Stattdessen können Sie die Ergebnisse der Abfrage Produkt abhängig und der video-ID oder die URL als Eigenschaft für die Produktdaten enthalten. Daher müssen Fotos und Videos anhand ihrer ID. abgerufen werden.

Benutzer werden darüber hinaus keine Updates auf vorhandene Fotos oder Videos vornehmen. Sie können jedoch neue Fotos für Produktbesprechungen hinzufügen. Beispielsweise kann ein Benutzer ein Abbild von sich selbst aus ihren neuen Schuhe mit hochladen. Als Mitarbeiter Sie auch hochladen und Löschen von Produktfotos Hersteller Ihres, aber, dass Update nicht so schnell wie Ihre anderen Produkt Datenupdates durchgeführt. 

Zusammenfassend lässt sich sagen, Fotos und Videos können abgefragt werden nach ID zurückgeben die gesamte Datei, aber erstellt und Updates werden weniger häufig und weniger mit einer Priorität.  

## <a name="business-data"></a>Geschäftsdaten

Bei Geschäftsdaten bezieht sich die gesamte Analyse auf historische Daten. Keine ursprünglichen Daten basieren, auf die Analyse, Geschäftsdaten nur-Lese aktualisiert. Benutzer erwarten nicht ihre komplexer Analytik an eine sofortige Ausführung, ist daher von Wartezeiten entstehen in den Ergebnissen zulässig. Darüber hinaus werden Geschäftsdaten in mehreren Datasets gespeichert, da Benutzer unterschiedliche Zugriffsrechte zum Schreiben von Daten in den einzelnen Datasets besitzen. Allerdings werden Wirtschaftsanalytiker aus allen Datenbanken lesen.

## <a name="summary"></a>Zusammenfassung

Bei der Entscheidung, welche speicherlösung verwenden, sollten überlegen Sie, wie Ihre Daten verwendet werden. Wie oft wird auf Ihre Daten zugegriffen? Sind Ihre Daten schreibgeschützt? Ist die Abfragezeit von Relevanz? All diese Fragen spielen für Ihre Entscheidung, welche Speicherlösung am besten für Ihre Daten geeignet ist, eine wichtige Rolle.