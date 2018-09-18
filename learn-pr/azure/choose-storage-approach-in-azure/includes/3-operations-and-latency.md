Wenn Sie geklärt haben, um welche Art von Daten es geht (strukturiert, teilweise strukturiert oder unstrukturiert), müssen Sie im nächsten Schritt bestimmen, wie Sie die Daten verwenden werden. Als Onlinehändler wissen Sie beispielsweise, dass Kunden schnellen Zugriff auf Produktdaten benötigen, während Geschäftsbenutzer komplexe Analyseabfragen ausführen müssen. Arbeiten Sie sich durch diese Anforderungen durch, und berücksichtigen Sie dabei Ihre Datenklassifizierung, um Ihre Datenspeicherlösung zu planen.

Im Folgenden werden einige Fragen vorgestellt, die Sie sich bei der Bestimmung, wie Sie mit Ihren Daten vorgehen möchten, stellen sollten.

## <a name="operations-and-latency"></a>Vorgänge und Latenz

Was sind die wichtigsten Vorgänge, die Sie für die einzelnen Datentypen durchführen, und welche Leistungsanforderungen müssen erfüllt werden?

Stellen Sie sich folgende Fragen:
* Führen Sie einfache Suchvorgänge anhand einer ID durch? 
* Müssen Sie mindestens ein Feld der Datenbank abfragen? 
* Wie viele Erstellungs-, Aktualisierungs- und Löschvorgänge werden Sie aller Voraussicht nach durchführen? 
* Müssen Sie komplexe Analyseabfragen ausführen? 
* Wie schnell müssen diese Vorgänge ausgeführt werden?

Sehen Sie sich unter Beachtung dieser Fragen die einzelnen Datasets und Anforderungen genauer an.

## <a name="product-catalog-data"></a>Produktkatalogdaten

Für die Produktkatalogdaten im Szenario des Onlinehandels liegt die oberste Priorität bei den Bedürfnissen der Kunden. Beispielsweise möchten Kunden den Produktkatalog abfragen, um sämtliche Herrenschuhe, Herrenschuhe im Angebot und dann Herrenschuhe im Angebot mit einer bestimmten Größe zu durchsuchen. Für die Bedürfnisse der Kunden können viele Lesevorgänge und die Möglichkeit, bestimmte Felder abzufragen, erforderlich sein.

Darüber hinaus muss die Anwendung die Produktmengen aktualisieren, wenn Kunden Bestellungen aufgeben. Diese Aktualisierungsvorgänge müssen genau so schnell wie die Lesevorgänge erfolgen, damit Benutzer keine Artikel in Ihren Einkaufswagen legen, der ausverkauft ist. Es sind also nicht nur viele Lesevorgänge für Produktkatalogdaten erforderlich, sondern auch viele Schreibvorgänge. Ermitteln Sie in jedem Fall die Prioritäten aller Datenbankbenutzer, nicht nur die der primären Benutzer.

## <a name="photos-and-videos"></a>Fotos und Videos

Für die Fotos und Videos, die auf den Produktseiten angezeigt werden, gelten wiederum andere Anforderungen. Sie erfordern schnelle Abrufzeiten, sodass sie zur gleichen Zeit wie die Produktkatalogdaten auf der Website angezeigt werden, jedoch müssen sie nicht unabhängig abgefragt werden. Stattdessen können Sie sich auf die Ergebnisse der Produktabfrage konzentrieren und nur die Video-ID oder -URL als Eigenschaft für die Produktdaten verwenden. Fotos und Videos müssen also nur anhand ihrer ID abgerufen werden.

Darüber hinaus werden Benutzer keine Updates an vorhandenen Fotos oder Videos vornehmen. Sie können jedoch neue Fotos für Produktrezensionen hinzufügen. Beispielsweise kann ein Benutzer ein Bild von sich selbst mit seinen neuen Schuhen hochladen. Als Mitarbeiter laden Sie außerdem Produktfotos von Ihrem Hersteller hoch und löschen sie. Diese Aktualisierungsvorgänge müssen jedoch nicht so schnell wie andere Aktualisierungsvorgänge für Ihre Produktdaten durchgeführt werden. 

Zusammengefasst können Fotos und Videos anhand einer ID abgefragt werden, um die komplette Datei zurückzugeben, jedoch werden diese seltener erstellt und aktualisiert, weshalb hierfür eine geringere Priorität besteht.  

## <a name="business-data"></a>Geschäftsdaten

Bei Geschäftsdaten bezieht sich die gesamte Analyse auf historische Daten. Ursprüngliche Daten werden nicht basierend auf der Analyse aktualisiert, Geschäftsdaten sind also schreibgeschützt. Benutzer erwarten nicht, dass ihre komplexen Analysen sofort ausgeführt werden, daher sind Latenzen bei den Ergebnissen bis zu einem gewissen Grad akzeptabel. Darüber hinaus werden Geschäftsdaten in mehreren Datasets gespeichert, da Benutzer unterschiedliche Zugriffsrechte zum Schreiben von Daten in den einzelnen Datasets besitzen. Business Analysts können Daten aus allen Datenbanken lesen.

## <a name="summary"></a>Zusammenfassung

Bei der Entscheidung, welche Speicherlösung am besten für Sie geeignet ist, sollten Sie sich fragen, wie Ihre Daten verwendet werden. Wie oft wird auf Ihre Daten zugegriffen? Sind Ihre Daten schreibgeschützt? Ist die Abfragezeit von Relevanz? All diese Fragen spielen für Ihre Entscheidung, welche Speicherlösung am besten für Ihre Daten geeignet ist, eine wichtige Rolle.