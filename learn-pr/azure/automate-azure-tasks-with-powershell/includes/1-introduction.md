## <a name="motivation"></a>Motivation
Das Erstellen von Verwaltungsskripts ist eine leistungsstarke Möglichkeit, Ihren Workflow optimieren, können Sie allgemeine, repetative Aufgaben automatisieren und nachdem ein Skript überprüft wurde, wird es gleichbleibend, wahrscheinlich geringeren ausgeführt.

Angenommen Sie, Sie in einem Unternehmen arbeiten, die Azure Virtual Machines (VMs) verwendet, um Ihre Software (Customer Relationship Management, CRM) zu testen. Die virtuellen Computer werden aus Images erstellt, die ein Web-Front-End eines Webdiensts enthalten, die Geschäftslogik und einer SQL-Datenbank implementiert.

Wurde verfügen mehrere Runden von Tests auf einem einzelnen virtuellen Computer jedoch noticed, die Änderungen in der Datenbank ausführen und Konfigurationsdateien, können zu inkonsistente Ergebnissen führen. Im ersten Fall erstellt ein Fehler einen Telefonanruf-Datensatz mit keine entsprechenden Kunden in der Datenbank. Der verwaiste Datensatz verursacht nachfolgende Integrationstests fehlschlagen, auch wenn der Fehler behoben wurde. Sie planen, dieses Problem zu lösen, mit einer neuen VM-Bereitstellung für jeden Test-Zyklus. Möchten Sie das Setup der VM-Erstellung zu automatisieren, da es viele Male pro Woche ausgeführt wird. 

Hier sehen Sie, wie Sie Azure-Ressourcen mithilfe von Azure PowerShell verwalten. Sie verwenden Azure PowerShell interaktiv für einmalige Aufgaben und Skripts schreiben, um wiederholte Aufgaben zu automatisieren. 

## <a name="learning-objectives"></a>Lernziele
> [!div class="checklist"]
> * Entscheiden Sie, ob Azure PowerShell das richtige Tool für Ihre Azure-Administrationsaufgaben ist.
> * Installieren Sie Azure PowerShell unter Linux, MacOS und Windows
> * Verbinden Sie mit einem Azure-Abonnement mithilfe von Azure PowerShell
> * Erstellen Sie Azure-Ressourcen mithilfe von Azure PowerShell

## <a name="prerequisites"></a>Voraussetzungen
- Erleben Sie mit der eine Befehlszeilenschnittstelle, z.B. PowerShell oder Bash
- Kenntnisse der grundlegenden Azure-Konzepten wie Ressourcengruppen und virtuellen Computern
- Erfahrungen von Azure-Ressourcen über das Azure-Portal
