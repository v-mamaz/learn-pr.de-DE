Um Ihnen die Entscheidung zu erleichtern, ob serverloses Computing das Richtige für Sie ist, möchten wir zunächst erläutern, worum es bei serverlosem Computing eigentlich geht.

## <a name="what-is-serverless-compute"></a>Was ist serverloses Computing?

Serverloses Computing kann als Function-as-a-Service (FaaS) oder Microservice aufgefasst werden, der auf einer Cloudplattform gehostet wird. Ihre Geschäftslogik wird in Form von Funktionen ausgeführt, sodass Sie die Infrastruktur nicht manuell bereitstellen oder skalieren müssen. Der Cloudanbieter verwaltet die Infrastruktur. Ihre App wird automatisch je nach Last horizontal hoch- oder herunterskaliert. Azure bietet mehrere Möglichkeiten, diese Art von Architektur zu erstellen. Die beiden gängigsten sind Azure Logic Apps und Azure Functions, auf die wir uns in diesem Modul konzentrieren.

## <a name="what-is-azure-functions"></a>Was ist Azure Functions?

Azure Functions ist eine serverlose Anwendungsplattform. Sie ermöglicht Entwicklern, Geschäftslogik zu hosten, die ohne Bereitstellung von Infrastruktur ausgeführt werden kann. Azure Functions bietet systeminterne Skalierbarkeit, und Ihnen werden nur die verwendeten Ressourcen in Rechnung gestellt. Sie können Ihren Funktionscode in der Sprache Ihrer Wahl schreiben, so z.B. in C#, F# und JavaScript. Unterstützung für NuGet und NPM wird ebenfalls geboten, sodass Sie beliebte Bibliotheken in Ihrer Geschäftslogik verwenden können.

## <a name="benefits-of-a-serverless-compute-solution"></a>Vorteile einer serverlosen Computinglösung

Serverloses Computing ist eine hervorragende Möglichkeit zum Hosten von Geschäftslogikcode in der Cloud. Mit serverlosen Lösungen wie Azure Functions können Sie Ihre Geschäftslogik in der Sprache Ihrer Wahl gestalten. Sie erhalten eine automatische Skalierung, müssen keine Server verwalten, und die Abrechnung erfolgt nach Verbrauch und nicht nach reservierter Zeit. Es folgen einige zusätzliche Merkmale einer serverlosen Lösung, die Sie beachten sollten.

### <a name="avoids-over-allocation-of-infrastructure"></a>Vermeiden von übermäßiger Zuteilung von Infrastruktur

Nehmen wir an, Sie haben VM-Server bereitgestellt und mit genügend Ressourcen zur Bewältigung Ihrer Spitzenlastzeiten konfiguriert. Bei geringer Last zahlen Sie möglicherweise für Infrastruktur, die Sie gar nicht nutzen. Serverloses Computing löst das Problem der übermäßigen Zuteilung durch automatisches zentrales Hochskalieren oder Herunterskalieren, und Ihnen wird nur die Nutzung in Rechnung gestellt, wenn Ihre Funktion Aufgaben verarbeitet.

### <a name="stateless-logic"></a>Zustandslose Logik

Zustandslose Funktionen sind gute Kandidaten für serverloses Computing. Funktionsinstanzen werden bei Bedarf erstellt und zerstört. Wenn der Zustand erforderlich ist, kann er in einem zugeordneten Speicherdienst gespeichert werden.

### <a name="event-driven"></a>Ereignisgesteuert

Funktionen sind _ereignisgesteuert_. Das heißt, dass sie nur als Reaktion auf ein (Trigger genanntes) Ereignis ausgeführt werden, z.B. beim Empfang einer HTTP-Anforderung oder Hinzufügen einer Nachricht zu einer Warteschlange. Sie konfigurieren einen Trigger im Rahmen der Funktionsdefinition. Dieser Ansatz vereinfacht Ihren Code, weil Sie die Quelle der Daten (Trigger/Eingabebindung) und das Ziel (Ausgabebindung) deklarieren können. Sie müssen keinen Code zur Überwachung von Warteschlangen, Blobs, Hubs usw. schreiben. Sie können sich ausschließlich auf die Geschäftslogik konzentrieren.

### <a name="functions-can-be-used-in-traditional-compute-environments"></a>Funktionen können in herkömmlichen Compute-Umgebungen verwendet werden.

Funktionen sind eine zentrale Komponente des serverlosen Computings, aber auch eine allgemeine Computeplattform für die Ausführung jeglicher Art von Code. Sollten sich die Anforderungen Ihrer App ändern, können Sie Ihr Projekt in einer nicht serverlosen Umgebung implementieren. Dies gibt Ihnen die nötige Flexibilität, um die Skalierung zu verwalten, für die Ausführung in virtuellen Netzwerken zu sorgen und sogar Ihre Funktionen vollständig zu isolieren.

## <a name="drawbacks-of-a-serverless-compute-solution"></a>Nachteile einer serverlosen Computinglösung

Serverloses Computing ist nicht immer die geeignete Lösung für das Hosten Ihrer Geschäftslogik. Nachstehend sind einige Merkmale von Funktionen aufgeführt, die Ihre Entscheidung zum Hosten Ihrer Dienste mit serverlosem Computing beeinflussen könnten.

### <a name="execution-time"></a>Ausführungszeit

Standardmäßig beträgt das Zeitlimit von Funktionen 5 Minuten. Dieser Wert kann mit maximal 10 Minuten konfiguriert werden. Wenn die Ausführung der Funktion mehr als 10 Minuten benötigt, können Sie sie auf einem virtuellen Computer hosten. Wenn Ihr Dienst darüber hinaus über eine HTTP-Anforderung ausgelöst wird, und Sie diesen Wert als HTTP-Antwort erwarten, wird das Timeout noch weiter auf 2,5 Minuten beschränkt. Schließlich gibt es auch eine Option mit dem Namen **Durable Functions**, mit der Sie die Ausführung mehrerer Funktionen ohne Zeitlimit koordinieren können.

### <a name="execution-frequency"></a>Ausführungshäufigkeit

Das zweite Merkmal ist die Ausführungshäufigkeit. Wenn Sie erwarten, dass Ihre Funktion fortlaufend von mehreren Clients ausgeführt wird, ist es ratsam, die Nutzung zu schätzen und die Kosten für das Verwenden von Funktionen entsprechend zu berechnen. Es kann kostengünstiger sein, Ihren Dienst auf einem virtuellen Computer zu hosten.

Hinsichtlich Skalierung kann bei bis zu maximal 200 Instanzen insgesamt nur alle 10 Sekunden eine Funktions-App-Instanz erstellt werden. Denken Sie daran, dass jede Instanz mehrere gleichzeitige Ausführungen unterstützt. Es gibt also keine Beschränkung für den Datenverkehr, den eine einzelne Instanz verarbeiten kann. Weil verschiedene Arten von Triggern unterschiedliche Anforderungen an die Skalierung haben, ermitteln Sie den Trigger Ihrer Wahl, und machen Sie seine Grenzen ausfindig.
