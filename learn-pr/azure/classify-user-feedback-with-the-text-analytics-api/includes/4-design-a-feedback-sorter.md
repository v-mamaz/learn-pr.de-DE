Können wir unser Wissen Analyse von Text in eine praktische Lösung arbeiten. Unsere Lösung konzentriert sich auf die Standpunktanalyse von Textdokumenten. Wir legen Sie den Kontext durch die Beschreibung des Problems, die wir in Angriff zu nehmen möchten.

## <a name="manage-customer-feedback-more-efficiently"></a>Feedback von Kunden effizienter verwalten

Soziale Medien ist aktiv, etwas über Ihren Produkten. Ihr Feedback-e-Mail-Alias ist auch aktiv mit Kunden, die ihrer Meinung nach Ihres Produkts zu teilen.

Wie bei jedem neuen Start der Fall ist, befinden Sie durch die IT-Mantra der Überwachung für Ihre Kunden. Allerdings hat der Erfolg Ihres Produkts das beibehalten dieser Zusage einfacher gesagt als getan. Es ist ein guter Problem jedoch ein Problem über die gleichen.

Das Team kann nicht mit der Menge an Feedback nicht mehr Schritt halten. Sie benötigen Sie Hilfe, sortieren das Feedback, damit Probleme möglichst effizient verwaltet werden können. Als der leitende Entwickler in der Organisation wurden Sie gebeten, eine Lösung zu erstellen.

Sehen wir uns einige allgemeinen Voraussetzungen an:

|Anforderung  | Details  |
|---------|---------|
|Kategorisieren Sie Feedback, damit wir darauf reagieren können.     |   Nicht alle Feedback entspricht. Einige zeugt leuchtendes. Ihre Rückmeldung ist Kritik, die von einem frustrierten Kunden bissigem.  Sie können nicht vielleicht feststellen, was der Kunde in anderen Fällen will. <br/><br/>Mindestens würden mit Angabe der Stimmung oder Ton, Feedback von uns es kategorisieren helfen.     |
|Die Lösung muss hoch- oder herunterskaliert bedarfsorientiert skaliert werden.    |   Wir sind ein Startup. Feste Kosten sind schwer zu rechtfertigen, und wir nicht wissen, das genaue Muster der Feedback-Datenverkehr. Wir benötigen eine Lösung, die Bursts von Aktivität, aber die Kosten so wenig wie möglich während Ruhezeiten meistern können. <br/><br/> Eine serverlose Architektur, die in Rechnung gestellt, in einem Verbrauchsplan ist ein guter Kandidat in diesem Fall aus.     |
| Erstellen Sie eine minimale geeignete Product (MVP), aber stellen Sie die Lösung angepasst.    | Heute möchten wir Feedback zu kategorisieren, damit wir unsere begrenzten Ressourcen auf das Feedback anwenden können, die wichtig ist. Wenn ein Kunde frustriert ist, möchten wir sofort zu wissen, und Ihnen zu chatten.  In Zukunft werden wir diese Lösung mehr verbessern. Eine Idee für ein neues Feature besteht darin, überprüfen Sie wichtige Begriffe in einem Feedback Problempunkte, die erkennen, bevor sie kritische Masse mit unseren Kunden erreichen.   Als weitere Idee ist, Rückgabe von Antworten an Kunden zu automatisieren, die entweder positiv oder neutral sind. Obwohl sie uns gern, möchten wir sie wissen, dass wir ihr Feedback weiterhin überwacht werden. <br/><br/>Eine Lösung, die eine Plug & Play Architektur bietet ist sehr gut. Wir könnten Sie z. B. Warteschlangen als eine Form der Factory Zeile verwenden. Sie führen eine Aufgabe und platzieren Sie das Ergebnis in eine Warteschlange für den nächsten Teil des Systems, wenn Sie die Datei und Prozess auszuwählen.   |
|Bereitstellen Sie schnell.     |   Wir haben alle eine vor gehört. Beachten Sie, dass diese Lösung arbeitet als MVP und schnell mit diesem Szenario getestet werden soll. Um die Geschwindigkeit und Qualität bedeutet weniger Code schreiben. <br/><br/> Nutzen der Textanalyse-API bedeutet, dass wir nicht zum Trainieren eines Modells, um Stimmung erkennen.  Mithilfe von Azure Functions und binden deklarativ an Warteschlangen reduziert die Menge an Code geschrieben haben.  Eine serverlose Projektmappe bedeutet auch, dass wir keine Server-Verwaltung kümmern.   |

