Ihre Website ist nun online und wird in Azure gehostet. Wie kann aber sichergestellt werden, dass Ihre Website ununterbrochen verfügbar ist?

Und was geschieht beispielsweise, wenn Sie wöchentliche Wartungsarbeiten durchführen müssen? Innerhalb des Wartungsfensters ist Ihr Dienst nicht verfügbar. Da Ihre Website von Benutzern auf der ganzen Welt genutzt wird, gibt es keinen idealen Wartungszeitraum. Falls zu viele Benutzer gleichzeitig eine Verbindung mit Ihrer Website herstellen, kann es außerdem zu Leistungsproblemen kommen.

## <a name="what-are-availability-and-high-availability"></a>Was sind Verfügbarkeit und Hochverfügbarkeit?

Unter _Verfügbarkeit_ wird der Zeitraum verstanden, in dem ein Dienst ohne Unterbrechung ausgeführt werden kann. Unter _Hochverfügbarkeit_ (oder als Adjektiv _hochverfügbar_) wird ein langer Zeitraum verstanden, in dem ein Dienst ohne Unterbrechung ausgeführt werden kann.

Gute Beispiele sind Plattformen für soziale Medien oder bestimmte Nachrichtenseiten, die Sie vermutlich jeden Tag nutzen. Können Sie jederzeit auf diese Websites zugreifen oder werden häufig Fehlermeldungen wie „503 Service Unavailable“ (503 – Dienst nicht verfügbar) angezeigt? Wenn Informationen nicht zugänglich sind, ist das frustrierend, wie Sie sicherlich selbst wissen.

Möglicherweise haben Sie schon einmal den englischen Ausdruck „Five Nines Availability“ gehört. Dieser bezieht sich auf einen Dienst, für den eine Verfügbarkeit von 99,999 % garantiert wird. Dieser Zustand wird von vielen Teams angestrebt, da eine Verfügbarkeit von 100 % nur schwer gewährleistet werden kann.

## <a name="what-is-resiliency"></a>Was ist Resilienz?

Unter _Resilienz_ wird die Fähigkeit eines Systems verstanden, auch bei anormalen Bedingungen weiterhin einsatzfähig zu sein.

Zu diesen Bedingungen zählen

- Naturkatastrophen,
- geplante und ungeplante Systemwartungen, bei denen Software- oder Sicherheitspatches durchgeführt werden,
- Lastspitzen beim Website-Datenverkehr
- und von Angreifern ausgehende Bedrohungen wie verteilte Denial-of-Service-Angriffe (DDoS).

Angenommen, Ihr Marketingteam möchte einen Blitzverkauf organisieren, um eine neue Produktlinie zu bewerben. Für den geplanten Zeitraum rechnen Sie mit Lastspitzen. Diese könnten Ihr Verarbeitungssystem überfordern und dessen Leistung einschränken oder sogar zu einem Ausfall führen, was zu Enttäuschung auf Benutzerseite führen würde. Vielleicht haben Sie schon einmal eine ähnliche Erfahrung gemacht, als Sie Tickets für ein Event kaufen wollten und die Website nicht erreichbar war.

## <a name="what-is-a-load-balancer"></a>Was ist ein Lastenausgleich?

Ein _Lastenausgleich_ verteilt den Datenverkehr gleichmäßig auf die einzelnen Systeme in einem Pool. Dadurch können Sie leichter Hochverfügbarkeit und Resilienz gewährleisten.

Angenommen, Sie fügen allen Schichten jeweils gleich konfigurierte virtuelle Computer hinzu. Die Idee besteht darin, über zusätzliche Systeme zu verfügen, falls eines ausfällt oder zu viele Benutzeranforderungen gleichzeitig verarbeitet werden müssen.

Problematisch ist hier, dass jeder virtueller Computer über eine eigene IP-Adresse verfügt. Außerdem besteht keine Möglichkeit, den Datenverkehr zu verteilen, falls ein System ausfällt oder ausgelastet ist. Es stellt sich daher die Frage, wie die virtuellen Computer so verbunden werden, dass Benutzer den Eindruck haben, mit nur einem System zu interagieren.

Die Lösung besteht im Einsatz eines Lastenausgleichs, der den Datenverkehr verteilt. Der Lastenausgleich wird für die Benutzer zum Einstiegspunkt. Diese wissen nicht (und müssen auch nicht wissen), welches System vom Lastenausgleich dazu bestimmt wird, die Anforderung entgegenzunehmen.

Nachfolgend sehen Sie ein Diagramm.

