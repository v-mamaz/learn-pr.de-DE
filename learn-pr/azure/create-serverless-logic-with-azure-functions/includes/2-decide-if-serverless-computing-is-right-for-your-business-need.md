Bevor Sie den Temperaturdatendienst erstellen, sollten Sie sicherstellen, dass serverloses Computing die beste Lösung für den Auftrag ist. 

## <a name="what-is-serverless-compute"></a>Was ist serverloses Computing?
Serverloses Computing kann als Function-as-a-Service (FaaS) oder Microservice aufgefasst werden, der auf einer Cloudplattform gehostet wird. Diese Funktion enthält Geschäftslogikcode, der ohne manuelle Bereitstellung oder Skalierung der Infrastruktur ausgeführt werden kann. Die Hostingplattform ist abstrahiert; es gibt keine Server, auf die direkt zugegriffen werden kann, und keine Skalierung muss geschätzt werden. 

## <a name="what-is-azure-functions"></a>Was ist Azure Functions?
Azure Functions ist eine serverlose Anwendungsplattform. Sie ermöglicht Entwicklern, Geschäftslogik zu hosten, die ohne Bereitstellung von Infrastruktur ausgeführt werden kann. Azure Functions bietet systeminterne Skalierbarkeit, und es werden nur die verwendeten Ressourcen in Rechnung gestellt. Azure Functions kann in einer Vielzahl von Sprachen einschließlich C#, F# und JavaScript codiert werden und unterstützt NuGet sowie NPM, sodass Sie viele beliebte Bibliotheken einbeziehen können. 

## <a name="when-do-you-use-serverless-compute"></a>Wann verwenden Sie serverloses Computing?
Serverloses Computing ist eine hervorragende Möglichkeit zum Hosten von Geschäftslogikcode in der Cloud. Es bietet automatische Skalierung, Sie müssen keine Server verwalten, es gibt keine Abrechnung nach Sekundenbruchteilen, und mehrere Programmiersprachen stehen für die Implementierung zur Auswahl. Serverloses Computing weist einige weitere positive Merkmale auf.

### <a name="avoid-overallocation-of-infrastructure"></a>Vermeiden der überflüssigen Belegung von Infrastruktur
Nehmen wir an, Sie haben VM-Server bereitgestellt und mit genügend Ressourcen zur Abwicklung Ihrer Spitzenlastzeiten konfiguriert. Bei geringer Belastung könnten Sie potenziell für Infrastruktur bezahlen, die Sie nicht verwenden. Serverloses Computing löst das Problem der überflüssigen Belegung durch automatisches zentrales Hochskalieren oder Herunterskalieren, und Ihnen wird nur die Nutzung in Rechnung gestellt, wenn Ihre Funktion ausgeführt wird.

### <a name="stateless-logic"></a>Zustandslose Logik
Zustandslose Funktionen sind gute Kandidaten für serverloses Computing. Funktionsinstanzen werden bei Bedarf erstellt und zerstört. Wenn der Zustand erforderlich ist, kann er in einem zugeordneten Speicherdienst gespeichert werden.

### <a name="event-driven"></a>Ereignisgesteuert
Azure-Funktionen sind ereignisgesteuert und werden nur als Reaktion auf ein Ereignis ausgeführt, wie z.B. der Empfang einer HTTP-Anforderung oder das Hinzufügen einer Nachricht zu einer Warteschlange. Die Konfiguration von Azure-Funktionen vereinfacht Ihre Codebasis bedeutend, weil Sie die Quelle der Daten (Trigger/Eingabebindung) und das Ziel (Ausgabebindung) deklarieren. Sie müssen keinen Code zur Überwachung von Warteschlangen, Blobs, Hubs usw. schreiben. Sie konzentrieren sich ausschließlich auf die Geschäftslogik.

## <a name="when-do-you-not-use-serverless-compute"></a>Wann verwenden Sie serverloses Computing nicht?
Serverloses Computing ist nicht immer die geeignete Lösung für das Hosten Ihrer Geschäftslogik. Hier werden einige Merkmale von Azure-Funktionen aufgeführt, die Ihre Entscheidung zum Hosten Ihrer Dienste im serverlosen Computing beeinflussen könnten. 

### <a name="execution-time"></a>Ausführungszeit
Standardmäßig beträgt das Zeitlimit von Azure-Funktionen 5 Minuten. Dies kann auf ein Maximum von 10 Minuten konfiguriert werden. Wenn die Funktion mehr als 10 Minuten zur Ausführung benötigt, können Sie sie auf einem virtuellen Computer hosten. Wenn Ihr Dienst darüber hinaus über eine HTTP-Anforderung initiiert wird, und Sie diesen Wert als HTTP-Antwort erwarten, wird das Timeout weiter auf 2,5 Minuten beschränkt.

### <a name="execution-frequency"></a>Ausführungshäufigkeit
Das zweite Merkmal ist die Ausführungshäufigkeit. Wenn Sie erwarten, dass Ihre Funktion fortlaufend von mehreren Clients ausgeführt wird, wäre es ratsam, die Nutzung zu schätzen und die Kosten für das Verwenden von Azure-Funktionen entsprechend zu berechnen. Es könnte durchaus kostengünstiger sein, Ihren Dienst auf einem virtuellen Computer zu hosten.

Hinsichtlich der Skalierung kann bei bis zu 200 Instanzen insgesamt nur alle 10 Sekunden eine Funktions-App-Instanz erstellt werden. Denken Sie daran, dass jede Instanz mehrere gleichzeitige Ausführungen leisten kann; es gibt also kein Limit für den Datenverkehr, den eine einzelne Instanz verarbeiten kann. Weil verschiedene Arten von Triggern unterschiedliche Anforderungen an die Skalierung haben, untersuchen Sie den Trigger Ihrer Wahl, und machen Sie seine Grenzen ausfindig.
