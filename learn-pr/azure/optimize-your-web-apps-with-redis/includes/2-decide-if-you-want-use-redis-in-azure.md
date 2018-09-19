Im Hintergrund Ihrer Sportwebseite befindet sich eine Datenbank, die abgefragte Daten zurückgibt. Allerdings verlangsamt sich die Leistung bei hoher Auslastung – insbesondere bei großen Sportereignissen. In gehosteten Umgebungen führt ein erhöhter Ressourcenverbrauch zu höheren Kosten. Das Zwischenspeichern von Daten im Cache stellt sicher, dass Ihre Website eine gute Leistung wirtschaftlich liefert.

## <a name="what-is-caching"></a>Was ist Zwischenspeichern?

Beim Zwischenspeichern werden häufig abgerufene Daten in einem Arbeitsspeicher gespeichert, der sich sehr nah an der Anwendung befindet, die die Daten nutzt. Zwischenspeichern wird verwendet, um die Leistung zu erhöhen und die Auslastung Ihrer Server zu verringern. Wir verwenden Redis, um einen In-Memory-Cache zu erstellen, der eine ausgezeichnete Wartezeit bietet und die Leistung potenziell verbessern kann.

## <a name="what-is-a-redis-cache"></a>Was ist eine Redis Cache-Instanz?

Redis (**RE**mote **DI**ctionary **S**erver) Cache ist ein Open-Source-basierter In-Memory-Speicher für Schlüssel-Wert-Paare. Redis ist aufgrund seiner Schnelligkeit beliebt und kann gängige Datentypen wie Zeichenfolgen, Hashes und Datasets speichern und bearbeiten. Zudem gilt Redis als entwicklerfreundlich, da zahlreiche Sprachen wie Python, C, C++, C#, Java und JavaScript unterstützt werden.

## <a name="what-is-azure-redis-cache"></a>Was ist Azure Redis Cache?

Microsoft Azure Redis Cache basiert auf dem beliebten Open-Source-Redis Cache. Sie erhalten Zugriff auf einen sicheren dedizierten Redis Cache, der von Microsoft verwaltet wird. Ein mit Azure Redis Cache erstellter Cache ist für beliebige Anwendungen in Microsoft Azure erreichbar. Azure Redis Cache wird in der Regel zum Verbessern der Leistung von Systemen verwendet, die stark von Back-End-Datenspeichern abhängig sind.

Ihre zwischengespeicherten Daten befinden sich im Arbeitsspeicher eines Azure-Servers, auf dem der Redis Cache betrieben wird, anstatt dass eine Datenbank sie vom Datenträger lädt. Der Cache ist zudem äußerst skalierbar. Größe und Tarif können jederzeit geändert werden.

## <a name="what-type-of-data-can-be-stored-in-the-cache"></a>Welche Arten von Daten können im Cache gespeichert werden?

Redis unterstützt eine Vielzahl von Datentypen rund um _sichere Binärzeichenfolgen_. Als Wert kann also jede beliebige binäre Sequenz verwendet werden – von „ich-liebe-kuchen“ bis hin zum Inhalt einer Bilddatei. Auch eine leere Zeichenfolge ist zulässig.

- Sichere Binärzeichenfolgen (am gängigsten)
- Zeichenfolgenlisten
- Unsortierte Zeichenfolgensätze
- Hashes
- Sortierte Zeichenfolgensätze
- Zeichenfolgenzuordnungen

Jeder Datenwert wird einem _Schlüssel_ zugeordnet, der verwendet werden kann, um den Wert im Cache nachzuschlagen. Redis funktioniert am besten mit kleineren Werten (bis 100 KB). Es empfiehlt sich daher, größere Daten auf mehrere Schlüssel aufzuteilen. Größere Werte (bis zu 500 MB) können zwar gespeichert werden, dies führt jedoch zu einer höheren Netzwerklatenz und kann Probleme aufgrund von unzureichendem Arbeitsspeicher verursachen, wenn für den Cache kein Ablauf alter Werte konfiguriert ist.

## <a name="what-is-a-redis-key"></a>Was ist ein Redis-Schlüssel?
Bei Redis-Schlüsseln handelt es sich ebenfalls um sichere Binärzeichenfolgen. Im Anschluss folgen einige Richtlinien für die Schlüsselwahl:

