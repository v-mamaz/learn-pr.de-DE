Für die meisten Organisationen sind Daten die wichtigste und wertvollste Ressource. Die Verschlüsselung ist die letzte und stärkste Verteidigungslinie einer mehrschichtigen Sicherheitsstrategie. 

Contoso Shipping weiß, dass Verschlüsselung der einzige Schutz für die Daten ist, sobald diese das Datencenter verlassen und an die mobilen Apps übermittelt werden.

## <a name="what-is-encryption"></a>Was ist Verschlüsselung?

Verschlüsselung ist der Vorgang, bei dem Daten für unberechtigte Betrachter nicht lesbar und nicht verwendbar gemacht werden. Um verschlüsselte Daten verwenden oder lesen zu können, müssen sie *entschlüsselt* werden. Hierfür ist ein geheimer Schlüssel erforderlich. Es gibt zwei Arten von Verschlüsselungen auf oberster Ebene: **symmetrisch** und **asymmetrisch**.

Bei der symmetrischen Verschlüsselung wird zum Verschlüsseln und Entschlüsseln der Daten jeweils der gleiche Schlüssel verwendet. Ziehen Sie eine Kennwort-Manager-Desktopanwendung in Betracht. Sie geben Ihre Passwörter ein, und diese werden mit Ihrem persönlichen Schlüssel verschlüsselt (Ihr Schlüssel wird oft von Ihrem Masterkennwort abgeleitet). Wenn die Daten abgerufen werden müssen, wird der gleiche Schlüssel verwendet, und die Daten werden entschlüsselt.

Bei der asymmetrischen Verschlüsselung wird ein Schlüsselpaar mit einem öffentlichen und einem privaten Schlüssel verwendet. Beide Schlüssel können für das Verschlüsseln genutzt werden, aber mit nur einem Schlüssel können die eigenen verschlüsselten Daten nicht entschlüsselt werden. Zum Entschlüsseln benötigen Sie jeweils den anderen Schlüssel des Paars. Die asymmetrische Verschlüsselung wird beispielsweise für Transport Layer Security (TLS) (für HTTPS) und Datensignaturen verwendet.

Sowohl die symmetrische als auch die asymmetrische Verschlüsselung spielen eine Rolle bei der korrekten Sicherung von Daten. 

Bei der Verschlüsselung wird in der Regel zwischen zwei Optionen unterschieden: Verschlüsselung ruhender Daten und Verschlüsselung während der Übertragung.

## <a name="encryption-in-transit"></a>Verschlüsselung während der Übertragung

Daten während der Übertragung sind Daten, die aktiv zwischen zwei Orten übermittelt werden – etwa über das Internet oder über ein privates Netzwerk. Die sichere Übertragung kann von mehreren verschiedenen Ebenen übernommen werden. Die Daten können vor dem Senden über ein Netzwerk beispielsweise auf der Anwendungsebene verschlüsselt werden. HTTPS ist ein Beispiel für eine Verschlüsselung auf Anwendungsebene bei der Übertragung. 

Sie können auch einen sicheren Kanal (z.B. ein virtuelles privates Netzwerk (VPN)) auf Netzwerkebene einrichten, um Daten zwischen zwei Systemen zu übertragen. 

Das Verschlüsseln von Daten während der Übertragung schützt die Daten vor externen Beobachtern und bietet einen Mechanismus zur Datenübertragung bei gleichzeitiger Einschränkung des Offenlegungsrisikos. 

![Verschlüsselung während der Übertragung](../media/encryption-in-transit.png)


## <a name="encryption-at-rest"></a>Verschlüsselung ruhender Daten

Ruhende Daten sind Daten, die auf einem physischen Medium gespeichert sind. Das sind beispielsweise Daten, die auf dem Datenträger eines Servers, in einer Datenbank oder in einem Speicherkonto gespeichert sind. Unabhängig vom Speichermechanismus stellt die Verschlüsselung ruhender Daten sicher, dass die gespeicherten Daten ohne die zum Entschlüsseln erforderlichen Schlüssel und Geheimnisse nicht lesbar sind. Wenn ein Angreifer eine Festplatte mit verschlüsselten Daten erhält, aber keinen Zugriff auf die Verschlüsselungsschlüssel hat, kann der Angreifer die Daten nicht ohne Weiteres kompromittieren.

