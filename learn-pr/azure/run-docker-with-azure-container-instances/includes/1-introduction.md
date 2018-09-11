Container entwickeln sich mehr und mehr zum bevorzugten Instrument für das Packen, Bereitstellen und Verwalten von Cloudanwendungen. Mit Azure Container Instances lassen sich Container in Azure besonders schnell und einfach ausführen, ohne dass Sie dazu virtuelle Computer verwalten oder einen übergeordneten Dienst einführen müssen.

Azure Container Instances ist eine großartige Lösung für jedes Szenario, das für die Verwendung isolierter Container geeignet ist. Hierzu zählen unter anderem einfache Anwendungen, Aufgabenautomatisierung und Erstellungsaufträge. Für Szenarien, die eine umfassende Containerorchestrierung erfordern (etwa für die containerübergreifende Dienstermittlung, automatische Skalierung und für koordinierte Anwendungsupgrades), empfehlen wir Azure Kubernetes Service (AKS).

Azure Container Instances bietet die folgenden Vorteile:

- **Schneller Start:** Azure Container Instances kann Container in Azure innerhalb weniger Sekunden starten.
- **Sekundengenaue Abrechnung:** Kosten fallen nur während der Containerausführung an.
- **Sicherheit auf Hypervisorebene**: Azure Container Instances gewährleistet, dass Ihre Anwendung in einem Container isoliert ist – genau wie bei einem virtuellen Computer.
- **Benutzerdefinierte Größe**: Azure Container Instances ermöglicht exakte Angaben für CPU-Kerne und Arbeitsspeicher und bietet dadurch eine optimale Auslastung.
- **Beständiger Speicher**: Dank der Möglichkeit zur direkten Einbindung von Azure Files-Freigaben können Sie mit Azure Container Instances den Zustand abrufen und speichern.
- **Linux und Windows**: Azure Container Instances kann sowohl Windows- als auch Linux-Container mit der gleichen API planen.

## <a name="learning-objectives"></a>Lernziele  

In diesem Modul wird Folgendes thematisiert:

- Ausführen eines Containers in Azure Container Instances.
- Steuern des Neustartverhaltens von Containern.
- Verwenden von Umgebungsvariablen in Ihren Containern.
- Anfügen von Datenvolumes an Azure Container Instances.
- Informationen zur Problembehandlung in Azure Container Instances.
