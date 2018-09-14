Ihre Website ist nun online und wird in Azure gehostet. Wie kann aber sichergestellt werden, dass Ihre Website ununterbrochen verfügbar ist?

Und was geschieht beispielsweise, wenn Sie wöchentliche Wartungsarbeiten durchführen müssen? Innerhalb des Wartungsfensters ist Ihr Dienst nicht verfügbar. Da Ihre Website von Benutzern auf der ganzen Welt genutzt wird, gibt es keinen idealen Wartungszeitraum. Falls zu viele Benutzer gleichzeitig eine Verbindung mit Ihrer Website herstellen, kann es außerdem zu Leistungsproblemen kommen.

## <a name="what-are-availability-and-high-availability"></a>Was sind Verfügbarkeit und Hochverfügbarkeit?

Unter _Verfügbarkeit_ wird der Zeitraum verstanden, in dem ein Dienst ohne Unterbrechung ausgeführt werden kann. Unter _Hochverfügbarkeit_ (oder als Adjektiv _hochverfügbar_) wird ein langer Zeitraum verstanden, in dem ein Dienst ohne Unterbrechung ausgeführt werden kann.

Gute Beispiele sind Plattformen für soziale Medien oder bestimmte Nachrichtenseiten, die Sie vermutlich jeden Tag nutzen. Können Sie jederzeit auf diese Websites zugreifen oder werden häufig Fehlermeldungen wie „503 Service Unavailable“ (503 – Dienst nicht verfügbar) angezeigt? Wenn Informationen nicht zugänglich sind, ist das frustrierend, wie Sie sicherlich selbst wissen.

Haben vielleicht Sie Begriffe wie "5 Neunen Verfügbarkeit." gehört. Dieser bezieht sich auf einen Dienst, für den eine Verfügbarkeit von 99,999 % garantiert wird. Dieser Zustand wird von vielen Teams angestrebt, da eine Verfügbarkeit von 100 % nur schwer gewährleistet werden kann.

## <a name="what-is-resiliency"></a>Was ist Resilienz?

Unter _Resilienz_ wird die Fähigkeit eines Systems verstanden, auch bei anormalen Bedingungen weiterhin einsatzfähig zu sein.

Zu diesen Bedingungen zählen

- Naturkatastrophen in Kraft tritt.
- Systemwartung, geplante und ungeplante, einschließlich Softwareupdates und Sicherheitspatches.
- Spitzen im Datenverkehr auf Ihrer Website.
- Bedrohungen, die von böswilligen Parteien vorgenommen werden, wie z. B. verteilte Denial--Diensts oder DDoS, Angriffe.

Angenommen Sie, Ihr marketing-Team möchte, dass einen flash Verkauf um eine Reihe von neuen Produkten höher zu stufen. Für den geplanten Zeitraum rechnen Sie mit Lastspitzen. Diese könnten Ihr Verarbeitungssystem überfordern und dessen Leistung einschränken oder sogar zu einem Ausfall führen, was zu Enttäuschung auf Benutzerseite führen würde. Vielleicht haben Sie schon einmal eine ähnliche Erfahrung gemacht, Wollten Sie schon einmal Tickets für ein Ereignis aus, um dann festzustellen, dass die Website reagiert, wurde nicht?

## <a name="what-is-a-load-balancer"></a>Was ist ein Lastenausgleich?

Ein _Lastenausgleich_ verteilt den Datenverkehr gleichmäßig auf die einzelnen Systeme in einem Pool. Dadurch können Sie leichter Hochverfügbarkeit und Resilienz gewährleisten.

Angenommen, Sie fügen allen Schichten jeweils gleich konfigurierte virtuelle Computer hinzu. Die Idee ist zusätzliche Systeme bereit, falls eine ausfällt oder zu viele Benutzer gleichzeitig bereitstellt.

Problematisch ist hier, dass jeder virtueller Computer über eine eigene IP-Adresse verfügt. Außerdem besteht keine Möglichkeit, den Datenverkehr zu verteilen, falls ein System ausfällt oder ausgelastet ist. Es stellt sich daher die Frage, wie die virtuellen Computer so verbunden werden, dass Benutzer den Eindruck haben, mit nur einem System zu interagieren.

Die Lösung besteht im Einsatz eines Lastenausgleichs, der den Datenverkehr verteilt. Der Lastenausgleich wird für die Benutzer zum Einstiegspunkt. Diese wissen nicht (und müssen auch nicht wissen), welches System vom Lastenausgleich dazu bestimmt wird, die Anforderung entgegenzunehmen.

Die folgende Abbildung zeigt die Rolle von einem Load Balancer.