Die tatsächlichen verschlüsselten Daten können im Hinblick auf Inhalt, Verwendung und Bedeutung für das Unternehmen variieren. Dies können geschäftskritische Finanzinformationen, geistiges Eigentum des Unternehmens, persönliche Kunden- oder Mitarbeiterdaten in Speichern des Unternehmens und auch die Schlüssel und Geheimnisse sein, die für die Datenverschlüsselung verwendet werden.

![Verschlüsselung ruhender Daten](../media/encryption-at-rest.png)

## <a name="encryption-on-azure"></a>Verschlüsselung in Azure

Betrachten wir einige Möglichkeiten, wie Sie mit Azure Daten dienstübergreifend verschlüsseln können.

:::row:::
  :::column:::
    ![Bild zu verschlüsseltem Speicher](../media/4-encrypt-raw-storage.png)
  :::column-end:::
    :::column span="3"::: **Verschlüsseln von unformatiertem Speicher**

Die Azure-Speicherdienstverschlüsselung für ruhende Daten unterstützt Sie dabei, Ihre Daten zu schützen, um die Sicherheits- und Complianceanforderungen Ihrer Organisation zu erfüllen. Mit dieser Funktion verschlüsselt die Azure-Speicherplattform Ihre Daten automatisch vor dem Ablegen in Azure Managed Disks, Azure Blob Storage, Azure Files oder Azure Queue Storage und entschlüsselt sie vor dem Abrufen. Die Verarbeitung der Ver- und Entschlüsselung, der Verschlüsselung ruhender Daten und der Speicherdienstverschlüsselung ist für Anwendungen, die die Dienste verwenden, transparent.
  :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    ![Bild mit einem verschlüsselten virtuellen Computer](../media/4-encrypt-virtual-machines.png)
  :::column-end:::
    :::column span="3"::: **Verschlüsseln virtueller Computer**

Die Speicherdienstverschlüsselung bietet für Daten, die auf einen physischen Datenträger geschrieben werden, einen Verschlüsselungsschutz auf niedriger Ebene. Wie aber schützen Sie die virtuellen Festplatten (VHDs) von virtuellen Computern (VMs)? Angenommen, ein Angreifer erhält Zugriff auf Ihr Azure-Abonnement und entwendet die VHDs Ihrer virtuellen Computer: Wie stellen Sie dann sicher, dass er nicht auf die VHD-Daten zugreifen kann?

Azure Disk Encryption ist eine Funktion, mit der Sie die Datenträger von virtuellen Windows- und Linux-IaaS-Computern verschlüsseln können. Azure Disk Encryption nutzt das Branchenstandardfeature BitLocker von Windows und das Feature dm-crypt von Linux, um Volumeverschlüsselung für das Betriebssystem und die Datenträger bereitzustellen. Die Lösung ist in Azure Key Vault integriert, damit Sie die Verschlüsselungsschlüssel und Geheimnisse für die Datenträgerverschlüsselung steuern und verwalten können. Sie können mit verwalteten Dienstidentitäten auf Key Vault zugreifen.

Für Contoso Shipping war die Verwendung virtueller Computer einer der ersten Schritte auf dem Weg in die Cloud. Die Verschlüsselung aller VHDs ist eine sehr einfache Methode mit geringem Aufwand, mit der Sie sicherstellen können, dass Sie alles für den Schutz Ihrer Unternehmensdaten tun.
  :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    ![Bild einer verschlüsselten Datenbank](../media/4-encrypt-databases.png)
  :::column-end:::
    :::column span="3"::: **Verschlüsseln von Datenbanken**

