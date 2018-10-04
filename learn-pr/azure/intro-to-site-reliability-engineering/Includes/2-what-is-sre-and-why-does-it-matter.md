In der Regel sollten Sie am Anfang ansetzen. Beginnen wir mit der grundlegenden Frage: „Was ist Site Reliability Engineering?“
Es sind viele Antworten auf diese Frage im Umlauf, einschließlich einem [Zitat](https://landing.google.com/sre/book/chapters/introduction.html) von der Person, die den Begriff geprägt hat: Ben Treynor Sloss (Google). Seine Aussage ist jedoch die beste verfügbare Antwort:

> Bei Site Reliability Engineering handelt es sich um einen Aufgabenbereich bei der Entwicklung, der dafür vorgesehen ist, Organisationen beim Erreichen eines angemessenen Grads an Zuverlässigkeit für ihre Systeme, Dienste und Produkte zu unterstützen.

Später kommen noch andere Definitionen dazu. Wir beginnen jedoch mit dieser. Diese Definition enthält zwei wichtige Bestandteile, die uns bei näherer Betrachtung zur Frage „Warum ist das wichtig?“ führen.

## <a name="reliability"></a>Reliability (Zuverlässigkeit)

In der Mitte von „SRE“ steht Reliability für „Zuverlässigkeit“. Die Definition spricht nicht vom „angemessenen Grad an Leistung“, „angemessenen Grad an Effizienz“, „angemessenen Grad an Stabilität“ oder vom „angemessenen Grad an Einkommen“, sondern vom „angemessenen Grad an Zuverlässigkeit“. Warum?

Dies wird im Folgenden veranschaulicht. Hier sehen Sie einen Screenshot. Was wird Ihrer Meinung nach darauf dargestellt? Fahren Sie nicht fort, bis Sie eine Idee haben oder aufgeben. Hinweis: Wenn Sie nicht viele Details im Bild erkennen können, ist das kein Problem, es wird in Ihrem Browser perfekt gerendert.

   ![Screenshot 1](../media/02_blank-screenshot.png)

Das Bild ist ein Screenshot, der darstellt, wie eine PHP-App (ohne zusätzliche Debugging-Unterstützung) aussieht, wenn ein Fehler auftritt. Für eine Java-App sieht dies etwa folgendermaßen aus:

   ![Screenshot 2](../media/02_java-screenshot.png)

Warum sehen wir uns diese Beispiele an? Jeder dieser Screenshots stellt eine Anwendung dar, in deren Erstellung ein Unternehmen viel Zeit, Energie und viele Ressourcen investiert hat. Wenn die Anwendung nicht betriebsbereit ist, wenn ein Kunde darauf zugreifen muss, also wenn sie nicht zuverlässig ist, profitiert niemand von ihr, am wenigsten das Unternehmen. Mangelnde Zuverlässigkeit kann einem Unternehmen sogar schaden, z.B. dem Ruf, den Finanzen, Verträgen oder der Arbeitsmoral.

Deshalb ist Zuverlässigkeit so wichtig und die grundlegende Eigenschaft von SRE – vielleicht sogar die grundlegende Eigenschaft eines Diensts, Systems oder Produkts. Zuverlässigkeit kann eine Reihe von Faktoren umfassen (diese werden später näher erläutert). Befassen wir uns jedoch zunächst mit dem zweiten entscheidenden Teil der Definition.

## <a name="appropriate-levels-of-reliability"></a>Angemessener Grad an Zuverlässigkeit

Beim ersten Lesen der Definition ist Ihnen ein weiteres wichtiges Wort möglicherweise nicht aufgefallen, das nun näher erläutert werden soll:

> Bei Site Reliability Engineering handelt es sich um einen Aufgabenbereich bei der Entwicklung, der dafür vorgesehen ist, Organisationen beim Erreichen eines *angemessenen* Grads an Zuverlässigkeit für ihre Systeme, Dienste und Produkte zu unterstützen.

Warum ist dieses Wort so wichtig?

Eine wichtige Beobachtung der SRE-Branche ist die, dass es wenige Systeme und Dienste gibt, für die eine Zuverlässigkeit von 100 % erforderlich ist. Eine wichtige Ausnahme stellen z.B. die Luftfahrt oder medizinische Geräte dar, bei denen Zuverlässigkeit über Leben und Tod entscheiden kann.

Tatsächlich gibt es jedoch nur wenige Situationen, in denen Zuverlässigkeit erstrebenswert ist. Der Aufwand und die Ressourcen (und somit die Kosten), die für mehr Zuverlässigkeit aufgewendet werden müssen, steigen mit dem angestrebten Grad an Zuverlässigkeit an. Einfach gesagt verschwenden Sie Zeit und Geld, wenn Sie einen Grad an Zuverlässigkeit anstreben, den Sie nicht benötigen. _Sie möchten den angemessen Grad an Zuverlässigkeit in Ihren Systemen, Diensten und Produkten erreichen._ 

Dieser muss den Anforderungen Ihres Unternehmens entsprechen und dennoch umsetzbar sein. Wenn Ihre Kunden beispielsweise eine Verbindung mit Ihnen über ein Netzwerk herstellen, das nicht zu 100 % zuverlässig ist (gehen wir von 90 % aus), ist es der Definition nach eine Verschwendung von Zeit und Geld, in eine Zuverlässigkeit von 95 % zu investieren. _Sie möchten den angemessen Grad an Zuverlässigkeit in Ihren Systemen, Diensten und Produkten erreichen._

SRE denkt diesen Pragmatismus weiter. Wenn wir nun einen gewünschten Grad an Zuverlässigkeit im Sinn haben, stellt sich die Frage, welche Handlungen erfolgen sollen, wenn dieser Grad erfolgreich erreicht oder sogar übertroffen wird. Gleichermaßen stellt sich die Frage, was geschehen soll, wenn dieser nicht erreicht wird.

Bleiben Sie dran, denn genau diese Fragen werden nach einer kurzen Unterbrechung beantwortet, die Sie weiter in den Kontext einführen soll.
