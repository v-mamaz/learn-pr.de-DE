Angenommen, die Handelspartner Ihres Unternehmens haben Sicherheitsrichtlinien, die verlangen, dass ihre Handelsdaten durch eine starke Verschlüsselung geschützt sind. Sie verwenden eine B2B-Anwendung, die auf Ihren Windows-Servern ausgeführt wird, und Daten auf dem Serverdatenträger speichert. Jetzt, da Sie in die Cloud wechseln, müssen Sie Ihren Handelspartnern nachweisen, dass auf die auf Ihren Azure-VMs gespeicherten Daten nicht von unbefugten Benutzern, Geräten oder Anwendungen zugegriffen werden kann. Sie müssen sich für eine Strategie für die Implementierung der Verschlüsselung Ihrer B2B-Daten entscheiden.

Ihre Anforderungen an die Überprüfung schreiben dabei vor, dass Ihre Verschlüsselungsschlüssel nicht von einem Drittanbieter, sondern organisationsintern verwaltet werden müssen. Es ist Ihnen außerdem wichtig, dass die Leistung und Verwaltbarkeit Ihrer Azure-basierten Server erhalten bleibt. Bevor Sie also Verschlüsselung implementieren, möchten Sie sicherstellen, dass es nicht zu einem Leistungseinbruch kommt.

## <a name="what-is-encryption"></a>Was ist Verschlüsselung?

Bei Verschlüsselung geht es um die Konvertierung bedeutungshaltiger Informationen in etwas, das bedeutungslos erscheint, wie eine zufällige Abfolge von Buchstaben und Ziffern. Bei einer Verschlüsselung wird ein bestimmter **Schlüssel** als Teil des Algorithmus verwendet, der die verschlüsselten Daten erstellt. Für die Entschlüsselung wird ebenfalls ein Schlüssel benötigt. Bei **_symmetrischen_** Schlüsseln wird für die Verschlüsselung und Entschlüsselung der gleiche Schlüssel verwendet, während bei **_asymmetrischen_** Schlüsseln verschiedene Schlüssel verwendet werden. Ein Beispiel für die letztgenannte Variante ist ein Schlüsselpaar aus einem **öffentlichen und einem privaten** Schlüssel, das in digitalen Zertifikaten verwendet wird.

### <a name="symmetric-encryption"></a>Symmetrische Verschlüsselung

Algorithmen, die symmetrische Schlüssel verwenden, wie etwa der Advanced Encryption Standard (AES), sind normalerweise schneller als Algorithmen mit einem öffentlichen Schlüssel und werden häufig für den Schutz großer Datenspeicher verwendet. Da es nur einen Schlüssel gibt, müssen Verfahren wirksam sein, die ein öffentliches Bekanntwerden des Schlüssels verhindern.

### <a name="asymmetric-encryption"></a>Asymmetrische Verschlüsselung

Bei asymmetrischen Algorithmen muss nur das private Schlüsselelement des Paars privat und sicher verwahrt werden; wie es der Name suggeriert, kann der öffentliche Schlüssel jedermann zur Verfügung gestellt werden, ohne dass die verschlüsselten Daten dadurch gefährdet würden. Der Nachteil öffentlicher Schlüsselalgorithmen besteht jedoch darin, dass sie viel langsamer als die symmetrischen Algorithmen sind und nicht zur Verschlüsselung großer Datenmengen verwendet werden können.

## <a name="key-management"></a>Schlüsselverwaltung

In Azure können Ihre Verschlüsselungsschlüssel von Microsoft oder vom Kunden verwaltet werden. Die Nachfrage nach von Kunden verwalteten Schlüsseln geht häufig von Organisationen aus, die ihre Konformität mit HIPAA oder anderen Bestimmungen nachweisen müssen. Diese Konformität kann es erforderlich machen, dass der Zugriff auf Schlüssel protokolliert wird und dass regelmäßige Änderungen des Schlüssels erfolgen, die ihrerseits erfasst werden.

## <a name="azure-disk-encryption-technologies"></a>Azure-Technologien zur Datenträgerverschlüsselung

Die wichtigsten verschlüsselungsbasierten Technologien zum Schutz von Datenträgern für Azure-VMs sind:

- Speicherdienstverschlüsselung (Storage Service Encryption, SSE)
- Azure Disk Encryption (ADE)

### <a name="storage-service-encryption"></a>Speicherdienstverschlüsselung

Die Azure-Speicherdienstverschlüsselung (SSE) ist ein in Azure integrierter Verschlüsselungsdienst, der zum Schutz von ruhenden Daten verwendet wird. Die Azure-Speicherplattform verschlüsselt Daten automatisch, bevor sie in verschiedenen Speicherdiensten wie Azure Managed Disks gespeichert werden. Als Standardverschlüsselung kommt AES mit 256 Bit zum Einsatz. Diese wird vom Administrator des Speicherkontos verwaltet.

