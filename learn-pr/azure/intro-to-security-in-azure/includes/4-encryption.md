Die meisten Organisationen sind die Daten der wichtigsten und wertvollsten Asset. Verschlüsselung dient als die stärksten und letzten Verteidigungslinie in einer mehrschichtigen Sicherheitsstrategie. 

Contoso Protokollversand weiß, dass die Verschlüsselung der einzige verfügbare Schutz ist, den über Daten verfügt, sobald das Rechenzentrum überlässt, wie es leitet an die mobile apps.

## <a name="what-is-encryption"></a>Was ist Verschlüsselung?

Verschlüsselung ist der Vorgang, Daten nicht lesbar und nicht verwendbar zu machen. Damit Sie verschlüsselte Daten verwenden oder lesen können, müssen diese *entschlüsselt* werden. Dies erfordert einen geheimen Schlüssel. Es gibt zwei Typen von der obersten Ebene der Verschlüsselung: **symmetrischen** und **asymmetrischen**.

Die symmetrische Verschlüsselung verwendet den gleichen Schlüssel zum Verschlüsseln und Entschlüsseln der Daten. Ziehen Sie eine Kennwort-Manager-Desktopanwendung in Betracht. Sie geben Ihre Passwörter ein, und diese werden mit Ihrem persönlichen Schlüssel verschlüsselt (Ihr Schlüssel wird oft von Ihrem Masterkennwort abgeleitet). Wenn die Daten abgerufen werden müssen, wird der gleiche Schlüssel verwendet, und die Daten werden entschlüsselt.

Die asymmetrische Verschlüsselung verwendet ein öffentlich-privates Schlüsselpaar. Beide Schlüssel verschlüsseln kann, aber ein einzelner Schlüssel kann nicht seine eigenen verschlüsselten Daten entschlüsselt. Zum Entschlüsseln benötigen Sie das jeweils andere Schlüsselpaar. Asymmetrischer Verschlüsselung wird für Dinge wie Sicherheit TLS (Transport Layer) (verwendet in HTTPS) und das Signieren von Daten verwendet.

Sowohl die symmetrische als auch die asymmetrische Verschlüsselung spielen eine Rolle bei der ordnungsgemäßen Sicherung von Daten. 

Bei der Verschlüsselung wird in der Regel zwischen zwei Optionen unterschieden: Verschlüsselung ruhender Daten und Verschlüsselung in Übertragung begriffener Daten.

## <a name="encryption-in-transit"></a>Verschlüsselung in Übertragung begriffener Daten

In Übertragung begriffene Daten sind Daten, die sich aktiv von einem Ort zu einem anderen bewegen, z.B. über das Internet oder über ein privates Netzwerk. Sicherer Übertragung kann von mehreren verschiedenen Ebenen behandelt werden. Es konnte durch Verschlüsseln der Daten auf der Anwendungsebene vor dem Senden über ein Netzwerk erfolgen. HTTPS ist ein Beispiel für die Anwendungsebene in der Übertragung Verschlüsselung. 

Sie können auch einen sicheren Kanal wie ein virtuelles privates Netzwerk (VPN), auf der Netzwerkebene ein einrichten, zum Übertragen von Daten zwischen zwei Systemen. 

Das Verschlüsseln von Daten, die übertragen werden, schützt die Daten vor externen Beobachtern und bietet einen Mechanismus zur Datenübertragung bei gleichzeitiger Einschränkung des Offenlegungsrisikos. 

<!--TODO: replace with final media which was submitted for Design-for-security-in-azure -->
![Verschlüsselung während der Übertragung](../media-COPIED-FROM-DESIGNFORSECURITY/encryption-in-transit.png)


## <a name="encryption-at-rest"></a>Verschlüsselung ruhender Daten

Ruhende Daten sind Daten, die auf einem physischen Medium gespeichert sind. Das sind beispielsweise Daten, die auf dem Datenträger eines Servers, in einer Datenbank oder in einem Speicherkonto gespeichert sind. Unabhängig vom Speichermechanismus stellt die Verschlüsselung ruhender Daten sicher, dass die gespeicherten Daten ohne die zum Entschlüsseln erforderlichen Schlüssel und Geheimnisse nicht lesbar sind. Wenn ein Angreifer nun eine Festplatte mit verschlüsselten Daten erhält, aber keinen Zugriff auf die Verschlüsselungsschlüssel hat, kann der Angreifer die Daten nicht ohne Weiteres kompromittieren.

Die tatsächlich verschlüsselten Daten können in Hinblick auf Inhalt, Verwendung und Bedeutung für das Unternehmen variieren. Dies könnte finanzielle Informationen, die Geschäftsabläufe, geistiges Eigentum, die von Geschäfts, persönliche Daten über Kunden oder Mitarbeiter, die das Unternehmen speichert, entwickelt wurde und sogar die Schlüssel und Geheimnisse, die für die Verschlüsselung der Daten selbst verwendet werden. .

<!--TODO: replace with final media which was submitted for Design-for-security-in-azure -->
![Verschlüsselung ruhender Daten](../media-COPIED-FROM-DESIGNFORSECURITY/encryption-at-rest.png)

## <a name="encryption-on-azure"></a>Verschlüsselung in Azure

Betrachten wir einige Möglichkeiten, wie Sie mit Azure Daten dienstübergreifend verschlüsseln können.

### <a name="encrypt-raw-storage"></a>Verschlüsseln von unformatierten Speicher

