Nehmen wir an, Sie arbeiten für ein Lagerhausunternehmen, das seine IT in die Cloud verlagert. Derzeit verwenden Sie eine hybridumgebung, bestehend aus einem lokalen Windows Server, Azure Virtual Machines (VMs) und Azure Active Directory. Ihr Unternehmen hat eine interne, benutzerdefinierte B2B-Infrastruktur (Business-to-Business) entwickelt, die eine sichere Auftragsverwaltung mit Ihren Lieferanten unterstützt. Einige Ihrer Lieferanten verwenden Linux-Server, und Sie betreiben mehrere Linux-Server in Azure, um diese Lieferanten zu unterstützen.

Ihre Sicherheitsrichtlinien schreiben vor, dass Daten mit Ihren eigenen Verschlüsselungsschlüsseln verschlüsselt werden müssen, und dass Ihr Unternehmen für die Verwaltung dieser Schlüssel zuständig ist.

Ihr Administratorteam setzt bereits PowerShell für die Verwaltung der lokalen Server ein. Sie werden bereitstellen und Testen viele Azure-VMs und Azure Resource Manager-Vorlagen verwenden, um diesen Prozess automatisieren möchten.

Hier werfen wir einen Blick auf die Schutzarten, die für VM-Datenträger verfügbar sind, damit Sie entscheiden können, ob Azure Disk Encryption (ADE) die beste Wahl für ein bestimmtes Szenario ist. Wir dann ADE auf vorhandene VM-Datenträger aktivieren, und Verwenden von Vorlagen zum ADE für neue VM-Bereitstellungen zu aktivieren.


## <a name="learning-objectives"></a>Lernziele

Aufgaben in diesem Modul:

- Bestimmen der optimalen Verschlüsselungsmethode für Ihre VM
- Verschlüsseln vorhandener VM-Datenträger mithilfe des Azure-Portals
- Verschlüsseln vorhandener VM-Datenträger mit PowerShell
- Ändern Sie Azure Resource Manager-Vorlagen zum Automatisieren von datenträgerverschlüsselung auf neuen Computern
