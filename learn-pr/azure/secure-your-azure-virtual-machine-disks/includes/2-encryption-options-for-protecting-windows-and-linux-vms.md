Angenommen, die Handelspartner Ihres Unternehmens haben Sicherheitsrichtlinien, die verlangen, dass ihre Handelsdaten durch eine starke Verschlüsselung geschützt sind. Sie verwenden eine B2B-Anwendung, die auf Ihren Windows-Servern ausgeführt wird, und Daten auf dem Serverdatenträger speichert. Jetzt, da Sie in die Cloud wechseln, müssen Sie Ihren Handelspartnern nachweisen, dass auf die auf Ihren Azure-VMs gespeicherten Daten nicht von unbefugten Benutzern, Geräten oder Anwendungen zugegriffen werden kann. Sie müssen sich für eine Strategie für die Implementierung der Verschlüsselung Ihrer B2B-Daten entscheiden.

Ihre Anforderungen an die Überprüfung schreiben dabei vor, dass Ihre Verschlüsselungsschlüssel im Hause verwaltet werden, nicht von einem Drittanbieter. Es ist Ihnen außerdem wichtig, dass die Leistung und Verwaltbarkeit Ihrer Azure-basierten Server erhalten bleibt. Bevor Sie also Verschlüsselung implementieren, möchten Sie sicherstellen, dass es nicht zu einem Leistungseinbruch kommt.

## <a name="what-is-encryption"></a>Was ist Verschlüsselung?

Bei Verschlüsselung geht es um die Konvertierung bedeutungshaltiger Informationen in etwas, das bedeutungslos erscheint, wie eine zufällige Abfolge von Buchstaben und Ziffern. Der Vorgang der Verschlüsselung verwendet eine bestimmte Form von **Schlüssel** als Teil des Algorithmus, der die verschlüsselten Daten erstellt, und zum Durchführen der Entschlüsselung wird ebenfalls ein Schlüssel benötigt. Schlüssel können **_symmetrisch_** sein, dann wird für die Verschlüsselung und die Entschlüsselung der gleiche Schlüssel verwendet, oder **_asymmetrisch_**, dann werden verschiedene Schlüssel verwendet, wie etwa bei den **öffentlich-privaten** Schlüsselpaaren, die in digitalen Zertifikaten verwendet werden.

### <a name="symmetric-encryption"></a>Symmetrische Verschlüsselung

Algorithmen, die symmetrische Schlüssel verwenden, wie etwa der Advanced Encryption Standard (AES), sind normalerweise schneller als Algorithmen mit einem öffentlichen Schlüssel und werden häufig für den Schutz großer Datenspeicher verwendet. Da es nur einen Schlüssel gibt, müssen Verfahren wirksam sein, die ein öffentliches Bekanntwerden des Schlüssels verhindern.

### <a name="asymmetric-encryption"></a>Asymmetrische Verschlüsselung

Bei asymmetrischen Algorithmen muss nur das private Schlüsselelement des Paars privat und sicher verwahrt werden; wie es der Name suggeriert, kann der öffentliche Schlüssel jedermann zur Verfügung gestellt werden, ohne dass die verschlüsselten Daten dadurch gefährdet würden. Der Nachteil öffentlicher Schlüsselalgorithmen besteht jedoch darin, dass sie viel langsamer als die symmetrischen Algorithmen sind und nicht zur Verschlüsselung großer Datenmengen verwendet werden können.

## <a name="key-management"></a>Schlüsselverwaltung

In Azure können Ihre Verschlüsselungsschlüssel entweder von Microsoft oder vom Kunden verwaltet werden. Häufig kommt die Nachfrage nach vom Kunden verwalteten Schlüsseln von Organisationen, die ihre Konformität mit HIPAA oder anderen Bestimmungen nachweisen müssen. Diese Konformität kann es erforderlich machen, dass der Zugriff auf Schlüssel protokolliert wird und dass regelmäßige Änderungen des Schlüssels erfolgen, die ihrerseits erfasst werden.

## <a name="azure-disk-encryption-technologies"></a>Azure-Technologien zur Datenträgerverschlüsselung

Die wichtigsten verschlüsselungsbasierten Technologien zum Schutz von Datenträgern für Azure-VMs sind:

- Speicherdienstverschlüsselung (Storage Service Encryption, SSE)
- Azure Disk Encryption (ADE)

### <a name="storage-service-encryption"></a>Speicherdienstverschlüsselung

Azure-Speicherdienstverschlüsselung (SSE) ist ein in Azure integrierter Verschlüsselungsdienst, der zum Schutz von ruhenden Daten verwendet wird. Die Azure-Speicherplattform verschlüsselt Daten automatisch, bevor sie auf verschiedenen Speicherdiensten gespeichert werden, darunter Azure Managed Disks. Verschlüsselung mit 256-Bit-AES-Verschlüsselung ist standardmäßig aktiviert und wird vom Administrator des Speicherkontos verwaltet.

