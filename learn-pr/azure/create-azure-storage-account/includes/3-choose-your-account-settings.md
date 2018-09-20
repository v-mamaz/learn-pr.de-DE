Die bereits thematisierten Speicherkontoeinstellungen gelten für die Datendienste in dem jeweiligen Konto. Nachfolgend werden die drei Einstellungen thematisiert, die für das Konto an sich und nicht für die darin gespeicherten Daten gelten:

- Name
- Bereitstellungsmodell
- Kontoart

Diese Einstellungen haben Einfluss darauf, wie Sie Ihr Konto und die Kosten für die darin enthaltenen Dienste verwalten.

## <a name="name"></a>Name

Jedes Speicherkonto verfügt über einen Namen. Der Name muss in Azure global eindeutig und zwischen 3 und 24 Zeichen lang sein. Außerdem dürfen nur Kleinbuchstaben und Ziffern verwendet werden.

## <a name="deployment-model"></a>Bereitstellungsmodell

Azure verwendet _Bereitstellungsmodelle_, um Ihre Ressourcen zu organisieren. Das Modell definiert die API, die Sie verwenden, um diese Ressourcen zu erstellen, zu konfigurieren und zu verwalten. Azure stellt zwei Bereitstellungsmodelle bereit:

- **Resource Manager:** das aktuelle Modell, das die Azure Resource Manager-API verwendet
- **Klassisch:** ein älteres Modell, das die Azure-Dienstverwaltungs-API verwendet

Die Entscheidung für eins der beiden Modelle fällt in der Regel leicht, da die meisten Azure-Ressourcen nur mit Resource Manager funktionieren. Speicherkonten, virtuelle Computer und virtuelle Netzwerke unterstützen jedoch beide Modelle. Beim Erstellen eines Speicherkontos müssen Sie sich daher für eines der beiden entscheiden.

Ein wichtiger Unterschied zwischen den Modellen besteht in der Unterstützung von Gruppierungen. Mit dem Resource Manager-Modell kann das Konzept einer _Ressourcengruppe_ verwendet werden, das im klassischen Modell nicht verfügbar ist. Mithilfe einer Ressourcengruppe können Sie eine Sammlung von Ressourcen als einzelne Einheit bereitstellen und verwalten.

Microsoft empfiehlt die Verwendung von **Resource Manager** für alle neuen Ressourcen.

## <a name="account-kind"></a>Kontoart

Die _Art_ des Speicherkontos stellt eine Reihe von Richtlinien dar, die bestimmen, welche Datendienste Sie zu dem Konto hinzufügen können und wie hoch die Preise für diese Dienste sind. Es gibt drei Arten von Speicherkonten:

- **StorageV2 (universelle Version 2):** das aktuelle Speicherkonto, das sämtliche Speichertypen und die neusten Features unterstützt
- **Storage (general purpose v1)** (Speicher (universell, Version 1)): ein veraltetes Speicherkonto, das zwar alle Speichertypen, aber ggf. nicht alle Features unterstützt
- **Blobspeicher:** ein veraltetes Speicherkonto, das nur Blockblobs und Anfügeblobs zulässt

Microsoft empfiehlt bei neuen Speicherkonten die Verwendung von **General-purpose v2** (universell, Version 2).

In Einzelfällen bietet sich allerdings die Verwendung der anderen Speicherkonten an. Beispielsweise sind die Preise für Transaktionen mit der universellen Version 1 geringer, wodurch Sie Kosten sparen können, wenn Ihre Workload mit dieser Version kompatibel ist.

Generell wird empfohlen, das Bereitstellungsmodell **Resource Manager** und die Kontoart **StorageV2 (universelle Version 2)** für sämtliche Speicherkonten zu verwenden. Die anderen Optionen sind allerdings in erster Linie weiter verfügbar, damit bereits vorhandene Ressourcen weiter verwendet werden können. Für neue Ressourcen gibt es wenige Gründe, die für die Verwendung der älteren Optionen sprechen.