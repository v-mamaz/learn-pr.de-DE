Beim Erstellen einer Anwendung spielt die Servicequalität für Benutzer eine entscheidende Rolle. Hierzu gehören auch schnelle Datenabrufe. Üblicherweise ist das Abrufen von Daten langsam. Bei häufigen Lesezugriffen kann dies die Servicequalität negativ beeinflussen. Das cachefremde Muster (Cache-Aside Pattern) wird angewendet, um einen Cache zusammen mit einer Datenbank so zu implementieren, dass Daten, auf die besonders häufig zugegriffen wird, möglichst schnell zurückgegeben werden.

Hier erfahren Sie, wie Sie mithilfe dieses Musters wichtige Daten schnell abfragen können.

## <a name="what-is-the-cache-aside-pattern"></a>Was wird unter dem cachefremden Muster verstanden?

Das cachefremde Muster gibt vor, dass beim Abrufen von Daten aus einer Datenquelle (beispielsweise aus einer relationalen Datenbank) zunächst die Daten im Cache überprüft werden sollten. Wenn die Daten sich im Cache befinden, sollten sie genutzt werden. Andernfalls sollte die Datenbank abgefragt werden. Wenn anschließend die Daten an den Benutzer gesendet werden, sollten sie dem Cache hinzugefügt werden. Dadurch können Sie auf die Daten im Cache zugreifen, wenn diese beim nächsten Mal benötigt werden.

## <a name="when-to-implement-cache-aside-pattern"></a>In welchen Fällen sollte das cachefremde Muster implementiert werden?

Datenbankabfragen sind in der Regel langsam. Dies liegt daran, dass komplexe Abfragen durchgeführt werden und ein Abfrageausführungsplan vorbereit wird. Anschließend müssen die Abfrage ausgeführt und das Ergebnis vorbereit werden. In einigen Fällen werden bei diesem Vorgang möglicherweise auch Daten vom Datenträger gelesen. Zwar lassen sich auf Datenbankebene Optimierungen vornehmen, bei denen beispielsweise Abfragen vorkompiliert und einige Daten in den Speicher geladen werden. Die Ausführung der Abfrage und die Vorbereitung der Ergebnisse finden jedoch immer erst beim Abruf von Daten aus der Datenbank statt.

Dieses Problem lässt sich mithilfe des cachefremden Musters lösen. Dieses sieht auch weiterhin eine Anwendung und eine Datenbank vor. Zusätzlich ist jedoch auch ein Cache vorhanden. Dieser speichert Daten im Speicher, damit ein Zugriff auf das Dateisystem vermieden wird. Caches speichern Daten in sehr einfachen Datenstrukturen wie z.B. Schlüssel-Wert-Paaren. Dadurch wird verhindert, dass komplexen Abfragen ausgeführt werden, um Daten zu sammeln oder Indizes beim Schreiben von Daten zu verwalten. Ein Cache ist daher üblicherweise leistungsfähiger als eine Datenbank. Wenn Sie eine Anwendung verwenden, versucht diese zunächst, Daten aus dem Cache zu lesen. Wenn sich die angeforderten Daten nicht im Cache befinden, ruft die Anwendung diese wie üblich aus der Datenbank ab. Die Daten werden anschließend allerdings im Cache gespeichert, damit sie für die nachfolgenden Anforderungen bereitstehen. Wenn ein Benutzer beim nächsten Mal die Daten anfordert, werden diese direkt aus dem Cache zurückgegeben.

![Laden von Daten in den Cache](../media-draft/cache-aside-set-cache.png)

### <a name="how-to-manage-updating-data"></a>Verwalten von Daten, die aktualisiert werden

Bei der Implementierung des cachefremden Musters stoßen Sie auf ein Problem. Da Ihre Daten nun in einem Cache und in einem Datenspeicher gespeichert werden, können Probleme auftreten, wenn Sie versuchen, eine Aktualisierung vorzunehmen. Wenn Sie beispielsweise Ihre Daten aktualisieren möchten, müssen Sie diesen Vorgang sowohl für den Cache als auch für den Datenspeicher ausführen.

Die Lösung dieses Problems besteht innerhalb des cachefremden Musters darin, die Gültigkeit der Daten im Cache aufzuheben. Bei der Aktualisierung von Daten in Ihrer Anwendung sollten Sie zuerst die Daten im Cache löschen und anschließend Änderungen direkt an der Datenquelle vornehmen. Dadurch sind die Daten bei der nächsten Anforderung nicht mehr im Cache, und der Vorgang wiederholt sich. 

![Aufheben der Gültigkeit von zwischengespeicherten Daten](../media-draft/cache-aside-invalidate.png)

## <a name="considerations-for-using-the-cache-aside-pattern"></a>Überlegungen zur Verwendung des cachefremden Musters

Sie sollten genau überlegen, welche Daten im Cache gespeichert werden. Nicht alle Daten eignen sich hierfür.

- **Lebensdauer:** Stellen Sie sicher, dass die Ablaufrichtlinie auf die Häufigkeit des Datenzugriffs abgestimmt ist. Nur so kann das cachefremde Muster wirksam eingesetzt werden. Wenn der festgelegte Ablaufzeitraum zu kurz ist, kann dies dazu führen, dass Anwendungen Daten kontinuierlich aus dem Datenspeicher abrufen und dem Cache hinzufügen.

- **Entfernen von Daten:** Caches weisen im Vergleich zu üblichen Datenspeichern nur eine eingeschränkte Größe auf. Daten müssen daher ggf. entfernt werden. Achten Sie deswegen darauf, eine geeignete Entfernungsrichtlinie für Ihre Daten zu verwenden.

- **Auffüllen des Caches im Vorfeld:** Um das cachefremde Muster effektiv einzusetzen, füllen viele Lösungen den Cache vorab mit Daten auf, die voraussichtlich häufig abgefragt werden.

- **Konsistenz:** Durch das Implementieren des cachefremden Musters ist die Konsistenz zwischen dem Datenspeicher und dem Cache nicht garantiert. Daten in einem Datenspeicher können ohne Benachrichtigung des Caches geändert werden. Dies kann zu schwerwiegenden Synchronisierungsproblemen führen.

Das cachefremde Muster ist nützlich, wenn Sie häufig Daten aus einer Datenquelle abfragen müssen, die auf einen Datenträger zurückgreift. Durch die Umsetzung dieses Musters speichern Sie wichtige Daten in einem Cache, um diese schneller abrufen zu können. 