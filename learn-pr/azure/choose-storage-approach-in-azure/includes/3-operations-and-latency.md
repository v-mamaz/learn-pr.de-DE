Wenn Sie die Art der Daten, mit denen Sie arbeiten (strukturiert, teilweise strukturiert oder unstrukturiert), ermittelt haben, besteht der nächste wichtige Schritt darin, festzustellen, wie die Daten verwendet werden. Ein Onlinehändler würde z.B. wollen, dass Kunden einen schnellen Zugriff auf Produktdaten haben, während Geschäftsbenutzer komplexe Analyseabfragen ausführen können sollen. Arbeiten Sie sich durch diese Anforderungen durch, und berücksichtigen Sie dabei Ihre Datenklassifizierung, um Ihren Datenspeicheransatz zu konzipieren.

Im Folgenden werden einige Fragen vorgestellt, die Sie sich bei der Bestimmung, wie Sie Ihre Daten behandeln, stellen sollten.

## <a name="operations-and-latency"></a>Vorgänge und Latenzen

Welche sind die wichtigsten Vorgänge, die Sie für die einzelnen Datentypen durchführen, und welche Leistungsanforderungen gilt es zu erfüllen?

Führen Sie insbesondere einfache Suchvorgänge anhand einer ID durch? Müssen Sie ein oder mehrere Felder der Datenbank abfragen? Wie viele Erstellungs-, Aktualisierungs- und Löschvorgänge werden Sie aller Voraussicht nach durchführen? Müssen Sie außerdem komplexe Analyseabfragen ausführen? Wie schnell müssen diese Vorgänge ausgeführt werden?

Sehen wir uns die einzelnen Datasets und Anforderungen genauer an.

### <a name="product-catalog-data"></a>Produktkatalogdaten

In dem Szenario eines Onlinehändlers liegt die oberste Priorität für Benutzer bei den Produktkatalogdaten. Beispielsweise möchten Benutzer den Produktkatalog abfragen, um sämtliche Herrenschuhe, Herrenschuhe im Angebot und dann Herrenschuhe im Angebot mit einer bestimmten Größe zu durchsuchen. Sie könnten Kundenanforderungen also nach der Notwendigkeit für eine Vielzahl von erforderlichen Lesevorgängen kategorisieren, mit der Möglichkeit, bestimmte Felder abzufragen.

Wenn Kunden Bestellungen aufgeben, müssen darüber hinaus auch die Mengen an Produktdaten von der Anwendung aktualisiert werden. Diese Aktualisierungsvorgänge müssen genau so schnell wie die Lesevorgänge erfolgen, um zu verhindern, dass Benutzer Artikel in ihren Einkaufskorb legen, die kurz vorher schon ausverkauft sind. Es sind also nicht nur viele Lesevorgänge für Produktkatalogdaten erforderlich, sondern auch viele Schreibvorgänge. Ermitteln Sie in jedem Fall die Prioritäten aller Datenbankbenutzer, nicht nur die der primären Benutzer.

### <a name="photos-and-videos"></a>Fotos und Videos

Für die Fotos und Videos, die auf den Produktseiten angezeigt werden, gelten wiederum andere Anforderungen. Auch hier sind kurze Abrufzeiten für die Anzeige auf der Website vonnöten, separate Abfragen allerdings nicht. Stattdessen können Sie sich auf die Produktabfrage konzentrieren und nur die Video-ID oder -URL als Eigenschaft für die Produktdaten verwenden. Fotos und Videos müssen demnach nur anhand ihrer ID abgefragt werden.

Darüber hinaus nehmen Benutzer keine Aktualisierungen an vorhandenen Fotos oder Videos vor, können jedoch neue Fotos für Produktprüfungen hinzufügen. Beispielsweise könnten sie ein Bild von sich mit ihren neuen Schuhen hochladen. Zudem laden Sie Produktfotos von Ihrem Hersteller hoch und löschen solche, diese Aktualisierungsvorgänge müssen jedoch nicht so schnell wie andere Aktualisierungsvorgänge für Ihre Produktdaten durchgeführt werden. Zusammenfassend lässt sich folgern, dass Fotos und Videos nur nach ID abgefragt werden müssen, um die gesamte Datei zurückzugeben, Erstellungs- und Aktualisierungsvorgänge kommen jedoch seltener vor und weisen eine geringere Priorität auf.  

### <a name="business-data"></a>Geschäftsdaten

Bei Geschäftsdaten bezieht sich die gesamte Analyse auf historische Daten. Keine der ursprünglichen Daten werden basierend auf der Analyse aktualisiert. Die Geschäftsdaten sind damit schreibgeschützt und Benutzer erwarten nicht, dass ihre komplexen Analysevorgänge sofort ausgeführt werden. Latenzen, die bei der Ausgabe der Ergebnisse eventuell auftreten können, sind daher bis zu einem gewissen Grad akzeptabel. Darüber hinaus werden Geschäftsdaten in mehreren Datasets gespeichert, da Benutzer unterschiedliche Zugriffsrechte zum Schreiben von Daten in den einzelnen Datasets besitzen. Business Analysten können jedoch Daten aus allen Datenbanken lesen.

## <a name="summary"></a>Zusammenfassung

Bei der Entscheidung, welche Speicherlösung am besten für Sie geeignet ist, sollten Sie sich auf die Frage konzentrieren, wie Ihre Daten verwendet werden. Wie oft wird auf Ihre Daten zugegriffen? Sind Ihre Daten schreibgeschützt? Ist die Abfragezeit von Relevanz? All diese Fragen spielen für Ihre Entscheidung, welche Speicherlösung am besten für Ihre Daten geeignet ist, eine wichtige Rolle.

