Die Cloud wurde geändert, wie Organisationen zu lösen, die geschäftsanforderungen des Kunden, und wie Anwendungen und Systeme entwickelt wurden. Die Rolle als Solution Architect ist nicht nur auf die wertschöpfung durch den funktionalen Anforderungen der Anwendung, sondern auch um sicherzustellen, dass die Lösung in Möglichkeiten entworfen wurde, die skalierbare, belastbare, effizient und sicher sind. Architektur der Lösung ist mit der Planung, Entwurf, Implementierung und fortlaufende Verbesserung von einem System mit Technologie befasst. Die Architektur eines Systems muss die geschäftlichen Anforderungen mit den technischen Funktionen in Einklang bringen, die zur Erfüllung dieser Anforderungen erforderlich sind. Dazu gehört die Bewertung von Risiken, Kosten und Funktionen für das gesamte System und dessen Komponenten.

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yEv2]

Es gibt zwar keine allgemeingültige Herangehensweise für das Entwerfen einer Architektur, gibt es einige universelle Konzepte, die unabhängig von der Architektur, Technologien oder Cloud-Anbieter angewendet werden. Während diese nicht pauschel eingerechnet sind, helfen zu diesen Konzepten konzentrieren erstellen Sie eine zuverlässige, sichere und flexible Grundlage für Ihre Anwendung Ihnen.

Eine gute Architektur baut auf einem soliden Fundament mit vier Säulen auf:

* Sicherheit
* Leistung und Skalierbarkeit
* Verfügbarkeit und Zuverlässigkeit
* Effizienz und Vorgänge

![Säulen einer guten Architektur](../media-draft/pillars.png)

## <a name="security"></a>Sicherheit

Daten in verschiedenen Formen ist der Teil der wichtigsten technischen Speicherbedarf Ihrer Organisation. Bei dieser Säule stehen der Schutz des Zugriffs auf Ihre Architektur mittels Authentifizierung sowie der Schutz Ihrer Anwendung und Ihrer Daten vor Netzwerksicherheitslücken im Mittelpunkt. Darüber hinaus muss die Integrität Ihrer Daten geschützt werden – etwa durch Verschlüsselung.

Sie müssen über die Sicherheit im gesamten Lebenszyklus Ihrer Anwendung, von Entwurf und Implementierung zu Bereitstellung und Betrieb vorstellen. Sie benötigen zur Sicherheit in Ihrer Anwendung, die Prozesse und die Unternehmenskultur, aber die Cloud bietet Schutz vor einer Vielzahl von Bedrohungen, z.B. Netzwerkangriffe und DDoS-Angriffe.

![Arten von Angriffen](../media-draft/security.png)

## <a name="performance-and-scalability"></a>Leistung und Skalierbarkeit

Eine gut funktionierende und skalierbare Architektur muss die Ressourcenkapazität ordnungsgemäß auf die Nachfrage abstimmen. Hierzu skalieren Cloudarchitekturen Anwendungen in der Regel dynamisch auf der Grundlage der Aktivitäten in der Anwendung. Die Nachfrage für Dienste ändert sich. Daher ist es wichtig, dass auch Ihre Architektur an die Nachfrage angepasst werden kann. Wenn Sie die Leistung und Skalierbarkeit bei Ihrem Architekturentwurf berücksichtigen, können Sie eine großartige und kostengünstige Kundenerfahrung bieten.

![Grafik mit hohem Daten- oder Anforderungsaufkommen](../media-draft/performance-demand.png))

## <a name="availability-and-recoverability"></a>Verfügbarkeit und Zuverlässigkeit

Die größte Sorge eines Architekten ist es, dass die Architektur ausfällt und nicht wiederhergestellt werden kann. Das Design einer erfolgreichen Cloudumgebung ist daher auf mögliche Fehler auf sämtlichen Ebenen vorbereitet. Zur Antizipierung dieser Fehler muss das System unter anderem so entworfen werden, dass es im Falle eines Fehlers innerhalb der von Ihrer Organisation und Ihren Kunden erwarteten Zeit wiederhergestellt werden kann.

![Systemfehler](../media-draft/system-failure.png)

## <a name="efficiency-and-operations"></a>Effizienz und Vorgänge

Sie sollten Ihre Cloud-Umgebung so entwerfen, dass es kostengünstig ist, Betrieb und Entwicklung auf. Ineffizienz und unnötigen Aufwand in die Cloud Ausgaben sollten identifiziert werden um sicherzustellen, verbringen Sie Geld, in dem wir den größten Nutzen machen können. Sie müssen eine gute Architektur verfügen, damit Sie Fehler und Probleme erkennen können, bevor sie auftreten oder zumindest vor, beachten Sie, Ihre Kunden dass. Sie müssen auch etwaigen Überblick, wie Ihre Anwendung die verfügbaren Ressourcen über ein stabiles Framework für die Remoteüberwachung verwendet haben.

![Effizienz](../media-draft/efficiency.png)

## <a name="shared-responsibility"></a>Gemeinsame Verantwortung

In die Cloud verschieben, wird ein Modell für gemeinsame Verantwortung eingeführt. In diesem Modell wird Ihrem Cloudanbieter bestimmte Aspekte Ihrer Anwendung, verwalten, sodass Sie die verbleibenden Verantwortung. In einer lokalen Umgebung sind Sie für alles zuständig. Wie Sie mit Infrastruktur als Dienst (IaaS) verschieben, klicken Sie dann dauert Platform-as-a-Service (PaaS) und Software-as-a-Service (SaaS), Ihrem Cloudanbieter auf mehrere dieser Verantwortung. Diese gemeinsame Verantwortung wird bei architektonischen Entscheidungen, eine Rolle spielen, da sie Auswirkungen auf die Kosten, Funktionen, Sicherheit und die technischen Funktionen Ihrer Anwendung haben können. Sie können durch die Umstellung dieser Aufgaben an Ihren Anbieter konzentrieren, profitiert Ihr Unternehmen sind und Abkehr von Aktivitäten, die nicht von einer zentralen Geschäftsfunktion.

![Clouddienstmodelle](../media-draft/cloud-responsibility-model.png)

## <a name="design-choices"></a>Designentscheidungen

In einer idealen Architektur würden wir die sicherste, leistungsfähigste, hochverfügbarste und effizienteste Umgebung überhaupt erstellen. Wie so oft müssen wir jedoch gewisse Kompromisse eingehen. Eine Umgebung, die bei allen Säulen das Höchstmaß erreicht, hat ihren Preis. Das können tatsächliche Kosten sein oder beispielsweise eine höhere Bereitstellungsdauer oder Abstriche bei der betrieblichen Flexibilität. Jede Organisation hat andere Prioritäten, die sich auf die Designentscheidungen für die einzelnen Säulen auswirken. Wie Sie Ihre Architektur entworfen haben, müssen Sie bestimmen, welche vor-und Nachteile akzeptabel sind und welche nicht.

Bei der Erstellung einer Azure-Architektur müssen zahlreiche Aspekte berücksichtigt werden. Die Architektur soll sicher, skalierbar, verfügbar und wiederherstellbar sein. Um, die zu ermöglichen, müssen Sie Entscheidungen basierend auf Kosten, organisatorische Prioritäten und dem Risiko.