### <a name="azure-disk-encryption"></a>Azure Disk Encryption

Azure Disk Encryption (ADE) wird vom Besitzer des virtuellen Computers verwaltet. Der Dienst steuert die Verschlüsselung von Windows- und Linux-VM-Datenträgern und verwendet dazu **BitLocker** auf Windows-VMs und **DM-Crypt** auf Linux-VMs. Die BitLocker-Laufwerkverschlüsselung ist ein Feature zum Schutz von Daten, das in das Betriebssystem integriert ist und der Bedrohung durch Datendiebstahl oder der Offenlegung durch verlorene, gestohlene oder unsachgemäß außer Betrieb gesetzte Computer entgegenwirkt. In ähnlicher Weise verschlüsselt DM-Crypt ruhende Daten für Linux vor dem Schreiben in den Speicher.

ADE stellt sicher, dass alle Daten auf den VM-Datenträgern im ruhenden Zustand im Azure-Speicher verschlüsselt werden. ADE ist für VMs erforderlich, die im Recovery-Tresor gesichert werden.

Bei der Verwendung von ADE werden beim Start von VMs die vom Kunden verwalteten Schlüssel und Richtlinien berücksichtigt. ADE ist zum Zweck der Verwaltung dieser Datenträger-Verschlüsselungsschlüssel und -Geheimnisse in Azure Key Vault integriert.

> [!NOTE] 
> ADE unterstützt nicht die Verschlüsselung von VMs im Basic-Tarif, und Sie können keinen lokalen Schlüsselverwaltungsdienst zusammen mit ADE verwenden.

## <a name="when-to-use-encryption"></a>Wann soll Verschlüsselung verwendet werden?

Computerdaten sind bei der Übermittlung (Übermittlung über das Internet oder andere Netzwerke) und im Ruhezustand (auf einem Speichergerät gespeichert) gefährdet. Dem Szenario der ruhenden Daten gilt beim Schutz von Daten auf Azure VM-Datenträgern das Hauptaugenmerk. Beispielsweise kann jemand die einer Azure-VM zugeordnete VHD-Datei (Virtual Hard Disk) herunterladen und sie auf seinem Laptop speichern. Wenn die VHD nicht verschlüsselt ist, kann im Prinzip jeder, der die VHD-Datei auf seinem Computer einbinden kann, auf die Inhalte der VHD zugreifen.

Für Betriebssystem-Datenträger werden Daten wie Kennwörter automatisch verschlüsselt, so dass selbst bei nicht verschlüsselten VHDs der Zugriff auf diese Informationen nicht einfach ist. Darüber hinaus verschlüsseln Anwendungen möglicherweise ihre eigenen Daten. Wenn eine Person mit böswilligen Absichten jedoch Zugriff auf einen seinerseits nicht verschlüsselten Datenträger erhält, kann sie sich trotz solcher Schutzmaßnahmen in der Lage sehen, alle bekannten Schwachstellen beim Datenschutz der betreffenden Anwendung auszunutzen. Bei vorhandener Datenträgerverschlüsselung sind solche Exploits nicht möglich.

Die Speicherdienstverschlüsselung (SSE) ist Teil von Azure und sollte zu keinen spürbaren Leistungseinbußen bei E/A-Vorgängen für VM-Datenträger führen. SSE wird mittlerweile standardmäßig für verwaltete Datenträger verwendet, und es sollte keinen Grund geben, diese Einstellung zu ändern. Azure Disk Encryption (ADE) nutzt Betriebssystemtools der VM (BitLocker und DM-Crypt). Daher muss die VM bei der Verschlüsselung oder Entschlüsselung von VM-Datenträgern selbst ein gewisses Maß an Arbeit erbringen. Die Auswirkungen dieser zusätzlichen CPU-Aktivität der VM sind normalerweise unerheblich. Es gibt jedoch Ausnahmesituationen. Wenn Sie beispielsweise über eine CPU-intensive Anwendung verfügen, kann es sinnvoll sein, den Betriebssystem-Datenträger unverschlüsselt zu lassen, um die Leistung zu maximieren. In einer derartigen Situation können Sie die Anwendungsdaten auf einem separaten, verschlüsselten Datenträger speichern, wodurch Sie die erforderliche Leistung ohne Beeinträchtigung der Sicherheit erhalten.

Azure stellt zwei sich ergänzende Verschlüsselungstechnologien zur Verfügung, die zum Schützen von Azure-VM-Datenträgern verwendet werden. SSE und ADE verschlüsseln auf verschiedenen Ebenen und dienen verschiedenen Zwecken. Beide verwenden eine AES-256-Bit-Verschlüsselung. Der Einsatz beider Technologien ermöglicht mithilfe eines mehrschichtigen Sicherheitsansatzes Schutz vor unberechtigtem Zugriff auf Ihren Azure-Speicher und auf bestimmte VHDs.
