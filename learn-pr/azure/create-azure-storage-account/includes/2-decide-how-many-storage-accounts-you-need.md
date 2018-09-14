Organisationen verfügen häufig über mehrere Speicherkonten, um unterschiedliche Anforderungskataloge implementieren zu können. In dem Beispiel eines Schokoladenherstellers ist jeweils ein Speicherkonto für die privaten Geschäftsdaten und die Dateien vorhanden, auf die der Kunde Zugriff hat. In diesem Artikel lernen Sie die Richtlinienfaktoren kennen, die von einem Speicherkonto gesteuert werden und Ihnen bei der Entscheidung helfen, wie viele Konten Sie benötigen.

## <a name="what-is-azure-storage"></a>Was ist Azure Storage?

Azure bietet viele Möglichkeiten zum Speichern Ihrer Daten. Es stehen mehrere Datenbankoptionen wie Azure SQL-Datenbank, Azure Cosmos DB und Azure Table Storage zur Verfügung. Zudem bietet Azure diverse Möglichkeiten zum Speichern von Nachrichten, z.B. Azure Queue Storage und Event Hubs. Sie können sogar lose Dateien mithilfe von Optionen wie Azure Files und Azure Blob Storage speichern.

Vier dieser Datendienste wurden unter dem Namen _Azure Storage_ zusammengefasst. Zu diesen vier Diensten zählen Azure Blob Storage, Azure Files, Azure Queue Storage und Azure Table Storage. Die folgende Abbildung zeigt die Elemente von Azure Storage.

![Abbildung zur Auflistung von Azure-Datendiensten, die Teil von Azure Storage sind](../media-drafts/2-azure-storage.png)

Diesen vier Diensten wurde besondere Aufmerksamkeit geschenkt, da sie alle primitive, cloudbasierte Speicherdienste darstellen und häufig zusammen in derselben Anwendung verwendet werden.

## <a name="what-is-a-storage-account"></a>Was ist ein Speicherkonto?

Ein _Speicherkonto_ ist ein Container, der eine Reihe von Azure Storage-Diensten zusammen gruppiert. Nur Datendienste von Azure Storage können in einem Speicherkonto enthalten sein (Azure Blob Storage, Azure Files, Azure Queue Storage und Azure Table Storage). Die folgende Abbildung zeigt ein Speicherkonto mit mehreren Datendiensten.

![Abbildung eines Azure Storage-Kontos mit einer gemischten Sammlung von Datendiensten](../media-drafts/2-what-is-a-storage-account.png)

Durch die Kombination von Datendiensten in einem Speicherkonto können Sie diese als Gruppe verwalten. Die Einstellungen, die Sie bei der Erstellung des Kontos angeben, oder die Sie nach der Erstellung ändern, werden auf sämtliche Bereiche im Konto angewendet. Beim Löschen des Speicherkontos werden alle darin gespeicherten Daten gelöscht.

Ein Speicherkonto ist eine Azure-Ressource, die in einer Ressourcengruppe enthalten ist. Die folgende Abbildung zeigt ein Azure-Abonnement, das mehrere Ressourcengruppen enthält, wobei jede Gruppe mindestens ein Speicherkonto umfasst.

![Abbildung eines Azure-Abonnements mit mehreren Ressourcengruppen und Speicherkonten](../media-drafts/2-resource-groups-and-storage-accounts.png)

Andere Azure-Datendienste wie Azure SQL-Datenbank und Azure Cosmos DB werden als unabhängige Azure-Ressourcen verwaltet und können nicht in einem Speicherkonto enthalten sein. Die folgende Abbildung zeigt eine typische Anordnung: In Speicherkonten sind zwar Azure Blob Storage, Azure Files, Azure Queue Storage und Azure Table Storage, aber keine weiteren Dienste enthalten.

![Abbildung eines Azure-Abonnements mit Datendiensten, die nicht in einem Speicherkonto platziert werden können](../media-drafts/2-typical-subscription-organization.png)

## <a name="storage-account-settings"></a>Speicherkontoeinstellungen

Ein Speicherkonto definiert eine Richtlinie, die auf alle Speicherdienste im Konto angewendet wird. Beispielsweise können Sie angeben, dass alle enthaltenen Dienste im Rechenzentrum in „USA, Westen“ gespeichert werden, auf die nur über HTTPS zugegriffen werden kann und die im Rahmen des Abonnements der Vertriebsabteilung abgerechnet werden.

Zu den von einem Speicherkonto gesteuerten Einstellungen zählen Folgende:

- **Abonnement**: Das Azure-Abonnement, das für die Dienste im Konto abgerechnet wird.

- **Standort**: Das Rechenzentrum, in dem die Dienste im Konto gespeichert werden.

- **Leistung**: Bestimmt die Datendienste, die in Ihrem Speicherkonto enthalten sein können, und den Typ des zugrunde liegenden Hardwaredatenträgers. Mit **Standard** können Sie beliebige Datendienste (Azure Blob Storage, Azure Files, Azure Queue Storage und Azure Table Storage) sowie magnetische Laufwerke verwenden. Bei **Premium** sind Sie auf einen bestimmten Typ von Blob, nämlich _Seitenblobs_, beschränkt. Zudem werden bei diesem Angebot Solid State Drives für die Speicherung verwendet.

