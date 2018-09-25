Nehmen wir an, Sie arbeiten für ein Lagerhausunternehmen, das seine IT in die Cloud verlagert. Aktuell verwenden Sie eine Hybridumgebung, die aus lokalen Windows-Servern, Azure Virtual Machines (VMs) und Azure Active Directory besteht. Ihr Unternehmen hat eine interne, individuelle B2B-Infrastruktur (Business-to-Business) entwickelt, die eine sichere Auftragsverwaltung mit Ihren Lieferanten unterstützt. Einige Ihrer Lieferanten verwenden Linux-Server, und Sie betreiben mehrere Linux-Server in Azure, um diese Lieferanten zu unterstützen.

Ihre Sicherheitsrichtlinien schreiben vor, dass Daten mit Ihren eigenen Verschlüsselungsschlüsseln verschlüsselt werden müssen, und dass Ihr Unternehmen für die Verwaltung dieser Schlüssel zuständig ist.

Ihr Administratorteam setzt bereits PowerShell für die Verwaltung der lokalen Server ein. Sie werden viele Azure-VMs bereitstellen und testen und haben die Absicht, Azure Resource Manager-Vorlagen einzusetzen, um diesen Vorgang zu automatisieren.

Hier werfen wir einen Blick auf die Schutzarten, die für VM-Datenträger verfügbar sind, damit Sie entscheiden können, ob Azure Disk Encryption (ADE) die beste Wahl für ein bestimmtes Szenario ist. Wir aktivieren anschließend ADE für vorhandene VM-Datenträger und verwenden Vorlagen, um ADE für neue VM-Bereitstellungen zu aktivieren.


## <a name="learning-objectives"></a>Lernziele

Aufgaben in diesem Modul:

- Bestimmen der optimalen Verschlüsselungsmethode für Ihre VM
- Verschlüsseln vorhandener VM-Datenträger mithilfe des Azure-Portals
- Verschlüsseln vorhandener VM-Datenträger mit PowerShell
- Bearbeiten von Azure Resource Manager-Vorlagen, um die Datenträgerverschlüsselung für neue VMs zu automatisieren
