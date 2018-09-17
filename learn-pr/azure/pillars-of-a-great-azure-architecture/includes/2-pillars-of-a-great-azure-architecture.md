Die Cloud hat die Art und Weise verändert, wie Unternehmen ihre geschäftlichen Herausforderungen meistern und Anwendungen und Systeme konzipiert sind. Die Aufgabe eines Lösungsarchitekten besteht nicht nur darin, durch die funktionalen Anforderungen der Anwendung einen geschäftlichen Nutzen zu generieren, sondern auch darin, eine skalierbare, ausfallsichere, effiziente und sichere Lösung bereitzustellen. Bei einer IT-Lösungsarchitektur geht es um die Planung, den Entwurf, die Implementierung und die kontinuierliche Verbesserung eines Technologiesystems. Die Architektur eines Systems muss die geschäftlichen Anforderungen mit den technischen Funktionen in Einklang bringen, die zur Erfüllung dieser Anforderungen erforderlich sind. Dazu gehört die Bewertung von Risiken, Kosten und Funktionen für das gesamte System und dessen Komponenten.

Für das Architekturdesign gibt es zwar keine Standardlösung, es gibt jedoch einige universelle Konzepte, die unabhängig von Architektur, Technologie oder Cloudanbieter gelten. Obwohl nicht allumfassend, hilft Ihnen die Konzentration auf diese Konzepte, eine zuverlässige, sichere und flexible Grundlage für Ihre Anwendung zu schaffen.

Eine gute Architektur baut auf einem soliden Fundament mit vier Säulen auf:

* Sicherheit
* Leistung und Skalierbarkeit
* Verfügbarkeit und Zuverlässigkeit
* Effizienz und Vorgänge

![Säulen einer guten Architektur](../media-draft/pillars.png)

## <a name="security"></a>Sicherheit

Daten in unterschiedlichster Form sind das wertvollste technische Gut Ihrer Organisation. Bei dieser Säule stehen der Schutz des Zugriffs auf Ihre Architektur mittels Authentifizierung sowie der Schutz Ihrer Anwendung und Ihrer Daten vor Netzwerksicherheitslücken im Mittelpunkt. Darüber hinaus muss die Integrität Ihrer Daten geschützt werden – etwa durch Verschlüsselung.

Sie müssen die Sicherheit für den gesamten Lebenszyklus Ihrer Anwendung berücksichtigen – von Entwurf und Implementierung bis hin zu Bereitstellung und Betrieb. Die Cloud verfügt zwar über Schutzmaßnahmen für verschiedenste Bedrohungen (etwa Eindringversuche in das Netzwerk und DDoS-Angriffe), Sicherheit muss aber dennoch in Ihre Anwendungen, Prozesse und Unternehmenskultur integriert werden.

![Arten von Angriffen](../media-draft/security.png)

## <a name="performance-and-scalability"></a>Leistung und Skalierbarkeit

Eine gut funktionierende und skalierbare Architektur muss die Ressourcenkapazität ordnungsgemäß auf die Nachfrage abstimmen. Hierzu skalieren Cloudarchitekturen Anwendungen in der Regel dynamisch auf der Grundlage der Aktivitäten in der Anwendung. Die Nachfrage für Dienste ändert sich. Daher ist es wichtig, dass auch Ihre Architektur an die Nachfrage angepasst werden kann. Wenn Sie die Leistung und Skalierbarkeit bei Ihrem Architekturentwurf berücksichtigen, können Sie eine großartige und kostengünstige Kundenerfahrung bieten.

![Grafik mit hohem Daten- oder Anforderungsaufkommen](../media-draft/performance-demand.png))

## <a name="availability-and-recoverability"></a>Verfügbarkeit und Zuverlässigkeit

Die größte Sorge eines Architekten ist es, dass die Architektur ausfällt und nicht wiederhergestellt werden kann. Das Design einer erfolgreichen Cloudumgebung ist daher auf mögliche Fehler auf sämtlichen Ebenen vorbereitet. Zur Antizipierung dieser Fehler muss das System unter anderem so entworfen werden, dass es im Falle eines Fehlers innerhalb der von Ihrer Organisation und Ihren Kunden erwarteten Zeit wiederhergestellt werden kann.

![Systemfehler](../media-draft/system-failure.png)

## <a name="efficiency-and-operations"></a>Effizienz und Vorgänge

Ihre Cloudumgebung soll kostengünstig zu betreiben und entwicklerfreundlich sein. Ineffizienz und unnötige Cloudausgaben müssen erkannt werden, um sicherzustellen, dass Sie den größtmöglichen Nutzen aus Ihren Investitionen ziehen. Sie benötigen eine gute Überwachungsarchitektur, um Fehler und Probleme zu erkennen – idealerweise, noch bevor sie auftreten (oder wenigstens, bevor sie von Ihren Kunden bemerkt werden). Darüber hinaus benötigen Sie ein robustes Überwachungsframework, das Aufschluss über die Nutzung der verfügbaren Ressourcen durch Ihre Anwendung gibt.

![Effizienz](../media-draft/efficiency.png)

## <a name="shared-responsibility"></a>Gemeinsame Verantwortung

Die Umstellung auf die Cloud bringt ein Modell der gemeinsamen Verantwortung mit sich. In diesem Modell verwaltet Ihr Cloud-Anbieter bestimmte Aspekte Ihrer Anwendung und überlässt Ihnen die restliche Verantwortung. In einer lokalen Umgebung sind Sie für alles zuständig. Wenn Sie erst zu IaaS (Infrastructure-as-a-Service) und anschließend zu PaaS (Platform-as-a-Service) und SaaS (Software-as-a-Service) wechseln, übernimmt Ihr Cloudanbieter mehr von dieser Verantwortung. Diese gemeinsame Verantwortung spielt eine Rolle bei Ihren Architekturentscheidungen, da sie Auswirkungen auf Kosten, Betriebsfunktionen, Sicherheit und die technischen Möglichkeiten Ihrer Anwendung haben kann. Indem Sie diese Verantwortung auf Ihren Provider übertragen, können Sie sich darauf konzentrieren, einen Mehrwert für Ihr Unternehmen zu schaffen und sich aus Aktivitäten zurückzuziehen, die keine zentralen geschäftlichen Aufgaben darstellen.

![Clouddienstmodelle](../media-draft/cloud-responsibility-model.png)

## <a name="design-choices"></a>Designentscheidungen

In einer idealen Architektur würden wir die sicherste, leistungsfähigste, hochverfügbarste und effizienteste Umgebung überhaupt erstellen. Wie so oft müssen wir jedoch gewisse Kompromisse eingehen. Eine Umgebung, in der bei allen diesen Säulen das Höchstmaß erreicht wird, ist mit gewissen Kosten verbunden. Dabei kann es sich um Kosten in Form von Geld, aber auch um die Bereitstellungsdauer oder um betriebliche Flexibilität handeln. Jede Organisation hat andere Prioritäten, die sich auf die Designentscheidungen für die einzelnen Säulen auswirken. Beim Entwurf Ihrer Architektur müssen Sie entscheiden, welche Kompromisse akzeptabel sind und welche nicht.

Bei der Erstellung einer Azure-Architektur müssen zahlreiche Aspekte berücksichtigt werden. Die Architektur soll sicher, skalierbar, verfügbar und wiederherstellbar sein. Um das zu erreichen, müssen Sie Entscheidungen auf der Grundlage von Kosten, organisatorischen Prioritäten und Risiken treffen.