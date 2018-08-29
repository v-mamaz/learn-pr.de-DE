## <a name="motivation"></a>Motivation
Das Azure-Portal eignet sich hervorragend für die Ausführung einzelner Aufgaben und um Ihnen eine schnelle Übersicht über den Zustand Ihrer Ressourcen zu verschaffen. Aber in Verbindung mit Aufgaben, die täglich oder sogar stündlich wiederholt werden müssen, können Sie mithilfe der Befehlszeile und eines Satzes getesteter Befehle oder Skripts Ihre Arbeit unter Umständen noch schneller erledigen und Fehler vermeiden. 

Nehmen wir an, Sie arbeiten in einem Unternehmen, das Azure-Web-Apps entwickelt. Dabei handelt es sich um Anwendungen, die in Azure gehostet werden, mit allen Vorteilen der automatischen Konfiguration von Sicherheit, Lastenausgleich, Verwaltung usw. Derzeit testen Sie eine Web-App, die Umsatzprognosen basierend auf einer Reihe von Eingaben aus verschiedenen Datenbanken und anderen Datenquellen generiert. Ihre Entwickler verwenden Windows-, Linux- und Mac-Computer und setzen ein GitHub-Repository für tägliche Builds der Anwendungen ein. 

Im Rahmen der Tests möchten Sie die App-Leistung für verschiedene Datenquellen und verschiedene Arten von Datenverbindungen vergleichen. Sie haben bemerkt: Wenn Ihr Entwicklungsteam eine neue Testinstanz der App im Azure-Portal erstellt, verwendet es nicht immer genau dieselben Parameter. Sie möchten dieses Problem lösen, indem Sie für jeden App-Test eine Reihe von Standardbereitstellungsbefehlen verwenden, die bei Bedarf automatisiert werden können und auf allen Computern, die Ihr Softwareteam verwendet, auf dieselbe Weise funktionieren.

In diesem Modul sehen Sie, wie die Azure-Ressourcen mithilfe der Azure CLI verwaltet werden. 

## <a name="learning-objectives"></a>Lernziele
> [!div class="checklist"]
> * Sie können die Azure CLI auf Linux, macOS und Windows installieren.
> * Stellen Sie mit der Azure CLI eine Verbindung mit einem Azure-Abonnement her.
> * Erstellen Sie Azure-Ressourcen mit der Azure CLI.

## <a name="prerequisites"></a>Voraussetzungen
- Erfahrung mit einer Befehlszeilenschnittstelle wie PowerShell oder Bash
- Kenntnisse der grundlegenden Azure-Konzepte, z.B. Ressourcengruppen
- Erfahrung beim Verwalten von Azure-Ressourcen über das Azure-Portal

## <a name="expected-duration"></a>Erwartete Dauer

30 Minuten