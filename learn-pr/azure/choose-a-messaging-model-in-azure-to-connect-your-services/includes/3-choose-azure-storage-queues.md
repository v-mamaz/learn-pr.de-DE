Angenommen, Sie planen die Architektur einer Anwendung für den Austausch von Musik. Dabei möchten Sie sicherstellen, dass Musikdateien in die zuverlässige Web-API der mobilen App hochgeladen wird. Anschließend sollen die Details zu neuen Liedern der Musiker direkt an die App weitergegeben werden. In einem solchen Szenario eignet sich ein nachrichtenbasiertes System besonders gut. Azure bietet dafür zwei Lösungen:

- Azure Queue Storage
- Azure Service Bus

## <a name="what-is-azure-queue-storage"></a>Was ist Azure Queue Storage?
Bei Queue Storage handelt es sich um einen Dienst, der Azure Storage verwendet, um eine große Menge von Nachrichten zu speichern, auf die von überall auf der Welt über eine einfache REST-basierte Schnittstelle zugegriffen werden kann. Warteschlangen können Millionen von Nachrichten enthalten. Die Anzahl an gespeicherten Nachrichten wird nur durch das jeweilige zugewiesene Speicherkonto begrenzt.

## <a name="what-is-azure-service-bus"></a>Was ist Azure Service Bus?
Bei Azure Service Bus handelt es sich um ein Brokersystem für Nachrichten, das auf Unternehmensanwendungen ausgerichtet ist. Diese Apps verwenden häufig mehrere Kommunikationsprotokolle, verfügen über verschiedene Datenverträge, höhere Sicherheitsanforderungen und können sowohl lokale Dienste als auch Clouddienste umfassen. Service Bus unterstützt dedizierte Infrastrukturen für Nachrichten, die genau für solche Szenarios konzipiert sind.

Beide Dienste basieren auf der Idee einer „Warteschlange“, die solange mehrere gesendete Nachrichten enthält, bis der Empfänger bereit ist, diese zu empfangen. Wenn Sie noch nie mit einem Warteschlangensystem für Nachrichten gearbeitet haben, sollten Sie sich über deren zahlreichen Vorteile informieren. Diese werden im Folgenden erläutert.

## <a name="increased-reliability"></a>Erhöhte Zuverlässigkeit
Warteschlangen werden von verteilten Anwendungen als temporäre Speicherorte für Nachrichten verwendet, deren Zustellung an eine Zielkomponente noch aussteht. Die Quellkomponente kann eine Nachrichten zu der Warteschlange hinzufügen, und die Zielkomponenten können die Nachrichten vorne in der Warteschlange abrufen, um diese zu verarbeiten. Warteschlangen erhöhen die Zuverlässigkeit des Nachrichtenaustauschs, da in Zeiten hoher Nachfrage Nachrichten einfach warten können, bis eine Zielkomponente bereit ist, diese zu verarbeiten.

## <a name="message-delivery-guarantees"></a>Übermittlungsgarantien für Nachrichten
Warteschlangensysteme garantieren in der Regel die Zustellung jeder Nachricht in der Warteschlange an eine Zielkomponente. Allerdings können dabei unterschiedliche Ansätze verfolgt werden:

- **At-Least-Once-Übermittlung** Bei diesem Ansatz wird jede Nachricht an mindestens eine der Komponenten übermittelt, die Nachrichten aus der Warteschlange abrufen. Unter Umständen ist es jedoch möglich, dass dieselbe Nachricht mehrfach übermittelt wird. Wenn beispielsweise zwei Instanzen einer Webanwendung Nachrichten aus einer Warteschlange abrufen, geht jede Nachricht in der Regel nur an eine dieser Instanzen. Wenn eine Instanz jedoch lange zum Verarbeiten der Nachrichten braucht, und ein Timeout abläuft, wird die Nachricht ggf. an die andere Instanz gesendet. Behalten Sie diese Möglichkeit im Hinterkopf, wenn Sie Ihren Web-App-Code entwickeln.

- **At-Most-Once-Zustellung.** Bei diesem Ansatz wird nicht garantiert, dass jede Nachricht übermittelt wird. Es besteht daher die sehr geringe Wahrscheinlichkeit, dass eine Nachricht nicht ankommt. Allerdings kann es anders als bei der „At-Least-Once-Übermittlung“ nicht vorkommen, dass Nachrichten mehrmals übermittelt werden. Dies wird teilweise auch als „automatische Duplikaterkennung“ bezeichnet.

- **First In, First Out (FIFO).** In den meisten Messaging-Systemen verlassen Nachrichten die Warteschlange in der Regel in der Reihenfolge, in der sie hinzugefügt wurden. Allerdings sollten Sie überprüfen, ob diese Reihenfolge eingehalten wird. Wenn Ihre verteilte Anwendung verlangt, dass Nachrichten genau in der richtigen Reihenfolge verarbeitet werden, müssen Sie ein Warteschlangensystem mit FIFO-Garantie verwenden.

