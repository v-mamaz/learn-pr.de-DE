Die bereits thematisierten Speicherkontoeinstellungen gelten für die Datendienste in dem jeweiligen Konto. Hier besprechen wir die drei Einstellungen, die für das Konto selbst und nicht auf die im Konto gespeicherten Daten gelten:

- Name
- Bereitstellungsmodell
- Kontoart

Diese Einstellungen beeinflussen, wie Sie Ihr Konto und die Kosten für die darin enthaltenen Dienste verwalten.

## <a name="name"></a>Name

Jedes Speicherkonto verfügt über einen Namen. Der Name muss global eindeutig sein, verwenden Sie nur Kleinbuchstaben und Ziffern und zwischen 3 und 24 Zeichen lang sein.

## <a name="deployment-model"></a>Bereitstellungsmodell

Azure verwendet _Bereitstellungsmodelle_, um Ihre Ressourcen zu organisieren. Sie definieren die API, die Sie verwenden, um diese Ressourcen zu erstellen, zu konfigurieren und zu verwalten. Azure stellt zwei Bereitstellungsmodelle bereit:

- **Ressourcen-Manager**: das aktuelle Modell, das die Azure Resource Manager-API verwendet.
- **Klassische**: ein legacy-Angebot, die die Azure Service Management-API verwendet.

Die Entscheidung der Wahl eines wird in der Regel einfach, da die meisten Azure-Ressourcen nur mit Resource Manager funktioniert. Allerdings unterstützt Speicherkonten, virtuelle Computer und virtuelle Netzwerke, damit Sie eine auswählen müssen, wenn Sie Ihr Storage-Konto erstellen.

Ein wichtiger Unterschied besteht in der Unterstützung von Gruppierungen. Resource Manager-Modell fügt das Konzept einer _Ressourcengruppe_, die nicht in das klassische Modell verfügbar ist. Mithilfe einer Ressourcengruppe können Sie eine Sammlung von Ressourcen als einzelne Einheit bereitstellen und verwalten.

Microsoft empfiehlt die Verwendung von **Resource Manager** für alle neuen Ressourcen.

## <a name="account-kind"></a>Kontoart

Die _Art_ des Speicherkontos stellt eine Reihe von Richtlinien dar, die bestimmen, welche Datendienste Sie zu dem Konto hinzufügen können und wie hoch die Preise für diese Dienste sind. Es gibt drei Arten von Speicherkonten:

- **StorageV2 (universelle Version 2):** das aktuelle Speicherkonto, das sämtliche Speichertypen und die neusten Features unterstützt
- **Storage (universelle Version 1):** ein veraltetes Speicherkonto, das zwar alle Speichertypen, aber ggf. nicht alle Features unterstützt
- **BLOB-Speicher**: eine ältere Art, die nur blockblobs und anfügeblobs

Microsoft empfiehlt die Verwendung der **General Purpose v2** Option für neue Speicherkonten.

In Einzelfällen bietet sich allerdings die Verwendung der anderen Speicherkonten an. Beispielsweise ist die Preise für Transaktionen weiter unten in der Allgemein v1, sodass Sie leicht Kosten zu reduzieren, wenn die typische arbeitsauslastung entspricht.

## <a name="summary"></a>Zusammenfassung

Generell wird empfohlen, das Bereitstellungsmodell **Ressourcen-Manager** und die Kontoart **StorageV2 (universelle Version 2)** für sämtliche Speicherkonten zu verwenden. Die anderen Optionen sind allerdings in erster Linie weiter verfügbar, damit bereits vorhandene Ressourcen weiter verwendet werden können. Für neue Ressourcen gibt es einige Gründe für den Einsatz von den anderen Optionen.