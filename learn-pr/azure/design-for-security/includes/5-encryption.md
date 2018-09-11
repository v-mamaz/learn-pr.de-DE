Daten sind das wertvollste und unersetzlichste Gut eines Unternehmens, und Verschlüsselung dient als letzte und stärkste Schutzmaßnahme in einer mehrstufigen Sicherheitsstrategie. Als Gesundheitsdienstleister speichert Lamna Healthcare große Mengen an vertraulichen Daten. Vor Kurzem kam es zu einer Sicherheitsverletzung, wobei unverschlüsselte vertrauliche Daten von Patienten offengelegt wurden. Nun ist sich das Unternehmen dessen bewusst, dass seine Datenschutzfunktionen Lücken haben. Lamna Healthcare möchte verstehen, wie Verschlüsselung das Unternehmen und seine Patienten besser vor dieser Art von Incidents schützen kann. Hier betrachten wir, was Verschlüsselung ist, wie Daten verschlüsselt werden, und welche Verschlüsselungsmöglichkeiten in Azure verfügbar sind.

## <a name="what-is-encryption"></a>Was ist Verschlüsselung?

Verschlüsselung ist der Vorgang, Daten nicht lesbar und nicht verwendbar zu machen. Um verschlüsselte Daten zu verwenden oder zu lesen, müssen sie *entschlüsselt* werden. Dies erfordert einen geheimen Schlüssel. Es gibt zwei Arten von Verschlüsselung auf oberster Ebene: **Symmetrische** und **asymmetrische** Verschlüsselung.

Die symmetrische Verschlüsselung verwendet den gleichen Schlüssel zum Verschlüsseln und Entschlüsseln der Daten. Ziehen Sie eine Kennwort-Manager-Desktopanwendung in Betracht. Sie geben Ihre Passwörter ein, und diese werden mit Ihrem persönlichen Schlüssel verschlüsselt (Ihr Schlüssel wird oft von Ihrem Masterkennwort abgeleitet). Wenn die Daten abgerufen werden müssen, wird der gleiche Schlüssel verwendet, und die Daten werden entschlüsselt.

Die asymmetrische Verschlüsselung verwendet ein öffentlich-privates Schlüsselpaar. Beide Schlüssel können verschlüsseln, allerdings können sie nicht ihre eigenen verschlüsselten Daten entschlüsseln. Zum Entschlüsseln benötigen Sie das jeweils andere Schlüsselpaar. Die asymmetrische Verschlüsselung wird beispielsweise für TLS (in HTTPS) und Datensignatur verwendet.

Sowohl die symmetrische als auch die asymmetrische Verschlüsselung spielen eine Rolle bei der ordnungsgemäßen Sicherung von Daten. 

Bei der Verschlüsselung wird in der Regel zwischen zwei Optionen unterschieden: Verschlüsselung ruhender Daten und Verschlüsselung in Übertragung begriffener Daten.

### <a name="encryption-at-rest"></a>Verschlüsselung ruhender Daten

Ruhende Daten sind Daten, die auf einem physischen Medium gespeichert sind. Das sind beispielsweise Daten, die auf dem Datenträger eines Servers, in einer Datenbank oder in einem Speicherkonto gespeichert sind. Unabhängig vom Speichermechanismus stellt die Verschlüsselung ruhender Daten sicher, dass die gespeicherten Daten ohne die zum Entschlüsseln erforderlichen Schlüssel und Geheimnisse nicht lesbar sind. Wenn ein Angreifer nun eine Festplatte mit verschlüsselten Daten erhält, aber keinen Zugriff auf die Verschlüsselungsschlüssel hat, kann der Angreifer die Daten nicht ohne Weiteres kompromittieren. In einem derartigen Szenario müsste ein Angreifer versuchen, die verschlüsselten Daten anzugreifen, was jedoch deutlich komplexer und ressourcenaufwändiger als bei unverschlüsselten Daten auf einer Festplatte ist.

Die tatsächlich verschlüsselten Daten können in Hinblick auf Inhalt, Verwendung und Bedeutung für das Unternehmen variieren. Dies können geschäftskritische Finanzinformationen, geistiges Eigentum des Unternehmens, persönliche Kunden- oder Mitarbeiterdaten des Unternehmens und sogar die Schlüssel und Geheimnisse sein, die für die Datenverschlüsselung verwendet werden.

