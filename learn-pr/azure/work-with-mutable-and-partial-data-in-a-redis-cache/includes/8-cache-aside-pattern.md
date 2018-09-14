Wenn eine Anwendung erstellen, möchten Sie ein optimales Benutzererlebnis zu bieten, und ein Teil davon ist die schnelle Abrufen von Daten. Abrufen von Daten aus einer Datenbank ist in der Regel einen langsamen Prozess aus, und wenn diese Daten oft gelesen werden, kann dies eine schlechte benutzererfahrung bieten. Das Cache-Aside-Muster beschreibt, wie Sie einen Cache in Verbindung mit einer-Datenbank wird zurückgegeben, die meisten Daten so schnell wie möglich häufig verwendete implementieren können.

Hier erfahren Sie, wie das Cache-Aside-Muster verwendet werden kann, um sicherzustellen, dass Ihre wichtigen Daten schnell zugegriffen werden kann.

## <a name="what-is-the-cache-aside-pattern"></a>Was ist der Cache-Aside-Muster?

Das Cache-Aside-Muster schreibt vor, dass wenn Sie zum Abrufen von Daten aus einer Datenquelle, wie eine relationale Datenbank, müssen Sie zuerst für die Daten im Cache überprüfen soll. Wenn die Daten im Cache befindet, verwenden Sie diese. Wenn die Daten sind nicht in Ihrem Cache, und klicken Sie auf die Datenbank abzufragen, und wenn Sie die Daten zurück an den Benutzer zurückgeben, fügen Sie sie mit dem Cache hinzu. Diese werden dann können Sie Zugriff auf die Daten aus dem Cache das nächste Mal, das wenn er benötigt wird.

## <a name="when-to-implement-the-cache-aside-pattern"></a>Wenn die Cache-Aside-Muster zu implementieren?

Lesen von Daten aus einer Datenbank ist in der Regel einen langsamen Prozess. Es beinhaltet die Kompilierung einer komplexen Abfrage, die zur Vorbereitung eines Abfrageplans für die Ausführung, Ausführung der Abfrage und klicken Sie dann zur Vorbereitung des Ergebnisses. In einigen Fällen kann dieser Prozess die Daten vom Datenträger auch lesen. Es gibt Optimierungen, die auf Datenbankebene, z. B. Abfragen vorzukompilieren und Laden einige der Daten im Arbeitsspeicher erfolgen können. Die Ausführung der Abfrage und die Vorbereitung des Ergebnisses werden jedoch in der immer ausgeführt, beim Abrufen von Daten aus einer Datenbank.

Wir können dieses Problem lösen, mit dem Cache-Aside-Muster. Im Cache-Aside-Muster ist die Anwendung und die Datenbank auch weiterhin vorhanden, aber jetzt haben wir auch einen Cache. Ein Cache speichert seine Daten im Arbeitsspeicher, sodass es nicht für die Interaktion mit dem Dateisystem. Caches speichern Sie Daten auch in sehr einfache Datenstrukturen, z. B. Schlüssel-/Wertpaaren, sodass sie keine komplexen Abfragen zum Sammeln von Daten oder zum Verwalten von Indizes beim Schreiben von Daten ausführen. Aus diesem Grund ist ein Cache in der Regel leistungsfähiger als eine Datenbank. Wenn Sie eine Anwendung verwenden, wird versucht, Daten zuerst aus dem Cache zu lesen. Wenn die angeforderten Daten nicht im Cache vorhanden ist, wird die Anwendung es aus der Datenbank abrufen, wie immer war auch der Fall. Allerdings speichert er die Daten dann in den Cache für nachfolgende Anforderungen. Wenn jeder Benutzer die Daten anfordert nächsten wird es aus dem Cache direkt zurückgegeben.

![Diagramm des Laden von Daten in cache](../media-draft/cache-aside-set-cache.png)

### <a name="how-to-manage-updating-data"></a>Gewusst wie: Aktualisieren von Daten zu verwalten.

Wenn Sie das Cache-Aside-Muster implementieren, führen Sie ein kleines Problem. Da Ihre Daten nun in einem Cache und einem Datenspeicher gespeichert werden, können Probleme auftreten, wenn Sie versuchen, eine Aktualisierung vornehmen. Beispielsweise würde um Ihre Daten zu aktualisieren, Sie müssen den Cache und dem Datenspeicher zu aktualisieren.

Die Lösung für dieses Problem in den Cache-Aside-Muster werden die Daten im Cache für ungültig zu erklären. Wenn Sie Daten in Ihrer Anwendung aktualisieren, sollten Sie zuerst die Daten im Cache löschen und dann die Änderungen direkt an die Datenquelle vornehmen. Dadurch, nächste Mal, wenn die Daten angefordert werden, nicht im Cache vorhanden, und der Prozess wird wiederholt. 

![Diagramm der zwischengespeicherte Daten ungültig](../media-draft/cache-aside-invalidate.png)

## <a name="considerations-for-using-the-cache-aside-pattern"></a>Überlegungen zur Verwendung des cachefremden Musters

Überlegen Sie genau, welche Daten im Cache ablegen. Nicht alle Daten ist möglich, die zwischengespeichert werden.

- **Lebensdauer**: Cache-Aside wirksam sein kann, stellen sicher, dass die Ablaufrichtlinie die Access-Häufigkeit der Daten entspricht. Machen die zu kurzen Ablaufzeitraum fest können Ursache Anwendungen zum Abrufen von Daten aus den Daten kontinuierlich speichern und dem Cache hinzuzufügen.

- **Entfernen von**:-Caches verfügen über eine begrenzte Größe im Vergleich zum typischen Data Stores, und sie müssen Daten ggf. entfernen. Stellen Sie sicher, dass Sie eine entsprechende Entfernungsrichtlinie für Ihre Daten auswählen.

- **Vorbereiten**: damit das cachefremde Muster wirksam ist, werden viele Lösungen füllen den Cache mit Daten, die sie denken, dass der Zugriff auf häufig vorab.

- **Konsistenz**: Implementieren des Cache-Aside-Musters garantiert keine Konsistenz zwischen dem Datenspeicher und dem Cache. Daten in einem Datenspeicher können ohne Benachrichtigung des Caches geändert werden. Dies kann zu schwerwiegenden Synchronisierungsproblemen führen.

Das Cache-Aside-Muster ist nützlich, wenn Sie erforderlich, den Zugriff auf Daten häufig aus einer Datenquelle, die einen Datenträger verwendet. Verwenden das Cache-Aside-Muster, müssen Sie wichtige Daten in einen Cache für die Steigerung die Geschwindigkeit des abrufen speichern. 