### <a name="azure-disk-encryption"></a>Azure Disk Encryption

Azure Disk Encryption (ADE) wird vom Besitzer der VM verwaltet und steuert die Verschlüsselung von Datenträgern, die der Steuerung durch virtuelle Windows- oder Linux-VMs unterliegen, und verwendet dazu **BitLocker** auf Windows-VMs und **DM-Crypt** auf Linux-VMs. Die BitLocker-Laufwerkverschlüsselung ist eine Datenschutzfunktion, die in das Betriebssystem integriert ist und der Bedrohung durch Datendiebstahl oder der Offenlegung durch verlorene, gestohlene oder unsachgemäß außer Betrieb gesetzte Computer entgegenwirkt. In ähnlicher Weise verschlüsselt DM-Crypt ruhende Daten für Linux vor dem Schreiben in den Speicher.

ADE stellt sicher, dass alle Daten auf VM-Datenträgern verschlüsselt im Azure-Speicher ruhen, und ADE ist für VMs erforderlich, die im Recovery-Tresor gesichert werden.

Bei der Verwendung von ADE erfolgt der Start von VMs unter vom Kunden gesteuerten Schlüsseln und Richtlinien. ADE ist zum Zweck der Verwaltung dieser Datenträger-Verschlüsselungsschlüssel und -Geheimnisse in den Azure Key Vault integriert.

> [!NOTE] 
> ADE unterstützt nicht die Verschlüsselung von VMs im Basic-Tarif, und Sie können keinen lokalen Schlüsselverwaltungsdienst (Key Management Service, KMS) zusammen mit ADE verwenden.

## <a name="when-to-use-encryption"></a>Wann soll Verschlüsselung verwendet werden?

Computerdaten sind bei der Übermittlung (Übermittlung über das Internet oder andere Netzwerke) und in Ruhe (auf einem Speichergerät gespeichert) gefährdet. Dem Szenario der ruhenden Daten gilt beim Schutz von Daten auf Azure VM-Datenträgern das Hauptaugenmerk. Beispielsweise kann jemand die einer Azure-VM zugeordnete VHD-Datei (Virtual Hard Disk) herunterladen und sie auf seinem Laptop speichern. Wenn die VHD nicht verschlüsselt ist, kann im Prinzip jeder, der die VHD-Datei auf seinem Computer einbinden kann, auf die Inhalte der VHD zugreifen.

Für Betriebssystem-Datenträger werden Daten wie Kennwörter automatisch verschlüsselt, so dass selbst bei nicht verschlüsselten VHDs der Zugriff auf diese Informationen nicht einfach ist. Darüber hinaus verschlüsseln Anwendungen möglicherweise ihre eigenen Daten. Wenn eine Person mit böswilligen Absichten jedoch Zugriff auf einen seinerseits nicht verschlüsselten Datenträger erhält, kann sie sich trotz solcher Schutzmaßnahmen in der Lage sehen, alle bekannten Schwachstellen beim Datenschutz der betreffenden Anwendung auszunutzen. Bei vorhandener Datenträgerverschlüsselung sind solche Exploits nicht möglich.

Die Speicherdienstverschlüsselung (SSE) ist ein Teil von Azure selbst, und der Einsatz von SSE sollte keinen spürbaren Einfluss auf die EA-Leistung des VM-Datenträgers haben. Verwaltete Datenträger mit SSE stellen mittlerweile den Standard dar, und es sollte keinen Grund geben, daran etwas zu ändern. Azure Disk Encryption (ADE) nutzt Betriebssystemtools der VM (BitLocker und DM-Crypt), daher muss die VM bei der Verschlüsselung oder Entschlüsselung von VM-Datenträgern selbst ein gewisses Maß an Arbeit erbringen. Die Auswirkungen dieser zusätzlichen CPU-Aktivität der VM sind normalerweise unerheblich, außer in bestimmten Situationen. Wenn Sie beispielsweise über eine CPU-intensive Anwendung verfügen, kann es sinnvoll sein, den Betriebssystem-Datenträger unverschlüsselt zu lassen, um die Leistung zu maximieren. In einer derartigen Situation können Sie die Anwendungsdaten auf einem separaten, verschlüsselten Datenträger speichern, wodurch Sie die erforderliche Leistung ohne Beeinträchtigung der Sicherheit erhalten.

Azure stellt zwei sich ergänzende Verschlüsselungstechnologien zur Verfügung, die zum Schützen von Azure-VM-Datenträgern verwendet werden. Diese Technologien, SSE und ADE, verschlüsseln auf verschiedenen Ebenen und dienen verschiedenen Zwecken; beide verwenden AES-256-Bit-Verschlüsselung. Der Einsatz beider Technologien bietet einen tiefgreifenden Schutz vor unberechtigtem Zugriff auf Ihren Azure-Speicher und auf bestimmte VHDs.