![Verschlüsselung ruhender Daten](../media-draft/encryption-at-rest.png)

### <a name="encryption-in-transit"></a>Verschlüsselung in Übertragung begriffener Daten

In Übertragung begriffene Daten sind Daten, die sich aktiv von einem Ort zu einem anderen bewegen, z.B. über das Internet oder über ein privates Netzwerk. Die sichere Übertragung kann durch das Verschlüsseln der Daten vor dem Senden über ein Netzwerk oder durch das Einrichten eines sicheren Kanals zum Übertragen unverschlüsselter Daten zwischen zwei Systemen erfolgen. Das Verschlüsseln von Daten, die übertragen werden, schützt die Daten vor externen Beobachtern und bietet einen Mechanismus zur Datenübertragung bei gleichzeitiger Einschränkung des Offenlegungsrisikos. 

![Verschlüsselung in Übertragung begriffener Daten](../media-draft/encryption-in-transit.png)

## <a name="identify-and-classify-data"></a>Identifizieren und Klassifizieren von Daten

Kommen wir noch einmal auf das Problem zurück, das Lamna Healthcare lösen möchte. Es kam bereits zu Incidents, bei denen vertrauliche Daten offengelegt wurden. Das heißt, es gibt eine Diskrepanz zwischen dem, was verschlüsselt wird, und dem, was verschlüsselt werden soll. Zunächst müssen die Typen von Daten identifiziert und klassifiziert werden, die gespeichert werden. Diese müssen den geschäftlichen und gesetzlichen Anforderungen an die Datenspeicherung entsprechen. Es ist vorteilhaft, diese Daten bezüglich den Auswirkungen der Offenlegung für das Unternehmen, die Kunden oder die Partner zu klassifizieren. Eine exemplarische Klassifizierung könnte wie folgt aussehen:

|Datenklassifizierung|Erklärung|
|---|---|
|Eingeschränkt|Daten, die als „Eingeschränkt“ eingestuft werden, stellen ein erhebliches Risiko dar, wenn sie offengelegt, geändert oder gelöscht werden. Für diese Daten ist ein hohes Maß an Schutz erforderlich. |
|Privat| Daten, die als „Privat“ eingestuft werden, stellen ein mittleres Risiko dar, wenn sie offengelegt, geändert oder gelöscht werden. Für diese Daten ist ein angemessener Schutz erforderlich. Daten, die nicht als „Eingeschränkt“ oder „Öffentlich“ eingestuft werden, werden als „Privat“ klassifiziert.  |
|Öffentlich| Daten, die als „Öffentlich“ eingestuft werden, stellen kein Risiko dar, wenn sie offengelegt, geändert oder gelöscht werden. Sie erfordern keine Schutzmaßnahmen. |

Durch eine Bestandsaufnahme der gespeicherten Datentypen können sie sich ein besseres Bild davon machen, wo vertrauliche Daten gespeichert werden können, und wo bestehende Verschlüsselung angewendet werden kann.

Ein umfassendes Verständnis der gesetzlichen und geschäftlichen Anforderungen, die für Daten gelten, die eine Organisation speichert, ist ebenfalls wichtig. Die gesetzlichen Anforderungen, die eine Organisation erfüllen muss, bestimmen oft den Großteil der Datenverschlüsselungsanforderungen. Im Fall von Lamna Healthcare werden vertrauliche Daten gespeichert, die unter den Health Insurance Portability and Accountability Act (HIPAA) fallen, der Vorschriften für den Umgang und die Speicherung von Patientendaten enthält. Für andere Branchen gelten möglicherweise andere gesetzliche Richtlinien. Ein Finanzinstitut kann Kontoinformationen speichern, die den PCI-Standards (Payment Card Industry) entsprechen. Eine in der EU tätige Organisation unterliegt der Datenschutz-Grundverordnung (DSGVO), die den Umgang mit personenbezogenen Daten in der EU bestimmt. Geschäftsanforderungen können auch vorschreiben, dass Daten mit Wettbewerbsinformationen, die das Unternehmen einem finanziellen Risiko aussetzen könnten, verschlüsselt werden müssen.

Sobald Sie die Daten klassifiziert und Ihre Anforderungen definiert haben, können Sie die Vorteile verschiedener Tools und Technologien nutzen, um die Verschlüsselung in Ihrer Architektur zu implementieren und durchzusetzen.

