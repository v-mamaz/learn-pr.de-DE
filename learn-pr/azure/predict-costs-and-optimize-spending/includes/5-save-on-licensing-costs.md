Die Lizenzierung ist ein weiterer Bereich, der Ihre Cloudkosten erheblich erhöhen kann. Im Folgenden werden einige Möglichkeiten erläutert, um Ihre Lizenzierungskosten zu reduzieren.

## <a name="azure-hybrid-benefit-for-windows-server"></a>Azure-Hybridvorteil für Windows Server

Viele Kunden haben in Windows Server-Lizenzen investiert und möchten diese in Azure wiederverwenden. Mit dem Azure-Hybridvorteil können Kunden diese Lizenzen für virtuelle Computer in Azure verwenden. Das bedeutet, dass keine Kosten für die Windows Server-Lizenz entstehen und stattdessen die Linux-Gebühr abgerechnet wird. 

Ihre Windows-Lizenzen müssen ebenfalls durch Software Assurance abgedeckt sein, um diesen Vorteil nutzen zu können. Es gelten ebenfalls folgende Richtlinien:

- Jede Lizenz für zwei Prozessoren oder alle Lizenzen für je 16 Kerne kann für zwei Instanzen mit bis zu acht Kernen oder für eine Instanz mit bis zu 16 Kernen eingesetzt werden.
- Standard Edition-Lizenzen können nur einmalig entweder lokal oder in Azure verwendet werden. Das bedeutet, dass Sie dieselbe Lizenz nicht für einen virtuellen Azure-Computer und einen lokalen Computer verwenden können.
- Mit der Datacenter Edition ist die gleichzeitige Nutzung sowohl lokal als auch in Azure möglich. Diese Lizenz umfasst also zwei ausgeführte Windows-Computer.

> [!NOTE]
> Die meisten Kunden verwenden eine Lizenzierung pro Kern, deshalb wird dieses Modell für die Berechnung verwendet. Wenn Sie Fragen zu Ihren Lizenzen haben, wenden Sie sich an Ihren Lizenzanbieter oder an Ihr Microsoft-Kontoteam.

Das Anwenden des Vorteils ist einfach. Er kann für vorhandene virtuelle Computer jederzeit aktiviert oder deaktiviert werden oder zum Zeitpunkt der Bereitstellung auf neue virtuelle Computer angewendet werden. Der Hybridvorteil (insbesondere in Kombination mit reservierten Instanzen) kann erheblich zur Einsparung von Lizenzkosten beitragen.

## <a name="azure-hybrid-benefit-for-sql-server"></a>Azure-Hybridvorteil für SQL Server

Der Azure-Hybridvorteil für SQL Server ermöglicht eine maximale Nutzung Ihrer aktuellen Lizenzinvestitionen sowie eine schnellere Migration in die Cloud. Mit dem Azure-Hybridvorteil für SQL Server können Sie Ihre SQL Server-Lizenzen mit aktiver Software Assurance verwenden und zahlen so einen geringeren Preis.

Sie können diesen Vorteil auch in Anspruch nehmen, wenn die Azure-Ressource aktiv ist. Die reduzierte Gebühr wird jedoch von dem Zeitpunkt an angewendet, zu dem dieser im Portal ausgewählt wird. Guthaben werden nicht rückwirkend gewährt.

### <a name="azure-sql-database-vcore-based-options"></a>Auf virtuellen Kernen basierende Optionen für Azure SQL-Datenbank

Für Azure SQL-Datenbank funktioniert der Azure-Hybridvorteil folgendermaßen:

