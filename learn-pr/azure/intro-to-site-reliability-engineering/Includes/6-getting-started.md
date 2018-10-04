In der letzten Einheit dieses Moduls wird besprochen, welche weiteren Schritte erforderlich sind, wenn Sie Interesse an der Erkundung von SRE haben. 

## <a name="reading-and-watching"></a>Lesen und Überwachen

Ausführlichere Informationen zu SRE finden Sie in einer aus drei Büchern bestehenden Buchreihe, die zu diesem Thema veröffentlicht wurde

1. [_Site Reliability Engineering: How Google Runs Production Systems_](http://shop.oreilly.com/product/0636920041528.do) (Site Reliability Engineering: So betreibt Google Produktionssysteme), auch bekannt unter „das SRE-Buch“
1. [_The Site Reliability Workbook: Practical Ways to Implement SRE_](http://shop.oreilly.com/product/0636920132448.do) (Das Site Reliability-Arbeitsbuch: Praktische Methoden zum Implementieren von SRE), auch bekannt unter „das SRE-Arbeitsbuch“
1. [_Seeking SRE: Conversations About Running Production Systems at Scale_](http://shop.oreilly.com/product/0636920063964.do) (SRE im Detail: Über die Ausführung umfangreicher Produktionssysteme)

(Eine Info am Rande: Der Hauptautor dieses Moduls ist Kurator bzw. Editor des dritten Buchs)

Alle diese Bücher enthalten wichtige Informationen:

- Das SRE-Buch enthält eine ausführliche Erläuterung der Vorgehensweise von Google bei der Implementierung von SRE im Verlauf der Jahre.

- Das SRE-Arbeitsbuch ist der Nachfolger des SRE-Buchs, in dem noch mehr ins Details gegangen wird. Darin geht es nicht nur um die Frage, auf „was“ von SRE Google und andere zurückgreifen, sondern auch um das Wie und das Warum.

- „SRE im Detail“ bietet einen umfassenderen Überblick über die SRE-Welt, der über den Ursprung dieser Disziplin hinausgeht. Dazu zählen Informationen zur Vorgehensweise bei der Implementierung von SRE in anderen Umgebungen.

Sie sollten alle drei Bücher beim Lesen kritisch hinterfragen. Nicht alle Inhalte dieser Bücher finden sind auf Sie und Ihr Unternehmen anwendbar. Nehmen Sie sich die Zeit, um die Informationen zu ermitteln, bei denen Sie sicher sind, dass Sie damit einen positiven Einfluss schaffen. Überlegen Sie, welche Bereiche Ihrer Unternehmenskultur und -werte die Funktionsweise von SRE unterstützen und welche Bereiche möglicherweise eine Herausforderung darstellen.

Wenn Sie eher ein visueller Mensch sind, sehen Sie sich den Vortrag [Keys to SRE](https://www.usenix.org/conference/srecon14/technical-sessions/presentation/keys-sre) (Schlüssel zu SRE) von Ben Treynor auf der Konferenz SREcon14 an. Treynor erläutert auf überzeugende Weise, wie er SRE definieren würde (zumindest im Kontext von Google). Weitere aufgezeichnete Vorträge zu SRE aus [dieser Konferenzreihe](https://www.usenix.org/conferences/byname/925) sowie andere Vorträge können wirklich nützlich sein.

## <a name="talk-to-other-interested-people"></a>Tauschen Sie sich mit anderen interessierten Personen aus

Es ist wichtig, dass Sie sich anhand von Lesematerial ausführlich über SRE informieren. Häufig ist es jedoch noch wichtiger, sich mit Kollegen darüber auszutauschen. Das Diskutieren über Herausforderungen, Erfolge und Fehler rund um SRE kann eine entscheidende Rolle beim Erlangen eines umfassenden Verständnisses des Themas spielen. 

Es gibt eine Reihe von Meetups und Konferenzen, die SRE zum Inhalt haben. Die global verteilten [SREcon-Konferenzen](https://www.usenix.org/conferences/byname/925) von USENIX sind vermutlich am relevantesten (Hinweis: Der Hauptautor dieses Moduls ist einer der Mitbegründer von SREcon).

Immer mehr SRE-Inhalte finden ihren Weg in Konferenzen wie [Velocity](https://conferences.oreilly.com/velocity), [LISA](https://www.usenix.org/conferences/byname/5) sowie lokale DevOps-Konferenzen wie [DevOps Days](https://www.devopsdays.org). Suchen Sie überall, wo es möglich ist, nach diesen Inhalten und weiteren Personen, die an diesem Thema interessiert sind.

## <a name="first-steps-at-work"></a>Erste Schritte bei der Arbeit

Wenn Sie zunächst erkunden möchten, wie es wäre, SRE in Ihrer Umgebung einzubringen, sollten Sie bedenken, dass es bei SRE nicht um „alles oder nichts“ geht.  Sie können SRE-Prinzipien und -Methoden in kleinen Schritten einführen.

Mickey Dickerson – ein SRE, der für die Entwicklung des United States Digital Service (verantwortlich für die Rettung von healthcare.gov) bekannt ist – hat als Hommage an die Maslowsche Bedürfnishierarchie den Vorschlag einer Zuverlässigkeitshierarchie unterbreitet. Sie ist im ersten SRE-Buch im Abschnitt [Practices](https://landing.google.com/sre/book/chapters/part3.html) (Methoden) zu finden.

In dieser Hierarchie wird vorgeschlagen, dass zunächst dafür gesorgt werden muss, dass die Überwachung in Ihrer Umgebung funktionsfähig und vertrauenswürdig ist. Dies sollte auch einer der ersten Schritte auf dem Weg zur Integration von SRE in Ihre Umgebung sein. Zuverlässigkeit (bzw. eine Verbesserung oder Verschlechterung) kann nicht festgestellt werden, wenn diese nicht messbar ist.

Sobald Sie über eine vertrauenswürdige Überwachungsplattform verfügen, wählen Sie im nächstmöglichen Schritt bei der Arbeit einen Dienst aus und beginnen mit SLI- und SLO-Konversationen darüber. Fangen Sie klein an. Erstellen Sie SLIs und SLOs für den Dienst, implementieren Sie diese in Ihrem Überwachungssystem und beobachten Sie, was geschieht, wenn Sie anhand des SRE-Fokus auf die Zuverlässigkeit achten. Dies ist ein idealer Ausgangspunkt.