Die Azure-Speicherdienstverschlüsselung für ruhende Daten unterstützt Sie dabei, Ihre Daten zu schützen, um die Sicherheits- und Complianceanforderungen Ihrer Organisation zu erfüllen. Mit dieser Funktion verschlüsselt die Azure-Speicherplattform Ihre Daten automatisch vor dem Ablegen in Azure Managed Disks, Azure Blob Storage, Azure Files oder Azure Queue Storage und entschlüsselt sie vor dem Abrufen. Die Verarbeitung der Ver- und Entschlüsselung, der Verschlüsselung ruhender Daten und der Speicherdienstverschlüsselung ist für Anwendungen, die die Dienste verwenden, transparent.

### <a name="encrypt-virtual-machines"></a>Verschlüsseln virtueller Computer

Schützt Azure-Speicherdienstverschlüsselung Low-Level-Verschlüsselung für Daten, die auf physischen Datenträger geschrieben, aber wie schützen Sie die virtuellen Festplatten (VHDs) von virtuellen Computern? Angenommen ein bösartiger Angreifer erhält Zugriff auf Ihr Azure-Abonnement und filtert die VHDs Ihrer virtuellen Computer: Wie stellen Sie dann sicher, dass er nicht auf die VHD-Daten zugreifen kann?

Azure Disk Encryption ist eine Funktion, mit der Sie die Datenträger von virtuellen Windows- und Linux-IaaS-Computern verschlüsseln können. Azure Disk Encryption nutzt der Branche zum Standard-BitLocker-Features von Windows und die Funktion dm-Crypt von Linux, um Volumeverschlüsselung für das Betriebssystem und die Datenträger bereitzustellen. Die Lösung in Azure Key Vault können Sie steuern und Verwalten der Datenträger-Verschlüsselungsschlüssel und Geheimnisse integriert ist (und Sie können verwaltete Dienstidentitäten verwenden, für den Zugriff auf Key Vault).

Um den Rückversand für Contoso wurde mithilfe von virtuellen Computern eines ihrer ersten Verschiebungen in Richtung der Cloud. Alle VHDs, die verschlüsselt ist eine sehr schnell und mit geringen Auswirkungen Möglichkeit, um sicherzustellen, dass sie alle ausführen, um ihre Daten sichern kann.

### <a name="encrypt-databases"></a>Verschlüsseln von Datenbanken

Transparent Data Encryption (TDE) trägt zum Schutz von Azure SQL-Datenbank und Azure Data Warehouse vor der Bedrohung durch schädliche Aktivitäten bei. TDE ver- und entschlüsselt die Datenbank, die zugehörigen Sicherungen und die Transaktionsprotokolldateien im Ruhezustand in Echtzeit, ohne dass Änderungen an der Anwendung erforderlich sind. Standardmäßig ist TDE für alle neu bereitgestellten Azure SQL-Datenbank-Instanzen aktiviert.

TDE verschlüsselt die Speicherung einer gesamten Datenbank, indem ein symmetrischer Schlüssel verwendet wird, der als Datenbankverschlüsselungsschlüssel bezeichnet wird. Standardmäßig werden Azure stellt einen eindeutigen Verschlüsselungsschlüssel pro logischer SQL Server-Instanz und behandelt alle Details. Bring-your own Key (BYOK) wird ebenfalls mit Schlüsseln in Azure Key Vault unterstützt.

Da TDE standardmäßig aktiviert ist, kann Contoso Protokollversand sein sicher, dass sie die richtigen Schutzmaßnahmen für Daten in ihren Datenbanken verfügen.

### <a name="encrypt-secrets"></a>Verschlüsseln von Geheimnissen

Es wurde erläutert, dass alle Verschlüsselungsdienste Schlüssel zum Verschlüsseln und Entschlüsseln von Daten verwenden. Wie können Sie also sicherstellen, dass die Schlüssel selbst sicher sind? Möglicherweise müssen Unternehmen auch, Kennwörter, Verbindungszeichenfolgen und andere vertraulichen Informationen, die sie benötigen, um sicher zu speichern.

Azure Key Vault ist ein Clouddienst, der als sicherer Geheimnisspeicher fungiert. Mit Key Vault können Sie mehrere sichere Container (sogenannte Tresore) erstellen. Diese Tresore basieren auf Hardwaresicherheitsmodulen (HSMs). Tresore zentralisieren die Speicherung von Anwendungsgeheimnissen und verringern so die Gefahr, dass Sicherheitsinformationen verloren gehen. Key Vault-Instanzen auch steuern, und melden Sie den Zugriff auf alle darin gespeicherten Daten. Azure Key Vault können behandeln, anfordern und Erneuern von TLS-Zertifikate, die Funktionen für eine zuverlässige Lebenszyklus-Management-Lösung erforderlich sind. Key Vault ist für die Unterstützung jeder Art von Geheimnissen konzipiert. Diese Geheimnisse möglicherweise Kennwörter, Datenbank-Anmeldeinformationen, API-Schlüssel und Zertifikate.

Da es sich bei Azure AD-Identitäten Zugriff auf Azure Key Vault-Geheimnissen erteilt werden können, Anwendungen mit verwalteten Dienstidentitäten aktiviert können automatisch nahtlos bzw. abrufen und die geheimen Schlüssel, die sie benötigen.

Verschlüsselung ist häufig die letzte Stufe zum Schutz vor Angriffen, und es ist ein wichtiger Bestandteil der Verwendung eines Schichtenmodells für Sicherheit Ihrer Systeme. Azure bietet integrierte Funktionen und Dienste zum Verschlüsseln und die Daten vor unbeabsichtigten Offenlegung zu schützen. Schutz von Kundendaten in Azure-Dienste gespeichert ist von größter Wichtigkeit an Microsoft und in jedem Entwurf enthalten sein sollen. Grundlegende Dienste wie Azure Storage, Azure Virtual Machines, Azure SQL-Datenbank und Azure Key Vault können Ihre Umgebung durch Verschlüsselung schützen.