- Vermeiden Sie lange Schlüssel. Sie beanspruchen mehr Arbeitsspeicher und verlängern die Nachschlagedauer, da sie Byte für Byte verglichen werden müssen. Wenn Sie ein binäres Blob als Schlüssel verwenden möchten, generieren Sie einen eindeutigen Hash, und verwenden Sie stattdessen diesen als Schlüssel. Ein Schlüssel darf zwar bis zu 512 MB groß sein, Sie sollten aber _niemals_ einen Schlüssel dieser Größe verwenden.
- Verwenden Sie aussagekräftige Schlüssel für die Daten. „sport:fussball;datum:2008-02-02“ ist beispielsweise besser als „fb:8-2-2“. Die erste Variante ist besser lesbar, und die zusätzliche Größe ist zu vernachlässigen. Bemühen Sie sich um ein ausgewogenes Verhältnis zwischen Größe und Lesbarkeit.
- Verwenden Sie eine Konvention. Bewährt hat sich beispielsweise „Objekt:ID“ (wie in „sport:fussball“). 

## <a name="how-is-data-stored-in-a-redis-cache"></a>Wie werden Daten in Redis Cache gespeichert?

Daten in Redis befinden sich in _**Knoten**_ und _**Clustern**_.

**Knoten** sind ein Speicherplatz in Redis, in denen Ihre Daten gespeichert werden.

**Cluster** sind Gruppen von mindestens drei Knoten, auf die Ihr Dataset aufgeteilt ist. Cluster sind nützlich, da Ihre Vorgänge nicht unterbrochen werden, wenn ein Knoten ausfällt oder nicht mit dem Rest des Clusters kommunizieren kann.

## <a name="what-are-redis-caching-architectures"></a>Was sind Redis Cache-Architekturen?

Die Redis Cache-Architektur bestimmt, wie wir unsere Daten im Cache verteilen. Redis verteilt Daten allgemein auf drei Arten:

1. **Einzelner Knoten**
1. **Mehrere Knoten**
1. **Cluster**

Für Redis Cache-Architekturen gibt es in Azure verschiedene Tarife:

### <a name="basic-cache"></a>Cachetarif „Basic“

Dieser Cache bietet Ihnen einen Redis Cache mit _**einzelnem Knoten**_. Das vollständige Dataset wird in einem einzelnen Knoten gespeichert. Dieser Tarif eignet sich ideal für Entwicklungs- und Testzwecke sowie für nicht kritische Workloads.

### <a name="standard-cache"></a>Cachetarif „Standard“

Der Standard-Cache bietet Architekturen mit _**mehreren Knoten**_. Redis repliziert einen Cache in einer Primär-/Sekundärkonfiguration mit zwei Knoten. Azure verwaltet die Replikation zwischen den beiden Knoten. Dies ist ein produktionsbereiter Cache mit Replikation zwischen übergeordnetem und untergeordnetem Server.

### <a name="premium-tier"></a>Premium-Tarif

Der Premium-Tarif bietet die Leistungsmerkmale des Standardtarifs, ermöglicht aber auch das dauerhafte Speichern von Daten, das Erstellen von Momentaufnahmen und das Sichern von Daten. In diesem Tarif können Sie einen Redis-Cluster erstellen, der Daten auf mehrere Redis-Knoten verteilt, um den verfügbaren Arbeitsspeicher zu vergrößern. Der Premium-Tarif unterstützt auch ein Azure Virtual Network, um Ihnen die vollständige Kontrolle über Ihre Verbindungen, Subnetze, IP-Adressen und die Netzwerkisolation zu geben. Dieser Tarif bietet auch die Georeplikation, sodass Sie sicher sein können, dass sich Ihre Daten in der Nähe der App befinden, die sie benötigt.

## <a name="summary"></a>Zusammenfassung

Eine Datenbank ist ideal für die Speicherung großer Datenmengen, aber es gibt beim Nachschlagen von Daten eine inhärente Wartezeit. Sie senden eine Abfrage. Der Server interpretiert die Abfrage, schlägt die Daten nach und gibt sie zurück. Server weisen auch Kapazitätsbeschränkungen für die Bearbeitung von Anforderungen auf. Wenn zu viele Anforderungen gestellt werden, verlangsamt sich wahrscheinlich der Datenabruf. Beim Zwischenspeichern werden häufig angeforderte Daten im Arbeitsspeicher gehalten, die schneller zurückgegeben werden können als bei Abfrage einer Datenbank, was die Wartezeit verkürzen und die Leistung erhöhen sollte. Azure Redis Cache bietet Zugriff auf einen sicheren, dedizierten und skalierbaren Redis Cache, der in Azure gehostet und von Microsoft verwaltet wird.
