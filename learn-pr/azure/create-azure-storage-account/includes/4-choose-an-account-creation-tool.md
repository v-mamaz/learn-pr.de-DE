Es gibt mehrere Tools, die ein Speicherkonto erstellen. In der Regel hängt Ihre Entscheidung davon ab, ob Sie eine grafische Benutzeroberfläche (GUI) möchten und Automatisierung benötigen.

## <a name="available-tools"></a>Verfügbare Tools

Zu den verfügbaren Tools zählen:

- Portal
- Befehlszeilenschnittstelle (CLI)
- Azure PowerShell
- Verwaltung einer Clientbibliothek

Das Portal bietet eine GUI mit QuickInfos für jede Einstellung. Dadurch ist es einfach zu bedienen und bietet hilfreiche Informationen zu den Optionen.

Die anderen Tools unterstützen alle die Automatisierung. Mit der CLI und Azure PowerShell können Sie Skripts schreiben, während die Verwaltungsbibliotheken das Integrieren einer Erstellung in eine Client-App ermöglichen.

## <a name="how-to-choose-a-tool"></a>Auswählen eines Tools

Speicherkonten basieren normalerweise auf einer Analyse Ihrer Daten, sodass sie tendenziell relativ stabil sind. Dies bedeutet, dass die Erstellung von Speicherkonten in der Regel am Anfang eines Projekts in einem einmaligen Vorgang erfolgt. Das Portal ist für einmalige Aktivitäten die gängigste Wahl.

In den seltenen Fällen, in denen Sie Automatisierung benötigen, müssen Sie sich zwischen einer programmgesteuerten API und einer Skriptlösung entscheiden. In der Regel sind Skripts für das Erstellen schneller und in Sachen Verwaltung weniger arbeitsaufwendig, da keine integrierte Entwicklungsumgebung (IDE), NuGet-Pakete oder Buildschritte erforderlich sind. Wenn Sie eine vorhandene Clientanwendung haben, können die Verwaltungsbibliotheken eine attraktive Möglichkeit sein. Andernfalls sind Skripts wahrscheinlich die bessere Option.