- Wenn Sie die Standard Edition mit Lizenzen pro Kern mit aktiver Software Assurance besitzen, erhalten Sie einen virtuellen Kern in der universellen Dienstebene für jeden Kern, den Sie durch eine Lizenz lokal besitzen.
- Wenn Sie die Enterprise Edition mit Lizenzen pro Kern mit aktiver Software Assurance besitzen, erhalten Sie einen virtuellen Kern in der unternehmenskritischen Dienstebene für jeden Kern, den Sie durch eine Lizenz lokal besitzen. Beachten Sie, dass der Azure-Hybridvorteil für SQL Server für die unternehmenskritische Dienstebene nur für Kunden verfügbar ist, die Enterprise Edition-Lizenzen besitzen.
- Wenn Sie die hochgradig virtualisierte Enterprise Edition mit Lizenzen pro Kern mit aktiver Software Assurance besitzen, erhalten Sie vier virtuelle Kerne in der universellen Dienstebene für jeden Kern, den Sie durch eine Lizenz lokal besitzen. Dies ist ein einzigartiger Virtualisierungsvorteil, der nur für Azure SQL-Datenbank verfügbar ist.

Die folgende Abbildung zeigt die auf virtuellen Kernen basierenden Optionen, die in jeder Dienstebene mit Azure-Hybridvorteil für SQL Server-Lizenzen verfügbar sind.

![Eine Abbildung mit einem Beispiel, das verdeutlicht, wie Sie den Wert Ihrer vorhandenen SQL-Serverlizenz mithilfe des Azure-Hybridvorteils maximieren können.](../media-drafts/5-sql-tradein-value.png)

Für SQL Server auf virtuellen Azure-Computern funktioniert der Azure-Hybridvorteil folgendermaßen:

- Wenn Sie die Enterprise Edition mit Lizenzen pro Kern mit aktiver Software Assurance besitzen, erhalten Sie einen Kern für SQL Server Enterprise Edition auf virtuellen Azure-Computern für jeden Kern, den Sie durch eine Lizenz lokal besitzen.
- Wenn Sie die Standard Edition mit Lizenzen pro Kern mit aktiver Software Assurance besitzen, erhalten Sie einen Kern für SQL Server Standard Edition auf virtuellen Azure-Computern für jeden Kern, den Sie durch eine Lizenz lokal besitzen.

Dies kann sich erheblich auf Ihre Ausgaben in Azure durch SQL Server-Workloads auswirken.

## <a name="use-devtest-subscription-offers"></a>Verwenden von Dev/Test-Abonnementangeboten