- **Replikation**: bestimmt die zum Kopieren Ihrer Daten verwendete Strategie, um vor Hardwareausfällen oder Naturkatastrophen zu schützen. Azure behält automatisch mindestens eine Kopie Ihrer Daten innerhalb des Rechenzentrums bei, das dem Speicherkonto zugeordnet ist. Dies wird als lokal redundanter Speicher (LRS) bezeichnet und schützt zwar vor Hardwareausfällen, aber nicht vor einem Ereignis, das das gesamte Rechenzentrum außer Betrieb setzt. Sie können ein Upgrade auf eine der anderen Optionen wie georedundanten Speicher (GRS) durchführen, um Replikationen in anderen Rechenzentren auf der ganzen Welt durchführen zu können.

- **Zugriffsebene**: steuert, wie schnell Sie auf die Blobs in diesem Speicherkonto zugreifen können. Die heiße Speicherebene bietet zwar schnelleren Zugriff als die kalte Speicherebene, verursacht jedoch auch höhere Kosten. Dies gilt nur für Blobs und dient als Standardwert für neue Blobs.

- **Sichere Übertragung erforderlich**:ein Sicherheitsfeature, das die unterstützten Protokolle für den Zugriff bestimmt. Wenn diese Option aktiviert ist, ist HTTPS erforderlich, wohingegen bei Deaktivierung der Option HTTP zulässig ist.

- **Virtuelle Netzwerke**: ein Sicherheitsfeature, das nur eingehende Zugriffsanforderungen von den von Ihnen angegebenen virtuellen Netzwerken zulässt.

## <a name="how-many-storage-accounts-do-you-need"></a>Wie viele Speicherkonten benötigen Sie?

Ein Speicherkonto stellt eine Sammlung von Einstellungen wie Standort, Replikationsstrategie und Abonnements dar. Sie benötigen ein Speicherkonto für sämtliche Gruppen von Einstellungen, die auf Ihre Daten angewendet werden sollen. Die folgende Abbildung zeigt zwei Speicherkonten, die sich hinsichtlich einer Einstellung unterscheiden. Bereits ein Unterschied macht separate Speicherkonten erforderlich.

![Abbildung zu zwei Speicherkonten mit unterschiedlichen Einstellungen](../media-drafts/2-multiple-storage-accounts.png)

Die Anzahl von Speicherkonten, die Sie benötigen, wird in der Regel durch die Vielfalt Ihrer Daten, Kostensensitivität und Toleranz hinsichtlich des Verwaltungsaufwands bestimmt.

### <a name="data-diversity"></a>Datenvielfalt

Organisationen generieren oftmals Daten, die sich darin unterscheiden, wo sie genutzt werden, wie sensibel diese sind, welche Gruppe die Rechnungen begleicht etc. Bestehen bei diesen Vektoren Abweichungen, kann dies zu mehreren Speicherkonten führen. Sehen wir uns hierzu zwei Beispiele an:

1. Verfügen Sie über Daten, die speziell für ein Land oder eine Region gelten? In diesem Fall empfiehlt es sich aus Leistungs- bzw. Compliancegründen, diese Daten in einem Rechenzentrum im jeweiligen Land zu speichern. Sie benötigen ein Speicherkonto für jeden Standort.

1. Besitzen Sie Daten, die einerseits proprietär und andererseits für die öffentliche Nutzung bestimmt sind? Wenn dies der Fall ist, können Sie virtuelle Netzwerke für die proprietären Daten implementieren und bei öffentlichen Daten andere Netzwerke verwenden. Hierfür sind zudem separate Speicherkonten erforderlich.

Eine höhere Diversität bedeutet im Allgemeinen eine höhere Anzahl von Speicherkonten.

### <a name="cost-sensitivity"></a>Kostensensitivität

Ein Speicherkonto selbst bringt keine Kosten mit sich, allerdings wirken sich die Einstellungen, die Sie für das Konto festlegen, sehr wohl auf die Kosten für Dienste des Kontos aus. Georedundante Speicher sind kostspieliger als lokal redundante Speicher. Durch Leistung auf Premium-Niveau und die heiße Zugriffsebene werden die Kosten für Blobs in die Höhe getrieben.

Sie können mehrere Speicherkonten verwenden, um die Kosten zu reduzieren. Beispielsweise können Sie Ihre Daten in die Kategorien „Kritisch“ und „Nicht kritisch“ unterteilen. Sie könnten Ihre kritischen Daten in ein Speicherkonto mit georedundantem Speicher und nicht kritische Daten in ein anderes Speicherkonto mit lokal redundantem Speicher platzieren.

### <a name="tolerance-for-management-overhead"></a>Toleranz hinsichtlich des Verwaltungsaufwands

Für die Erstellung und Verwaltung der einzelnen Speicherkonten muss ein Administrator ein gewisses Maß an Zeit und Aufmerksamkeit aufwenden. Zudem wird es für alle Benutzer komplexer, Daten zu Ihrem Cloudspeicher hinzuzufügen. Alle Benutzer in dieser Rolle müssen sich über den Zweck der einzelnen Speicherkonten im Klaren sein, um neue Daten dem richtigen Konto hinzuzufügen.

## <a name="summary"></a>Zusammenfassung

Speicherkonten stellen ein leistungsstarkes Tool dar, mit dem Sie die erforderliche Leistung und Sicherheit erhalten und gleichzeitig die Kosten senken können. Eine typische Strategie besteht darin, mit einer Analyse Ihrer Daten zu beginnen und Partitionen zu erstellen, die Eigenschaften wie Standort, Abrechnung und Replikationsstrategie aufweisen, und anschließend ein Speicherkonto für jede Partition zu erstellen.
