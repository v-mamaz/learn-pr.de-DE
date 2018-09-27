Wenden wir unser Wissen zur Textanalyse auf eine praktische Lösung an. Unsere Lösung bezieht sich auf die Standpunktanalyse von Textdokumenten. Sehen wir uns den Kontext an, indem wir das Problem umreißen, das in Angriff genommen werden soll.

## <a name="manage-customer-feedback-more-efficiently"></a>Effizienteres Verwalten von Kundenfeedback

Nehmen wir einmal an, das Produkt Ihres Unternehmens ist in den sozialen Medien in aller Munde. Auch Ihr Feedback-E-Mail-Alias wird von Kunden oft genutzt, um ihre Meinung zu Ihrem Produkt mitzuteilen.

Wie bei jedem jungen Startup ist das Feedback Ihrer Kunden das A und O für Sie. Doch der Erfolg Ihres Produkts stellt Sie auch vor Herausforderungen, um Ihr Versprechen zu erfüllen. Dies ist zwar ein Luxusproblem, jedoch nichtsdestotrotz ein Problem, das es zu lösen gilt.

Denn das Team kann die Menge an Feedback einfach nicht mehr verarbeiten. Es benötigt Hilfe beim Sortieren des Feedbacks, um Probleme möglichst effizient verwalten zu können. Als leitender Entwickler in der Organisation wurden Sie gebeten, eine geeignet Lösung zu erstellen.

Sehen wir uns einige allgemeine Voraussetzungen an:

|Anforderung  | Details  |
|---------|---------|
|Das Feedback muss kategorisiert werden, damit das Team entsprechend darauf reagieren kann.     |   Nicht alle Feedbackmitteilungen sind gleich. Bei einigen handelt es sich um lobende Bekundungen, während in anderen Feedbackmitteilungen harsche Kritik von unzufriedenen Kunden geübt wird. Und in manchen Fällen ist es womöglich unklar, was der Kunde eigentlich möchte. <br/><br/>Wenigstens ein Hinweis auf den Standpunkt oder den Ton des Feedbacks würde Ihnen schon bei der Kategorisierung helfen.     |
|Die Lösung sollte sich je nach Bedarf zentral hoch- oder herunterskalieren lassen können.    |   Denken Sie an unser Szenario: Wir sind ein Startup. Fixkosten lassen sich nur schwer rechtfertigen, und wir haben kein genaues Muster im Feedbackdatenverkehr feststellen können. Wir benötigen also eine Lösung, die Aktivitätsbursts verarbeiten kann, in ruhigen Zeiten jedoch möglichst wenig Kosten verursacht. <br/><br/> In diesem Fall empfiehlt sich eine serverlose Architektur, die basierend auf einem Verbrauchstarif abgerechnet wird.     |
| Eine MVP-Lösung (Minimal Viable Product; Lösung mit dem minimalem Funktionsumfang, der für Kunden einen Wert darstellt) muss erstellt werden, die jedoch bei Bedarf anpassbar ist.    | Heutzutage sollte Feedback kategorisiert werden, damit wir unsere begrenzten Ressourcen für das Feedback einsetzen können, das eine hohe Priorität hat. Ist ein Kunde frustriert, sollten wir umgehend darüber Bescheid wissen und mit diesem in Dialog treten. Diese Lösung wird in Zukunft um zusätzliche Features erweitert. Ein neues Feature könnte beispielsweise sein, Schlüsselbegriffe in einem Feedback zu überprüfen, um Probleme zu erkennen, bevor sie ein kritisches Ausmaß bei unseren Kunden annehmen. Darüber hinaus könnten Antworten an Kunden automatisiert werden, die entweder positiv oder neutral sind. Denn auch wenn Kunden nur lobende Worte für uns haben, möchten wir sie wissen lassen, dass ihr Feedback weiterhin beachtet wird. <br/><br/>Für dieses Szenario eignet sich eine Lösung mit einer Plug & Play-Architektur. Beispielsweise könnten wir Warteschlangen nach dem Fließbandprinzip einsetzen. Sie führen also eine Aufgabe durch, und platzieren das Ergebnis in eine Warteschlange, die der anschließend zuständige Teil des Systems übernimmt und weiterverarbeitet.   |
|Es muss schnell eine Lösung bereitgestellt werden.     |   Ein altbekanntes Gesetz. Denken Sie daran, dass es hier um eine MVP-Lösung geht und diese schnell in unserem Szenario getestet werden soll. Um eine schnelle und qualitativ angemessene Lösung bereitzustellen, müssen wir den Umfang des zu schreibenden Codes einschränken. <br/><br/> Der Vorteil der Textanalyse-API besteht darin, dass ein Modell nicht für die Erkennung des Standpunkts trainiert werden muss. Mithilfe von Azure Functions und deklarativen Bindungen an Warteschlangen wird die Menge an Code, der geschrieben werden muss, reduziert. Eine serverlose Lösung bedeutet zudem, dass die Serververwaltung wegfällt.   |

