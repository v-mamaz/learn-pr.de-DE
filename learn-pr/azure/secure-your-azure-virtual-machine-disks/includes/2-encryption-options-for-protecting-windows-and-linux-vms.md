Angenommen, die Handelspartner Ihres Unternehmens haben Sicherheitsrichtlinien, die verlangen, dass ihre Handelsdaten durch eine starke Verschlüsselung geschützt sind. Sie verwenden eine B2B-Anwendung, die auf Ihren Windows-Servern ausgeführt wird, und Daten auf dem Serverdatenträger speichert. Jetzt, da Sie in die Cloud wechseln, müssen Sie Ihren Handelspartnern nachweisen, dass auf die auf Ihren Azure-VMs gespeicherten Daten nicht von unbefugten Benutzern, Geräten oder Anwendungen zugegriffen werden kann. Sie müssen sich für eine Strategie für die Implementierung der Verschlüsselung Ihrer B2B-Daten entscheiden.

Ihre Auditing-Anforderungen müssen bestimmen, dass Ihre Verschlüsselungsschlüssel intern, und nicht von Drittanbietern verwaltet werden. Es ist Ihnen außerdem wichtig, dass die Leistung und Verwaltbarkeit Ihrer Azure-basierten Server erhalten bleibt. Bevor Sie also Verschlüsselung implementieren, möchten Sie sicherstellen, dass es nicht zu einem Leistungseinbruch kommt.

## <a name="what-is-encryption"></a>Was ist Verschlüsselung?

Bei Verschlüsselung geht es um die Konvertierung bedeutungshaltiger Informationen in etwas, das bedeutungslos erscheint, wie eine zufällige Abfolge von Buchstaben und Ziffern. Der Prozess der Verschlüsselung verwendet eine Form der **Schlüssel** als Teil des Algorithmus, der die verschlüsselten Daten erstellt. Führen Sie die Entschlüsselung ist ein Schlüssel außerdem erforderlich. Schlüssel möglicherweise  **_symmetrischen_**, bei dem es sich bei der gleiche Schlüssel für die Ver- und Entschlüsselung verwendet wird oder  **_asymmetrischen_**, wobei die unterschiedliche Schlüsseln sind verwendet. Ein Beispiel für letzteren Fall wird die **öffentlichen / privaten** Schlüsselpaars in digitalen Zertifikaten verwendet.

### <a name="symmetric-encryption"></a>Symmetrische Verschlüsselung

Algorithmen, die symmetrische Schlüssel verwenden, wie etwa der Advanced Encryption Standard (AES), sind normalerweise schneller als Algorithmen mit einem öffentlichen Schlüssel und werden häufig für den Schutz großer Datenspeicher verwendet. Da es nur einen Schlüssel gibt, müssen Verfahren wirksam sein, die ein öffentliches Bekanntwerden des Schlüssels verhindern.

### <a name="asymmetric-encryption"></a>Asymmetrische Verschlüsselung

Bei asymmetrischen Algorithmen muss nur das private Schlüsselelement des Paars privat und sicher verwahrt werden; wie es der Name suggeriert, kann der öffentliche Schlüssel jedermann zur Verfügung gestellt werden, ohne dass die verschlüsselten Daten dadurch gefährdet würden. Der Nachteil öffentlicher Schlüsselalgorithmen besteht jedoch darin, dass sie viel langsamer als die symmetrischen Algorithmen sind und nicht zur Verschlüsselung großer Datenmengen verwendet werden können.

## <a name="key-management"></a>Schlüsselverwaltung

In Azure können Ihre Verschlüsselungsschlüssel entweder von Microsoft oder der Kunde verwaltet werden. Häufig kommt die Nachfrage nach vom Kunden verwalteten Schlüsseln von Organisationen, die ihre Konformität mit HIPAA oder anderen Bestimmungen nachweisen müssen. Diese Konformität kann es erforderlich machen, dass der Zugriff auf Schlüssel protokolliert wird und dass regelmäßige Änderungen des Schlüssels erfolgen, die ihrerseits erfasst werden.

## <a name="azure-disk-encryption-technologies"></a>Azure-Technologien zur Datenträgerverschlüsselung

Die wichtigsten verschlüsselungsbasierten Technologien zum Schutz von Datenträgern für Azure-VMs sind:

- Speicherdienstverschlüsselung (Storage Service Encryption, SSE)
- Azure Disk Encryption (ADE)

### <a name="storage-service-encryption"></a>Speicherdienstverschlüsselung

Azure Storage Service Encryption (SSE) ist eine Verschlüsselungsdienst erstellt in Azure, die es verwendet, um ruhende Daten zu schützen. Die Azure Storage-Plattform werden automatisch Daten verschlüsselt, bevor er auf mehrere Storage-Dienste, einschließlich Azure Managed Disks gespeichert wird. Verschlüsselung ist standardmäßig aktiviert, mittels 256-Bit-AES-Verschlüsselung und von der speicherkontoadministrator verwaltet wird.