Unsere vorgeschlagene Lösung für die einzelnen Anforderungen in der obigen Tabelle gibt einen Einblick in das Zuordnen von Anforderungen zu Lösungen.  Jetzt überprüfen wir eine Lösung könnte folgendermaßen aussehen auf Basis von Azure.

## <a name="a-solution-based-on-azure-functions-azure-queue-storage-and-text-analytics-api"></a>Eine Lösung auf Grundlage von Azure Functions, Azure Queue Storage und Textanalyse-API

Im folgende Diagramm ist ein Entwurfsvorschlag für eine Lösung. Es verwendet drei Kernkomponenten von Azure – Microsoft Cognitive Services, Azure Queue Storage und Azure Functions in Azure.

![Konzeptionelle Darstellung der Architektur sortieren Feedback.](../media/proposed-solution.PNG)

Die Idee ist, dass Textdokumente, Feedback von Benutzern in einer Warteschlange platziert werden, die wir mit dem Namen haben *Feedback-Q* in der obigen Abbildung. Der Eingang einer Nachricht, die mit dem Textdokument in die Warteschlange wird auslösen, oder starten, Ausführung. Die Funktion liest Nachrichten, die neue Dokumente aus der Eingabewarteschlange und sendet diese zur Analyse der Textanalyse-API. Basierend auf den Ergebnissen, die die API gibt zurück, wird eine neue Nachricht, die mit dem Dokument in eine Ausgabewarteschlange zur weiteren Verarbeitung platziert.

Das Ergebnis, das wir für jedes Dokument erhalten wird, einen stimmungswert zwischen. Die Ausgabe-Warteschlangen werden verwendet, um Feedback zu positiven, neutral und negative sortiert zu speichern. Hoffentlich wird die negative Warteschlange immer leer sein. :-)   Sobald wir jede eingehende in zahlreichen rückmeldungen in einer Ausgabewarteschlange basierend auf Stimmung Buckets zugeordnet haben, können Sie sich vorstellen, Logik, um die Nachrichten in jeder Warteschlange Aktionen hinzufügen.

Wir sehen uns ein Flussdiagramm weiter, um finden, was die Funktionslogik tun muss.

![Flussdiagramm der Logik innerhalb der Azure-Funktion zum Sortieren von Textdokumenten Stimmung in Ausgabe Warteschlangen.](../media/flow.PNG)

Unsere Logik ist wie ein Router. Es akzeptiert eine Texteingabe und leitet sie an einer Ausgabewarteschlange basierend auf dem stimmungswert des Texts. Wir setzen voraus, auf die Textanalyse-API. Während die Logik einfach scheint, entfernt dieser Funktion müssen für Personen im Team Feedback manuell analysieren.

## <a name="steps-to-implement-our-solution"></a>Schritte zur Implementierung unserer Lösung

Um die in dieser Einheit beschriebene Lösung zu implementieren, müssen wir die folgenden Schritte ausführen.

1. Erstellen Sie eine Funktions-app zum Hosten unserer Lösung.

1. Suchen Sie nach der Stimmung im eingehenden feedbacknachrichten, die mit der Textanalyse-API. Wir verwenden unsere Zugriffsschlüssel aus der vorherigen Übung und Schreiben von Code zum Senden der Anforderungen.

1. Senden Sie Feedback für die Verarbeitung von Warteschlangen basierend auf die Stimmungslage.

Betrachten wir nun unsere Funktions-app erstellen.