## <a name="encryption-on-azure"></a>Verschlüsselung in Azure

Betrachten wir einige Möglichkeiten, wie Sie mit Azure Daten dienstübergreifend verschlüsseln können.

### <a name="encrypting-raw-storage"></a>Verschlüsseln von Speicher

Die Azure-Speicherdienstverschlüsselung für ruhende Daten unterstützt Sie dabei, Ihre Daten zu schützen, um die Sicherheits- und Complianceanforderungen Ihrer Organisation zu erfüllen. Mit dieser Funktion verschlüsselt die Azure-Speicherplattform Ihre Daten automatisch vor dem Ablegen in Azure Managed Disks, Azure Blob Storage, Azure Files oder Azure Queue Storage und entschlüsselt sie vor dem Abrufen. Die Verarbeitung der Ver- und Entschlüsselung, der Verschlüsselung ruhender Daten und der Speicherdienstverschlüsselung ist für Anwendungen, die die Dienste verwenden, transparent.

Für Lamna Healthcare bedeutet das, dass beim Verwenden von Diensten, die die Speicherdienstverschlüsselung unterstützen, Daten auf dem physischen Speichermedium verschlüsselt werden. Im höchst unwahrscheinlichen Fall, dass ein Zugriff auf den physischen Datenträger erfolgt, sind die Daten nicht lesbar, weil sie beim Schreiben auf den physischen Datenträger verschlüsselt wurden.

### <a name="encrypting-virtual-machines"></a>Verschlüsseln virtueller Computer

Die Speicherdienstverschlüsselung bietet einen niedrigen Verschlüsselungsschutz für Daten, die auf einen physischen Datenträger geschrieben werden. Wie schützen Sie also die virtuellen Festplatten (VHDs) von virtuellen Computern (VMs)? Stellen Sie sich vor, ein bösartiger Angreifer erhält Zugriff auf Ihr Azure-Abonnement und filtert die VHDs Ihrer virtuellen Computer: Wie können Sie sicherstellen, dass er nicht auf die VHD-Daten zugreifen kann?

Azure Disk Encryption (ADE) ist eine Funktion, mit der Sie die Datenträger von Windows- und Linux-IaaS-VMs verschlüsseln können. ADE verwendet die Branchenstandardfunktion BitLocker von Windows und die Funktion DM-Crypt von Linux, um Volumeverschlüsselung für das Betriebssystem und Datenträger bereitzustellen. Die Lösung ist in Azure Key Vault integriert, damit Sie die Verschlüsselungsschlüssel und Geheimnisse für die Datenträgerverschlüsselung steuern und verwalten können. Sie können mit verwalteten Dienstidentitäten auf den Schlüsseltresor zugreifen.

 Lamna Healthcare kann ADE auf die VMs anwenden, um sicherzustellen, dass alle auf VHDs gespeicherten Daten gemäß den Geschäfts- und Complianceanforderungen gesichert sind. Da Startdatenträger auch verschlüsselt sind, kann die Nutzung kontrolliert und überprüft werden.

### <a name="encrypting-databases"></a>Verschlüsseln von Datenbanken

Lamna Healthcare verfügt über mehrere Datenbanken, in denen Daten gespeichert werden, die zusätzlichen Schutz benötigen. Das Unternehmen hat viele Datenbanken in Azure SQL-Datenbank verschoben, und möchte sicherstellen, dass seine Daten innerhalb der Datenbank verschlüsselt sind. Wenn Datendateien, Protokolldateien oder Sicherungsdateien gestohlen werden, soll sichergestellt werden, dass sie ohne Zugriff auf die Verschlüsselungscodes nicht lesbar sind.

Transparent Data Encryption (TDE) trägt zum Schutz von Azure SQL-Datenbank und Azure Data Warehouse vor der Bedrohung durch schädliche Aktivitäten bei. TDE ver- und entschlüsselt die Datenbank, die zugehörigen Sicherungen und die Transaktionsprotokolldateien im Ruhezustand in Echtzeit, ohne dass Änderungen an der Anwendung erforderlich sind. TDE ist standardmäßig für alle neu bereitgestellten Azure SQL-Datenbanken aktiviert.

