Ihre Organisation aus dem Gesundheitswesen speichert persönliche und potenziell vertrauliche Patientendaten. Ein Sicherheitsvorfall könnte diese sensiblen Daten offenlegen, was zu Peinlichkeiten oder finanziellem Schaden führen könnte. Wie stellen Sie die Integrität ihrer Daten sicher und gewährleisten, dass Ihre Systeme sicher sind? 

Hier wird erläutert, wie wir die Sicherheit einer Architektur angehen können.

## <a name="what-should-i-protect"></a>Was sollte ich schützen?

Die Daten, die Ihr Unternehmen speichert oder verwendet, bilden das Herzstück Ihrer zu schützenden Ressourcen. Diese Daten können sensible Kundendaten, Finanzinformationen Ihrer Organisation oder kritische Branchendaten sein, die Ihre Organisation benötigt. Neben den Daten ist auch die Sicherung der Infrastruktur, in der sie vorhanden sind, und der Identitäten, mit denen wir auf sie zugreifen, von entscheidender Bedeutung.

Ihre Daten können zusätzlichen gesetzlichen und regulatorischen Anforderungen unterliegen, je nachdem, wo Sie sich befinden, welche Art von Daten Sie speichern oder in welcher Branche Ihre Anwendung verwendet wird. Beispielsweise gibt es in den USA im Gesundheitswesen ein Gesetz namens Health Insurance Portability and Accountability Act (HIPAA). In der Finanzbrache wird der Umgang mit Kreditkartendaten durch den Payment Card Industry Data Security Standard (PCI DSS) geregelt. Organisationen, die Daten speichern, die diesen Gesetzen und Standards unterliegen, sind verpflichtet, bestimmte Sicherheitsvorkehrungen für diese Daten zu treffen. In Europa legt die Datenschutz-Grundverordnung (DSGVO) die Regeln für den Schutz personenbezogener Daten fest und definiert die Rechte des Einzelnen in Bezug auf gespeicherte Daten. Einige Länder verlangen, dass bestimmte Arten von Daten ihre Grenzen nicht überschreiten.

Wenn eine Sicherheitsverletzung eintritt, kann dies erhebliche Auswirkungen auf die Finanzen und den Ruf von Unternehmen und Kunden haben. Dies erschüttert das Vertrauen, das die Kunden bereit sind, in Ihr Unternehmen zu investieren, und kann sich auf seine langfristige Geschäftsentwicklung auswirken.

## <a name="defense-in-depth"></a>Tiefgehende Verteidigung

Ein Ansatz mit mehreren Ebenen zur Absicherung Ihrer Umgebung erhöht die Sicherheitslage Ihrer Umgebung. Die Ebenen der sog. _tiefgehenden Verteidigung_ können wir wie folgt aufschlüsseln:

* Daten
* Anwendungen
* VM/Compute
* Netzwerk
* Umkreis
* Richtlinien und Zugriff
* Physische Sicherheit

Jede Ebene konzentriert sich auf einen anderen Bereich, in dem Angriffe möglich sind, und schafft eine gewisse Schutzwirkung, sollte eine Ebene ausfallen oder von einem Angreifer umgangen werden. Wenn wir uns nur auf eine Ebene konzentrieren würden, hätte ein Angreifer ungehinderten Zugriff auf Ihre Umgebung, wenn er diese Ebene passieren würde. Die Behandlung der Sicherheit in Ebenen erhöht den Aufwand, den ein Angreifer treiben muss, um Zugang zu Ihren Systemen und Daten zu erhalten. Jede Ebene verfügt über unterschiedliche Sicherheitskontrollen, Technologien und Funktionen, die gelten. Bei der Ermittlung der zu implementierenden Schutzmaßnahmen sind die Kosten oft von Belang und müssen mit den Geschäftsanforderungen und dem Gesamtrisiko für das Unternehmen in Einklang gebracht werden.

![Abbildung der Verteidigung in der Tiefe mit Daten im Mittelpunkt. Die Daten werden durch folgende Sicherheitsringe geschützt: Anwendung, Compute, Netzwerk, Umgebung, Identität und Zugriff sowie physische Sicherheit.](../media/security-layers.png)