Die Angebote [Enterprise Dev/Test](https://azure.microsoft.com/offers/ms-azr-0148p/) und [Pay-As-You-Go Dev/Test](https://azure.microsoft.com/offers/ms-azr-0023p/) sind Vorteile, die Sie nutzen können, um Kosten in Ihren Nicht-Produktionsumgebungen zu sparen. Durch diesen Vorteil erhalten Sie verschiedene Rabatte, insbesondere für Windows-Workloads, sodass Lizenzgebühren und Kosten nur auf Basis der Linux-Rate für virtuelle Computer entstehen. Dies gilt ebenfalls für SQL Server und andere Microsoft-Software, die in Visual Studio-Abonnements (früher MSDN) enthalten ist. Für diesen Vorteil müssen einige Voraussetzungen erfüllt werden. Eine Voraussetzung ist, dass der Vorteil nur für Nicht-Produktionsworkloads gilt, und eine weitere ist, dass alle Benutzer dieser Umgebungen (mit Ausnahme von Testern) im Visual Studio-Abonnement abgedeckt sein müssen. Kurz gesagt können Sie für Nicht-Produktionsworkloads Kosten für Ihre Windows-, SQL-Server und sonstige Microsoft-Workloads für virtuelle Computer sparen.
Im Folgenden finden Sie die vollständigen Informationen zu jedem Angebot. Wenn Sie Kunde im Rahmen eines Enterprise Agreement sind, können Sie das Enterprise Dev/Test-Angebot nutzen. Wenn kein Enterprise Agreement vorliegt und Sie Pay-As-You-Go-Konten verwenden, können Sie das Pay-As-You-Go Dev/Test-Angebot nutzen.

## <a name="bring-your-own-sql-server-license"></a>Bring Your Own License (SQL Server)

Wenn Sie einen Kunden im Rahmen eines Enterprise Agreements und bereits über eine Investition in SQL Server-Lizenzen verfügen und diese durch die Verschiebung von Ressourcen in Azure frei geworden sind, können Sie **Bring Your Own License**-Images (BYOL) über den Azure Marketplace bereitstellen, um diese nicht verwendeten Lizenzen zu nutzen und Ihre Kosten für virtuelle Azure-Computer zu reduzieren. Dies war zuvor bereits möglich, indem ein virtueller Windows-Computer bereitgestellt und SQL Server manuell auf diesem installiert wurde. Dieses Verfahren erleichtert jedoch den Erstellungsprozess durch die Verwendung von durch Microsoft zertifizierten Images. Suchen Sie im Marketplace nach **BYOL**, um diese Images zu finden.

![BYOL für SQL Server in Azure](../media-drafts/5-byol-sql-server.png)

> [!IMPORTANT]
> Ein Enterprise Agreement-Abonnement ist erforderlich, um diese zertifizierten BYOL-Images zu verwenden.

## <a name="use-sql-server-developer-edition"></a>Verwenden von SQL Server Developer Edition

Vielen Benutzern ist nicht bekannt, dass SQL Server Developer Edition ein kostenloses Produkt ist, das jedoch **nicht für Produktionszwecke** gedacht ist. Developer Edition enthält die gleichen Features wie Enterprise Edition, für Nicht-Produktionsworkloads können Sie jedoch erheblich an Lizenzierungskosten einsparen.

Suchen Sie im Azure Marketplace nach SQL Server-Images für Developer Edition, und verwenden Sie diese für Entwicklungs- oder Testzwecke, um in diesen Fällen zusätzliche Kosten für SQL Server zu vermeiden. 

> [!TIP]
> Vollständige Informationen zur Lizenzierung finden Sie in den [Preisinformationen](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance).

## <a name="use-constrained-instance-sizes-for-database-workloads"></a>Verwenden von eingeschränkten Instanzgrößen für Datenbankworkloads 

Viele Kunden haben hohe Anforderungen an Arbeitsspeicher, Speicherplatz oder E/A-Bandbreite, besitzen jedoch wenige CPU-Kerne. Auf Grundlage dieser Anforderungen hat Microsoft die beliebtesten Größen für virtuelle Computer (DS, ES, GS und MS) in neuen Größen zur Verfügung gestellt, durch die die Anzahl der virtuellen CPUs auf die Hälfte oder sogar ein Viertel der ursprünglichen Größe des virtuellen Computers eingeschränkt wird, während gleich viel Arbeitsspeicher, Speicherplatz und E/A-Bandbreite beibehalten bleibt.

| Größe des virtuellen Computers | vCPUs | Arbeitsspeicher | Max. Anzahl Datenträger | Maximaler E/A-Durchsatz | SQL Server Enterprise-Lizenzierungskosten pro Jahr | Gesamtkosten pro Jahr (Compute und Lizenzierung) |
|---------|-------|--------|-----------|--------------------|-----------------------------------------------|---------------------------|
| Standard_DS14v2   | 16 | 112 GB | 32 | 51.200 IOPS oder 768 MB/s |           |           |
| Standard_DS14-4v2 | **4**  | 112 GB | 32 | 51.200 IOPS oder 768 MB/s | 75 % niedriger | 57 % niedriger |
| Standard_GS5      | 32 | 448    | 64 | 80.000 IOPS oder 2 GB/s   |           |           |
| Standard_GS5-8    | **8**  | 448    | 64 | 80.000 IOPS oder 2 GB/s   | 75 % niedriger | 42 % niedriger |

Da Datenbankprodukte wie SQL Server und Oracle pro CPU lizenziert werden, können Kunden die Lizenzierungskosten um bis zu 75 % senken und dennoch weiterhin die hohe Leistung nutzen, die ihre Datenbanken benötigen. 