### <a name="azure-disk-encryption"></a>Azure Disk Encryption

Azure Disk Encryption (ADE) wird vom Besitzer VM verwaltet. Er steuert die Verschlüsselung von Windows und Linux-VM gesteuerte Datenträger mithilfe von **BitLocker** auf Windows-VMs und **DM-Crypt** auf Linux-VMs. BitLocker Drive Encryption ist eine Datenschutzfunktion, die in das Betriebssystem und die Adressen der Bedrohung durch Datendiebstahl oder folgen von verlorenen, gestohlene oder nicht ordnungsgemäß außer Betrieb gesetzten Computern integriert ist. In ähnlicher Weise verschlüsselt DM-Crypt ruhende Daten für Linux vor dem Schreiben in den Speicher.

ADE stellt sicher, dass alle Daten auf VM-Datenträgern verschlüsselt im Azure-Speicher ruhen, und ADE ist für VMs erforderlich, die im Recovery-Tresor gesichert werden.

Mit ADE starten VMs unter Kunden gesteuerten Schlüsseln und Richtlinien aus. ADE ist zum Zweck der Verwaltung dieser Datenträger-Verschlüsselungsschlüssel und -Geheimnisse in den Azure Key Vault integriert.

> [!NOTE] 
> ADE unterstützt nicht die Verschlüsselung von Tarif "Basic" virtuelle Computer und einer lokalen Schlüsselverwaltungsdienst (KMS) mit ADE nicht verwendet werden können.

## <a name="when-to-use-encryption"></a>Wann soll Verschlüsselung verwendet werden?

Computerdaten sind bei der Übermittlung (Übermittlung über das Internet oder andere Netzwerke) und in Ruhe (auf einem Speichergerät gespeichert) gefährdet. Dem Szenario der ruhenden Daten gilt beim Schutz von Daten auf Azure VM-Datenträgern das Hauptaugenmerk. Beispielsweise kann jemand die einer Azure-VM zugeordnete VHD-Datei (Virtual Hard Disk) herunterladen und sie auf seinem Laptop speichern. Wenn die VHD nicht verschlüsselt ist, kann im Prinzip jeder, der die VHD-Datei auf seinem Computer einbinden kann, auf die Inhalte der VHD zugreifen.

Für Betriebssystem-Datenträger werden Daten wie Kennwörter automatisch verschlüsselt, so dass selbst bei nicht verschlüsselten VHDs der Zugriff auf diese Informationen nicht einfach ist. Darüber hinaus verschlüsseln Anwendungen möglicherweise ihre eigenen Daten. Wenn eine Person mit böswilligen Absichten jedoch Zugriff auf einen seinerseits nicht verschlüsselten Datenträger erhält, kann sie sich trotz solcher Schutzmaßnahmen in der Lage sehen, alle bekannten Schwachstellen beim Datenschutz der betreffenden Anwendung auszunutzen. Bei vorhandener Datenträgerverschlüsselung sind solche Exploits nicht möglich.

Storage Service Encryption (SSE) ist Teil von Azure selbst, und es sollten keine spürbaren Leistungseinbußen in der VM-Datenträger-e/a-Verwendung von SSE. Verwaltete Datenträger mit SSE werden nun die Standardeinstellung sollte, und es keinen Grund, ihn zu ändern. Azure Disk Encryption (ADE) nutzt Betriebssystemtools der VM (BitLocker und DM-Crypt), daher muss die VM bei der Verschlüsselung oder Entschlüsselung von VM-Datenträgern selbst ein gewisses Maß an Arbeit erbringen. Die Auswirkungen dieser zusätzlichen CPU-Aktivität der VM sind normalerweise unerheblich, außer in bestimmten Situationen. Z. B. Wenn Sie eine CPU-Intensive Anwendung haben, möglicherweise eine Anfrage zum Verlassen des Betriebssystem-Datenträgers, die entschlüsselt werden, um die Leistung zu maximieren. In einer derartigen Situation können Sie die Anwendungsdaten auf einem separaten, verschlüsselten Datenträger speichern, wodurch Sie die erforderliche Leistung ohne Beeinträchtigung der Sicherheit erhalten.

Azure stellt zwei sich ergänzende Verschlüsselungstechnologien zur Verfügung, die zum Schützen von Azure-VM-Datenträgern verwendet werden. Diese Technologien, SSE und ADE, verschlüsseln, die auf verschiedenen Ebenen und für andere Zwecke verwendet. Beide verwenden AES-256-Bit-Verschlüsselung. Der Einsatz beider Technologien bietet einen tiefgreifenden Schutz vor unberechtigtem Zugriff auf Ihren Azure-Speicher und auf bestimmte VHDs.