Es gibt kein einzelnes Sicherheitssystem und keine einzelne Kontrolle oder Technologie, die Ihre Architektur vollständig schützt. Sicherheit ist mehr als nur Technologie, es geht auch um Menschen und Prozesse. Die Schaffung einer Umgebung, die die Sicherheit ganzheitlich betrachtet und standardmäßig zur Anforderung erklärt, trägt dazu bei, dass Ihr Unternehmen so sicher wie möglich ist.

## <a name="common-attacks"></a>Gängige Angriffe

Auf jeder Ebene gibt es einige gängige Angriffstypen, vor denen Sie sich schützen müssen. Diese sind nicht allumfassend, können Ihnen aber eine Vorstellung davon geben, wie die einzelnen Ebenen angegriffen werden können und welche Arten von Schutz Sie berücksichtigen müssen.

* **Datenebene**: Die Offenlegung von Verschlüsselungsschlüsseln oder die Verwendung einer schwachen Verschlüsselung können Ihre Daten anfällig machen, falls ein unbefugter Zugriff erfolgt.
* **Anwendungsebene**: Die Einschleusung und Ausführung von bösartigem Code ist das Markenzeichen von Angriffen auf Anwendungsebene. Gängige Angriffe umfassen die SQL-Einschleusung und Cross-Site Scripting (XSS).
* **VM/Computeebene**: Schadsoftware ist eine gängige Methode, um eine Umgebung anzugreifen, bei der bösartiger Code ausgeführt wird, um ein System zu gefährden. Sobald Schadsoftware auf einem System vorhanden ist, können weitere Angriffe auftreten, die zu einer Offenlegung von Berechtigungen und einer Seitwärtsbewegung in der gesamten Umgebung führen.
* **Netzwerkebene**: Unnötige geöffnete Ports zum Internet sind eine gängige Angriffsmethode. Dazu könnte es gehören, SSH oder RDP für virtuelle Computer geöffnet zu lassen. Wenn diese geöffnet sind, können Brute-Force-Angriffe auf Ihre Systeme ermöglicht werden, wenn Angreifer versuchen, Zugriff zu erlangen.
* **Umkreisebene**: Denial-of-Service-Angriffe (DoS-Angriffe) treten häufig auf dieser Ebene auf. Diese Angriffe versuchen, Netzwerkressourcen zu überfordern, zwingen sie, offline zu gehen, oder machen sie unfähig, auf berechtigte Anforderungen zu reagieren.
* **Richtlinien- und Zugriffsebene**: Hier erfolgt die Authentifizierung für Ihre Anwendung. Dazu gehören ggf. moderne Authentifizierungsprotokolle wie OpenID Connect, OAuth oder Kerberos-basierte Authentifizierung wie Active Directory. Offengelegte Anmeldeinformationen stellen hier ein Risiko dar, und es ist wichtig, die Berechtigungen von Identitäten zu begrenzen. Wir möchten auch eine Überwachung einrichten, um nach möglichen kompromittierten Konten zu suchen (etwa nach Anmeldungen von ungewöhnlichen Orten).
* **Physische Ebene**: Unbefugter Zutritt zu Einrichtungen durch Methoden wie unberechtigte Verwendung von Sicherheitscodes und Diebstahl von Sicherheitsausweisen ist auf dieser Ebene zu finden.

## <a name="shared-security-responsibility"></a>Gemeinsame Verantwortung für die Sicherheit

Wenn wir das Modell der gemeinsamen Verantwortung erneut aufgreifen, können wir es im Zusammenhang mit Sicherheit neu fassen. Je nach Art des von Ihnen gewählten Diensts werden einige Sicherheitsvorkehrungen in den Dienst integriert, während andere in Ihrer Verantwortung verbleiben. Eine sorgfältige Bewertung der von Ihnen gewählten Dienste und Technologien ist unerlässlich, um sicherzustellen, dass Sie die richtigen Sicherheitskontrollen für Ihre Architektur bereitstellen.

![Abbildung, die zeigt, wie sich Cloudanbieter und Kunden Sicherheitsaufgaben unter verschiedenen Arten von Clouddienstmodellen teilen: lokal, Infrastructure-as-a-Service, Platform-as-a-Service und Software-as-a-Service. ](../media/shared_responsibilities.png)