## <a name="transactional-support"></a>Transaktionsunterstützung
Einige eng verwandte Nachrichtengruppen können Probleme verursachen, wenn die Übermittlung einer Nachricht in der Gruppe fehlschlägt.

Nehmen Sie als Beispiel eine E-Commerce-Anwendung. Wenn der Benutzer auf die Schaltfläche **Kaufen** klickt, werden möglicherweise mehrere Nachrichten generiert und an verschiedene Ziele zur Verarbeitung gesendet:

- Eine Nachricht mit den Details zur Bestellung wird an das Versandzentrum gesendet.
- Ein Nachricht mit den Details zur Gesamtsumme und der Bezahlung wird an einen Dienst zur Verarbeitung von Kreditkarteninformationen gesendet. 
- Eine Nachricht mit den Rechnungsinformationen wird an eine Datenbank gesendet, damit eine Rechnung für den Kunden generiert werden kann.

In diesem Fall soll sichergestellt werden, dass entweder _alle_ Nachrichten oder keine verarbeitet werden. Ihre Anwendung wird wahrscheinlich nicht lange verwendet, wenn die Nachricht zu den Kreditkarteninformationen nicht zugestellt wird und alle Bestellungen zwar versandt, aber nicht bezahlt werden. Solche Probleme können Sie vermeiden, indem Sie die beiden Nachrichten in einer Transaktion zusammenfassen. Nachrichtentransaktionen sind genauso wie bei Datenbanken immer als einzelne Einheit erfolgreich oder schlagen alle gemeinsam fehl. Wenn die Übermittlung der Kreditkartendaten fehlschlägt, gilt dasselbe für die Nachricht mit den Details zur Bestellung.

## <a name="which-service-should-i-choose"></a>Welcher Dienst eignet sich für mich?
Ihnen sollte klar sein, dass die Kommunikationsstrategie für diese Art von Architektur auf Nachrichten aufbauen sollte. Wenn dem so ist, können Sie entscheiden, ob Sie Azure Storage Queues oder Azure Service Bus verwenden möchten. Beide Dienste können verwendet werden, um Nachrichten zu speichern und an Ihre Komponenten zuzustellen. Beide weisen geringfügig unterschiedliche Funktionsmerkmale auf. Das heißt, Sie können sich für einen entscheiden oder beide verwenden. Welche Sie auswählen, hängt von dem zu lösenden Problem ab.

#### <a name="choose-service-bus-queues-if"></a>Verwenden Sie Service Bus-Warteschlangen, wenn Folgendes zutrifft:
- Sie benötigen eine At-Most-Once-Zustellungsgarantie.
- Sie benötigen eine FIFO-Garantie.
- Sie müssen Nachrichten in Transaktionen gruppieren.
- Sie möchten Nachrichten empfangen, ohne die Warteschlange abzufragen.
- Sie müssen ein rollenbasiertes Zugriffsmodell für die Warteschlange bereitstellen.
- Sie müssen Nachrichten mit einer Größe von 64 bis 256 KB verarbeiten.
- Die Warteschlangengröße liegt unter 80 GB.
- Sie möchten in der Lage sein, Nachrichtenbatches zu veröffentlichen und zu verarbeiten.

Queue Storage verfügt über weniger Features. Wenn dies aber für Ihre Anforderungen ausreichend, ist es deutlich einfacher für Sie, wenn Sie diesen Dienst wählen. Außerdem stellt er die bessere Lösung dar, wenn Ihre App die folgenden Anforderungen stellt:

#### <a name="choose-queue-storage-if"></a>Verwenden Sie Queue Storage, wenn Folgendes zutrifft:
- Sie benötigen serverseitige Protokolle aller Nachrichten, die die Warteschlange passieren.
- Sie gehen davon aus, dass die Größe der Warteschlange 80 GB überschreitet.
- Sie möchten den Verarbeitungsfortschritt einer Nachricht von der Anwendung innerhalb der Warteschlange nachverfolgen lassen.

## <a name="summary"></a>Zusammenfassung

Eine Warteschlange ist ein einfacher temporärer Speicherort für Nachrichten, die zwischen Komponenten einer verteilten Anwendung gesendet werden. Mit Warteschlangen können Sie Nachrichten organisieren und unvorhersehbare Nachfragespitzen bewältigen.

Verwenden Sie Azure Storage-Warteschlangen, wenn Sie ein einfaches und leicht zu codierendes Warteschlangensystem wünschen. Nutzen Sie für anspruchsvollere Anforderungen Service Bus-Warteschlangen.