Unsere vorgeschlagenen Lösungen für die einzelnen Anforderungen in der obigen Tabelle bieten einen Einblick in den Denkprozess, um passende Lösungen für die jeweiligen Anforderungen zu finden. Sehen wir uns nun an, wie eine Lösung auf Basis von Azure aussehen könnte.

## <a name="a-solution-based-on-azure-functions-azure-queue-storage-and-text-analytics-api"></a>Eine Lösung auf Grundlage von Azure Functions, Azure Queue Storage und der Textanalyse-API

Das folgende Diagramm zeigt einen Entwurfsvorschlag für eine Lösung. Darin werden drei Kernkomponenten von Azure verwendet: Azure Queue Storage, Azure Functions und Azure Cognitive Services.

![Konzeptionelle Darstellung einer Architektur zum Sortieren von Feedback](../media/proposed-solution.PNG)

Das obige Diagramm zeigt, wie Textdokumente mit Benutzerfeedback in eine Warteschlange mit dem Namen *new-feedback-q* eingefügt werden. Das Eintreffen einer Nachricht mit dem Textdokument in der Warteschlange löst die Ausführung bzw. den Start der Funktion aus. Die Funktion liest Nachrichten mit neuen Dokumenten aus der Eingabewarteschlange und sendet diese zur Analyse an die Textanalyse-API. Basierend auf den Ergebnissen, die die API zurückgibt, wird eine neue Nachricht mit dem Dokument zur weiteren Verarbeitung in eine Ausgabewarteschlange eingefügt.

Das für die einzelnen Dokumente berechnete Ergebnis ergibt einen Stimmungswert. In den Ausgabewarteschlangen wird Feedback gespeichert, und zwar sortiert nach positivem, neutralem und negativem Feedback. Die Warteschlange für negatives Feedback ist dabei hoffentlich stets leer. Sobald wir jedes eingehende Feedback basierend auf der Stimmung der jeweiligen Ausgabewarteschlange zugeordnet haben, können Sie beispielsweise Logik hinzufügen, um entsprechende Maßnahmen für die Nachrichten in den Warteschlangen vorzunehmen.

Sehen wir uns als Nächstes ein Flussdiagramm an, um zu erfahren, welche Schritte die Funktionslogik durchführen muss.

![Flussdiagramm zur Logik in der Azure-Funktion zum Sortieren von Textdokumenten nach Standpunkt in Ausgabewarteschlangen](../media/flow.PNG)

Unsere Logik ist wie ein Router. Sie empfängt eine Texteingabe und leitet sie abhängig vom Standpunktwert des Texts an eine Ausgabewarteschlange weiter. Wir sind auf die Textanalyse-API angewiesen. Zwar wirkt die Logik recht simpel, doch durch diese Funktion entfällt die Notwendigkeit für Teammitglieder, Feedback manuell zu analysieren.

## <a name="steps-to-implement-our-solution"></a>Schritte zur Implementierung unserer Lösung

Um die in dieser Einheit beschriebene Lösung zu implementieren, müssen die folgenden Schritte durchgeführt werden.

1. Erstellen Sie eine Funktions-App zum Hosten der Lösung.

1. Prüfen Sie den Standpunkt in eingehenden Feedbacknachrichten mittels der Textanalyse-API. Wir verwenden unseren Zugriffsschlüssel aus der vorherigen Übung und schreiben Code, um die Anforderungen zu senden.

1. Veröffentlichen Sie Feedback für die verarbeitenden Warteschlangen basierend auf der Stimmung.

Fahren wir nun mit der Erstellung der Funktions-App fort.