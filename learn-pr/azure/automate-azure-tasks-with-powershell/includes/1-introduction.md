Das Erstellen von Verwaltungsskripts ist eine leistungsstarke Möglichkeit, Ihren Workflow zu optimieren. Sie können allgemeine, sich wiederholende Aufgaben automatisieren, und nachdem ein Skript überprüft wurde, wird es konsistent ausgeführt, sodass wahrscheinlich weniger Fehler auftreten.

Angenommen, Sie arbeiten in einem Unternehmen, das mit Azure Virtual Machines (VMs) die CRM-Software (Customer Relationship Management) testet. Die VMs werden aus Images erstellt, die ein Web-Front-End, einen Webdienst, der die Geschäftslogik implementiert, und eine SQL-Datenbank enthalten.

Sie haben mehrere Testrunden auf einer VM ausgeführt, jedoch festgestellt, dass Änderungen an Datenbank- und Konfigurationsdateien zu inkonsistenten Ergebnissen führen können. In einem Fall wurde durch einen Fehler ein Datensatz für einen Telefonanruf ohne entsprechenden Kunden in der Datenbank erstellt. Durch den verwaisten Datensatz sind nachfolgende Integrationstests fehlgeschlagen, auch nachdem der Fehler behoben wurde. Sie planen, dieses Problem mit einer neuen VM-Bereitstellung für jeden Testzyklus zu lösen. Sie möchten das Setup der VM-Erstellung automatisieren, da es viele Male pro Woche ausgeführt wird. 

Hier sehen Sie, wie die Azure-Ressourcen mithilfe von Azure PowerShell verwaltet werden. Sie verwenden Azure PowerShell interaktiv für einmalige Aufgaben und schreiben Skripts, um sich wiederholende Aufgaben zu automatisieren. 

## <a name="learning-objectives"></a>Lernziele
In diesem Modul lernen Sie Folgendes:

- Entscheiden, ob Azure PowerShell das richtige Tool für Ihre Azure-Verwaltungsaufgaben ist
- Installieren Sie Azure PowerShell unter Linux, MacOS und/oder Windows
- Verbinden mit einem Azure-Abonnement über Azure PowerShell
- Erstellen von Azure-Ressourcen mit Azure PowerShell

## <a name="prerequisites"></a>Voraussetzungen

- Einführung in eine Befehlszeilenschnittstelle wie PowerShell oder Bash
- Kenntnisse der grundlegenden Azure-Konzepte wie Ressourcengruppen und virtuelle Computer
- Erfahrung beim Verwalten von Azure-Ressourcen über das Azure-Portal
