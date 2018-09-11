Die bereits thematisierten Speicherkontoeinstellungen gelten für die Datendienste in dem jeweiligen Konto. Nachfolgend werden die drei Einstellungen thematisiert, die für das Konto an sich und nicht für die darin gespeicherten Daten gelten:

- Name
- Bereitstellungsmodell
- Kontoart

Diese Einstellungen haben Einfluss darauf, wie Sie Ihr Konto und die Kosten für die darin enthaltenen Dienste verwalten.

## <a name="name"></a>Name

Jedes Speicherkonto verfügt über einen Namen. Der Name muss global eindeutig sein. Er muss zwischen 3 und 24 Zeichen lang sein und darf nur Zahlen und Kleinbuchstaben enthalten.

## <a name="deployment-model"></a>Bereitstellungsmodell

Azure verwendet _Bereitstellungsmodelle_, um Ihre Ressourcen zu organisieren. Sie definieren die API, die Sie verwenden, um diese Ressourcen zu erstellen, zu konfigurieren und zu verwalten. Azure stellt zwei Bereitstellungsmodelle bereit:

- **Ressourcen-Manager:** das aktuelle Modell, das die API des Azure Resource Managers (ARM) verwendet
- **Klassisch:** ein älteres Modell, das die API von Azure Service Management (ASM) verwendet

Die Entscheidung für eins der beiden Modelle fällt in der Regel leicht, da die meisten Azure-Ressourcen nur mit dem Ressourcen-Manager funktionieren. Allerdings unterstützen virtuelle Computer, Speicherkonten und virtuelle Netzwerke beide Modelle. Aus diesem Grund müssen Sie sich für eins entscheiden, wenn Sie Ihr Speicherkonto erstellen.

Ein wichtiger Unterschied besteht in der Unterstützung von Gruppierungen. Das Ressourcen-Manager-Modell fügt das Konzept einer _Ressourcengruppe_ hinzu, die im klassischen Modell nicht verfügbar ist. Mithilfe einer Ressourcengruppe können Sie eine Sammlung von Ressourcen als einzelne Einheit bereitstellen und verwalten.

Microsoft empfiehlt die Verwendung des Ressourcen-Managers für alle neuen Ressourcen.

## <a name="account-kind"></a>Kontoart

Die _Art_ des Speicherkontos stellt eine Reihe von Richtlinien dar, die bestimmen, welche Datendienste Sie zu dem Konto hinzufügen können und wie hoch die Preise für diese Dienste sind. Es gibt drei Arten von Speicherkonten:

- **StorageV2 (universelle Version 2):** das aktuelle Speicherkonto, das sämtliche Speichertypen und die neusten Features unterstützt
- **Storage (universelle Version 1):** ein veraltetes Speicherkonto, das zwar alle Speichertypen, aber ggf. nicht alle Features unterstützt
- **Blob Storage:** ein veraltetes Speicherkonto, das nur Blockblobs und Anfügeblobs zulässt

Microsoft empfiehlt bei neuen Speicherkonten die Verwendung der universellen Version 2.

In Einzelfällen bietet sich allerdings die Verwendung der anderen Speicherkonten an. Beispielsweise sind die Preise für Transaktionen mit der universellen Version 1 geringer, wodurch Sie Kosten sparen können, wenn Ihre Workload mit dieser Version kompatibel ist.

## <a name="summary"></a>Zusammenfassung

Generell wird empfohlen, das Bereitstellungsmodell **Ressourcen-Manager** und die Kontoart **StorageV2 (universelle Version 2)** für sämtliche Speicherkonten zu verwenden. Die anderen Optionen sind allerdings in erster Linie weiter verfügbar, damit bereits vorhandene Ressourcen weiter verwendet werden können. Für neue Ressourcen gibt es nur wenige Gründe, die für die Verwendung der älteren Optionen sprechen.