Transparent Data Encryption (TDE) trägt dazu bei, Azure SQL-Datenbank und Azure Data Warehouse vor Bedrohungen durch schädliche Aktivitäten zu schützen. TDE ver- und entschlüsselt die Datenbank, die zugehörigen Sicherungen und die Transaktionsprotokolldateien im Ruhezustand in Echtzeit, ohne dass Änderungen an der Anwendung erforderlich sind. Standardmäßig ist TDE für alle neu bereitgestellten Azure SQL-Datenbank-Instanzen aktiviert.

TDE verschlüsselt die Speicherung einer gesamten Datenbank, indem ein symmetrischer Schlüssel verwendet wird, der als Datenbankverschlüsselungsschlüssel bezeichnet wird. Azure stellt standardmäßig einen eindeutigen Verschlüsselungsschlüssel pro logischer SQL Server-Instanz zur Verfügung und verarbeitet alle Details. Bring Your Own Key (BYOK) wird ebenfalls mit Schlüsseln unterstützt, die in Azure Key Vault gespeichert sind.

Da TDE standardmäßig aktiviert ist, können Sie sicher sein, dass Contoso Shipping angemessene Schutzmaßnahmen für die in seinen Datenbanken gespeicherten Daten ergriffen hat.
  :::column-end:::
:::row-end:::

:::row:::
  :::column:::
    ![Bild eines verschlüsselten Geheimnisses](../media/4-encrypt-secrets.png)
  :::column-end:::
    :::column span="3"::: **Verschlüsseln von Geheimnissen**

Wie bereits erwähnt, verwenden Verschlüsselungsdienste Schlüssel zum Verschlüsseln und Entschlüsseln von Daten. Wie können Sie also sicherstellen, dass die Schlüssel selbst sicher sind? Konzerne verfügen möglicherweise auch über Kennwörter, Verbindungszeichenfolgen und andere vertrauliche Informationen, die sicher gespeichert werden müssen.

Azure Key Vault ist ein Clouddienst, der als sicherer Geheimnisspeicher fungiert. Mit Key Vault können Sie mehrere sichere Container (sogenannte Tresore) erstellen. Diese Tresore basieren auf Hardwaresicherheitsmodulen (HSMs). In Tresoren wird die Speicherung von Anwendungsgeheimnissen zentralisiert, um die Gefahr zu verringern, dass Sicherheitsinformationen verloren gehen. Darüber hinaus steuern und protokollieren Schlüsseltresore den Zugriff auf alle darin gespeicherten Daten. Azure Key Vault kann TLS-Zertifikate anfordern und erneuern. Außerdem stellt die Lösung Funktionen bereit, die für eine zuverlässige Lösung zur Verwaltung des Zertifikatlebenszyklus benötigt werden. Key Vault ist für die Unterstützung jeder Art von Geheimnissen konzipiert. Dies umfasst Kennwörter, Anmeldeinformationen für Datenbanken, API-Schlüssel und Zertifikate.

Da Azure AD-Identitäten Zugriff auf Azure Key Vault-Geheimnisse gewährt werden kann, erhalten Anwendungen, für die verwaltete Dienstidentitäten aktiviert sind, automatisch und nahtlos die benötigten Geheimnisse.
  :::column-end:::
:::row-end:::

## <a name="summary"></a>Zusammenfassung

Wie Sie vielleicht wissen, ist die Verschlüsselung oft die letzte Sicherheitsstufe bei Angriffen und ein wichtiger Teil eines mehrstufigen Ansatzes zum Schutz Ihrer Systeme. Azure enthält integrierte Funktionen und Dienste, um Daten zu verschlüsseln und vor unbeabsichtigter Offenlegung zu schützen. Der Schutz von in Azure-Diensten gespeicherten Kundendaten ist für Microsoft von größter Bedeutung und sollte in jeden Entwurf integriert werden. Grundlegende Dienste wie Azure Storage, Azure Virtual Machines, Azure SQL-Datenbank und Azure Key Vault können mit der Verschlüsselung einen Beitrag zum Schutz Ihrer Umgebung leisten.