![Lastenausgleich zum Verteilen von Datenverkehr zwischen virtuellen Computern](../media-draft/load-balancer.png)

Wie Sie sehen, empfängt der Lastenausgleich die Benutzeranforderung. Anschließend wird diese an einen der virtuellen Computer in der Webschicht weitergeleitet. Wenn der virtuelle Computer nicht verfügbar ist oder nicht mehr reagiert, leitet der Lastenausgleich keinen Datenverkehr mehr an diesen weiter. Stattdessen wird der Datenverkehr an einen der antwortenden Server weitergeleitet.

Mit einem Lastenausgleich können Sie Wartungsaufgaben ausführen, ohne den Dienst zu unterbrechen. Sie haben beispielsweise die Möglichkeit, das Wartungsfenster für jeden virtuellen Computer so festzulegen, dass keine Überschneidungen auftreten. Innerhalb des Wartungsfensters erkennt der Lastenausgleich, dass der virtuelle Computer nicht reagiert, und leitet den Datenverkehr an die anderen virtuellen Computer im Pool weiter.

Sie können auch der Logik- und Datenschicht Ihrer E-Commerce-Website einen Lastenausgleich hinzufügen. Ob diese Entscheidung sinnvoll ist, hängt von den Anforderungen Ihres Diensts ab.

## <a name="what-is-azure-load-balancer"></a>Was ist Azure Load Balancer?

Azure Load Balancer ist ein Lastenausgleichsdienst, der von Microsoft bereitgestellt wird.

Sie können Lastenausgleichssoftware zwar durchaus manuell in einem virtuellen Computer konfigurieren. Der Nachteil besteht jedoch darin, dass Sie dann über ein weiteres System verfügen, das Sie verwalten müssen. Wenn der Lastenausgleich ausfällt oder routinemäßige Wartungsaufgaben erforderlich sind, stehen Sie wieder vor dem ursprünglichen Problem.

Azure Load Balancer bietet eine Lösung für diese Herausforderung, da Sie bei der Nutzung dieses Diensts keine Infrastruktur oder Software verwalten müssen. Diese Aufgabe wird Ihnen von Azure abgenommen.

Im folgenden Diagramm sehen Sie, dass allen Schichten jeweils mehrere virtuelle Computer zugeordnet sind. Jede Schicht enthält eine Azure Load Balancer-Instanz, die den Datenverkehr auf die virtuellen Computer im Pool aufteilt.

![Lastenausgleich für die Verteilung von Datenverkehr auf unterschiedliche virtuelle Computer mithilfe von Azure Load Balancer](../media-draft/azure-load-balancer.png)

## <a name="what-about-dns"></a>Wie sieht es mit dem Einsatz von DNS aus?

Mit DNS (Domain Name System) können Sie Anzeigenamen den zugehörigen IP-Adressen zuordnen. DNS lässt sich mit einem Telefonbuch für das Internet vergleichen.

Ein Domänenname wie contoso.com könnte beispielsweise der IP-Adresse 40.65.106.192 des Lastenausgleichs in der Webschicht zugeordnet werden.

Sie können entweder Ihren DNS-Server oder Azure DNS, ein Hostingdienst für DNS-Domänen innerhalb der Azure-Infrastruktur, verwenden.

Mit dem folgenden Diagramm erhalten Sie einen Überblick über Azure DNS. Wenn der Benutzer contoso.com aufruft, leitet Azure DNS den Datenverkehr an den Lastenausgleich weiter.

![Verwenden von Azure DNS zum Zuweisen eines DNS-Namens](../media-draft/dns.png)

## <a name="summary"></a>Zusammenfassung

Mit dem eingerichteten Lastenausgleich haben Sie die Hochverfügbarkeit und Resilienz Ihrer E-Commerce-Website erhöht. Wenn Sie nun Wartungsarbeiten durchführen oder Lastspitzen auftreten, kann der Lastenausgleich den Datenverkehr an ein anderes verfügbares System weiterleiten.

Sie können zwar einen eigenen Lastenausgleich in einem virtuellen Computer konfigurieren. Der Einsatz von **Azure Load Balancer** bietet jedoch den Vorteil, dass sich der Unterhaltungsaufwand verringert, da Sie keine Infrastruktur und Software warten müssen.

Mit DNS werden Anzeigenamen den zugehörigen IP-Adressen zugeordnet. Domain Name System ist daher mit einem Telefonbuch vergleichbar, in dem die Namen von Personen oder Unternehmen Telefonnummern zugeordnet werden. Sie können entweder Ihren eigenen DNS-Server oder Azure DNS verwenden.