TDE verschlüsselt die Speicherung einer gesamten Datenbank, indem ein symmetrischer Schlüssel verwendet wird, der als Datenbankverschlüsselungsschlüssel bezeichnet wird. Standardmäßig stellt Azure einen eindeutigen Verschlüsselungsschlüssel pro logische SQL Server-Instanz zur Verfügung und verarbeitet alle Details. Bring Your Own Key wird ebenfalls mit Schlüsseln unterstützt, die in Azure Key Vault gespeichert sind.

Da TDE standardmäßig aktiviert ist, kann Lamna Healthcare sicher sein, dass die richtigen Schutzmaßnahmen für die in den Organisationsdatenbanken gespeicherten Daten gelten.

### <a name="encrypting-secrets"></a>Verschlüsseln von Geheimnissen

Sie haben gesehen, dass die Verschlüsselungsdienste Schlüssel verwenden, um Daten zu verschlüsseln und zu entschlüsseln. Wie können Sie also sicherstellen, dass die Schlüssel selbst sicher sind? Lamna Healthcare hat möglicherweise auch Kennwörter, Verbindungszeichenfolgen und andere vertrauliche Informationen, die sicher gespeichert werden müssen.

Azure Key Vault ist ein Clouddienst, der als sicherer Geheimnisspeicher fungiert. Mit Key Vault können Sie mehrere sichere Container (sogenannte Tresore) erstellen. Diese Tresore basieren auf Hardwaresicherheitsmodulen (HSMs). Tresore zentralisieren die Speicherung von Anwendungsgeheimnissen und verringern so die Gefahr, dass Sicherheitsinformationen verloren gehen. Darüber hinaus steuern und protokollieren Key Vault-Instanzen den Zugriff auf alle darin gespeicherten Daten. Azure Key Vault kann TLS-Zertifikate (Transport Layer Security) anfordern und erneuern. Außerdem stellt die Lösung Funktionen bereit, die für eine zuverlässige Zertifikatlebenszyklus-Verwaltungslösung benötigt werden. Key Vault ist für die Unterstützung jeder Art von Geheimnissen konzipiert. Das umfasst Kennwörter, Anmeldeinformationen für Datenbanken, API-Schlüssel und Zertifikate.

Da Azure AD-Identitäten Zugriff auf Azure Key Vault-Geheimnisse erhalten können, erhalten Anwendungen, für die die verwaltete Dienstidentität aktiviert ist, automatisch und nahtlos die benötigten Geheimnisse.

Lamna Healthcare kann Key Vault für die Speicherung aller vertraulichen Anwendungsinformationen verwenden, einschließlich der TLS-Zertifikate zur sicheren Kommunikation zwischen Systemen.

## <a name="encryption-at-lamna-healthcare"></a>Verschlüsseln bei Lamna Healthcare

Lamna Healthcare hat den Identifizierungs- und Klassifizierungsprozess für alle gespeicherten Daten durchlaufen. Die Organisation hat diese Klassifizierungen mit den gesetzlichen und geschäftlichen Anforderungen abgeglichen und festgestellt, dass sie weitaus mehr Daten hat, die verschlüsselt werden müssen. Es wurden alle VMs verschlüsselt, die vertrauliche Daten beinhalten. Außerdem verschlüsselt Lamna Healthcare alle vertraulichen Patienteninformationen, die in Blobspeichern gespeichert werden. TDE ist für alle Datenbanken aktiviert, sodass die relationalen Datenbanken die Verschlüsselungsanforderungen unabhängig von der Klassifizierung erfüllen. Lamna Healthcare hat die gesamte Organisation berücksichtigt und verwendet Key Vault, um alle Zertifikate und Anmeldeinformationen zu speichern, die Anwendungen für den Betrieb benötigen.

## <a name="summary"></a>Zusammenfassung

Verschlüsselung ist oft die letzte Sicherheitsstufe bei Angriffen und ein wichtiger Teil eines mehrstufigen Ansatzes zum Schutz Ihrer Architektur. Azure bietet integrierte Funktionen und Dienste zum Verschlüsseln und zum Schutz von Daten vor unbeabsichtigter Offenlegung. Der Schutz von Kundendaten, die in Azure-Diensten gespeichert sind, ist für Microsoft von größter Bedeutung und sollte in jeden Architekturentwurf integriert werden. Grundlegende Dienste wie Azure Storage, Azure Virtual Machines, Azure SQL-Datenbank und Azure Key Vault können Ihre Umgebung durch Verschlüsselung schützen.