![Eine Abbildung, zeigt die Webebene, einer drei-Ebenen-Architektur. Die Webebene verfügt über mehrere virtuelle Computer auf Anfragen von Benutzern. Es gibt ein Load Balancer, der benutzeranforderungen für die virtuellen Computer verteilt.](../media/3-load-balancer.png)

Wie Sie sehen, empfängt der Lastenausgleich die Benutzeranforderung. Anschließend wird diese an einen der virtuellen Computer in der Webschicht weitergeleitet. Wenn der virtuelle Computer nicht verfügbar ist oder nicht mehr reagiert, leitet der Lastenausgleich keinen Datenverkehr mehr an diesen weiter. Stattdessen wird der Datenverkehr an einen der antwortenden Server weitergeleitet.

Mit einem Lastenausgleich können Sie Wartungsaufgaben ausführen, ohne den Dienst zu unterbrechen. Sie haben beispielsweise die Möglichkeit, das Wartungsfenster für jeden virtuellen Computer so festzulegen, dass keine Überschneidungen auftreten. Während des Wartungsfensters erkennt der Load Balancer an, dass der virtuelle Computer nicht mehr reagiert, und leitet den Datenverkehr an andere virtuelle Computer im Pool.

Sie können auch der Logik- und Datenschicht Ihrer E-Commerce-Website einen Lastenausgleich hinzufügen. Ob diese Entscheidung sinnvoll ist, hängt von den Anforderungen Ihres Diensts ab.

## <a name="what-is-azure-load-balancer"></a>Was ist Azure Load Balancer?

Azure Load Balancer ist ein Lastenausgleichsdienst, der von Microsoft bereitgestellt wird.

Sie können Lastenausgleichssoftware zwar durchaus manuell in einem virtuellen Computer konfigurieren. Der Nachteil besteht jedoch darin, dass Sie dann über ein weiteres System verfügen, das Sie verwalten müssen. Wenn der Lastenausgleich ausfällt oder routinemäßige Wartungsaufgaben erforderlich sind, stehen Sie wieder vor dem ursprünglichen Problem.

Stattdessen können Sie Azure Load Balancer, da keine Infrastruktur oder Software für Sie verwalten. Azure übernimmt der Wartung für Sie.

Die folgende Abbildung zeigt die Rolle des Azure Load balancer in einer Architektur mit mehreren Ebenen.

![Eine Abbildung, zeigt die Webebene, einer drei-Ebenen-Architektur. Die Webebene verfügt über mehrere virtuelle Computer auf Anfragen von Benutzern. Es gibt ein Load Balancer, der benutzeranforderungen für die virtuellen Computer verteilt.](../media/3-azure-load-balancer.png)

## <a name="what-about-dns"></a>Wie sieht es mit dem Einsatz von DNS aus?

Mit DNS (Domain Name System) können Sie Anzeigenamen den zugehörigen IP-Adressen zuordnen. Sie können DNS als das Telefonbuch des Internets vorstellen.

Ein Domänenname wie contoso.com könnte beispielsweise der IP-Adresse 40.65.106.192 des Lastenausgleichs in der Webschicht zugeordnet werden.

Sie können entweder Ihren DNS-Server oder Azure DNS, ein Hostingdienst für DNS-Domänen innerhalb der Azure-Infrastruktur, verwenden.

Die folgende Abbildung zeigt die Azure DNS. Wenn der Benutzer contoso.com aufruft, leitet Azure DNS den Datenverkehr an den Lastenausgleich weiter.

![Eine Abbildung, zeigt Azure Domain Name System vor einem Load Balancer positioniert.](../media/3-dns.png)

## <a name="summary"></a>Zusammenfassung

Mit dem eingerichteten Lastenausgleich haben Sie die Hochverfügbarkeit und Resilienz Ihrer E-Commerce-Website erhöht. Wenn Sie nun Wartungsarbeiten durchführen oder Lastspitzen auftreten, kann der Lastenausgleich den Datenverkehr an ein anderes verfügbares System weiterleiten.

Auch wenn Sie Ihr eigenes Lastenausgleichsmodul auf einem virtuellen Computer konfigurieren können, verringert Azure Load Balancer Instandhaltung, da keine Infrastruktur Software oder zu verwalten.

Mit DNS werden Anzeigenamen den zugehörigen IP-Adressen zugeordnet. Domain Name System ist daher mit einem Telefonbuch vergleichbar, in dem die Namen von Personen oder Unternehmen Telefonnummern zugeordnet werden. Sie können Ihren eigenen DNS-Server, oder verwenden Sie Azure DNS.
