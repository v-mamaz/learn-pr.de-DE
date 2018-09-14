Anwendungen und Dienste müssen häufig nach Bedarf skaliert werden. Bei virtuellen Computern bedeutet dies horizontales hochskalieren oder das Erstellen zusätzlicher Instanzen an. Erstellen von Datenträgern für neue Instanzen können manuell eine Belastung für Azure-Administratoren platzieren. Wir können stattdessen **verwaltete Datenträger** reduzieren Sie die Verwaltung erforderlich, um neue Datenträger erstellen.

Handle-Datenträgern für Sie "hinter den Kulissen" verwaltet. Geben Sie den Datenträger und die Größe des Datenträgers, die Sie benötigen, und Azure erstellt und verwaltet die Datenträger für Sie. 

Wenn Sie verwaltete Datenträger verwenden, einen anderen Datenträgertyp kann Sie mit dem Namen **standard-SSD**.

## <a name="standard-ssds"></a>Standard-SSDs

Wenn Sie sich, mit nicht verwalteten Datenträgern erinnern können Sie über zwei verschiedene Datenträgertypen: standard Festplattenlaufwerke (HDDs), und Premium Solid-State-Laufwerken (SSDs).

Wenn Sie verwaltete Datenträger verwenden, können Sie einen dritten Typ des Datenträgers: standard, SSDs. Dieser Datenträgertyp befindet sich zwischen standard HDDs und SSDs mit Premium hinsichtlich der Leistung und Kosten.

Sie können standardmäßige SSDs verwenden, mit jeder VM-Größe, einschließlich der VM-Größen, die nicht Storage Premium unterstützen. In der Tat ist die Verwendung von standard-SSDs die einzige Möglichkeit zur Verwendung von SSDs mit diesen VMs.

## <a name="managed-disks-in-availability-sets"></a>Verwaltete Datenträger in Verfügbarkeitsgruppen

In einigen Fällen verwenden Sie mehrere virtuelle Computer zum Hosten der Anwendung aus, um die ansteigende Last zu bewältigen.

Sie können Ihre virtuellen Computer in Platzieren einer **verfügbarkeitsgruppe** reduzieren die Wahrscheinlichkeit, dass Kunden, die bei einem Ausfall. Verwenden eine verfügbarkeitsgruppe, werden Ihre virtuellen Computer über Fehlerdomänen hinweg verteilt. Eine Fehlerdomäne ist eine logische Gruppe von zugrunde liegender Hardware, der gemeinsam eine Stromquelle und einen Netzwerkswitch, ähnlich einem Rack in einem lokalen Rechenzentrum. Wenn Sie VMs in einer Verfügbarkeitsgruppe erstellen, werden Ihre VMs von der Azure-Plattform automatisch auf diese Fehlerdomänen verteilt. Durch diese Trennung in der Azure-Datencenter wird sichergestellt, dass kein single Point of Failure für alle virtuellen Computer in der verfügbarkeitsgruppe vorhanden ist.

Wenn Sie verwaltete Datenträger verwenden, erstellt Azure automatisch sicher, dass jede virtuelle Festplatte in der gleichen Fehlerdomäne als einem virtuellen Computer platziert wird. Diese Garantie wird entfernt, die Möglichkeit, dass die Konfiguration des Speicherkontos, eine einzelne Fehlerquelle enthalten kann. Es ist keine Möglichkeit, diese Trennung zu gewährleisten, wenn Sie nicht verwaltete Datenträger verwenden.

## <a name="choosing-managed-disks"></a>Auswählen von verwalteten Datenträgern

Es gibt einige Aspekte, die die Entscheidung, ob der Datenträger Ihrer virtuellen Computer als verwaltete Datenträger anstelle von nicht verwalteten Datenträgern erstellen beeinträchtigen können.

**Möchten Sie die Kontrolle über die Storage-Konten in Ihrem Abonnement?**

Verwaltete Datenträger sind leicht zu verwaltende, aber Sie fühlen sich möglicherweise, dass Sie Speicher optimieren können, oder Verwalten von Kosten, die eine bessere Kontrolle des Storage-Konten.

**Möchten Sie die standard-SSDs verwenden?** 

Wenn Sie möchten die SSDs mit einer VM-Größe zu verwenden, die Storage Premium nicht unterstützt, müssen Sie verwaltete Datenträger auswählen.

**Sind die virtuellen Computer in einer verfügbarkeitsgruppe?** 

Es wird dringend empfohlen, verwaltete Datenträger verwenden, um die Stabilität zu optimieren, wenn Ihre VMs einer verfügbarkeitsgruppe angehören.

## <a name="migrating-to-managed-disks"></a>Migrieren zu managed disks

Sie können Ihre nicht verwalteten Datenträger in verwaltete Datenträger konvertieren, zu einem beliebigen Zeitpunkt mit einer dieser beiden Methoden:

- Über das Azure-Portal. Klicken Sie auf der Seite Datenträger der VM Einstellungen finden Sie die **Migrieren zu managed Disks** Tool. Dieser Prozess beenden des virtuellen Computers, migrieren die Datenträger, und wiederholen Sie den virtuellen Computer für Sie. Es werden eine dienstunterbrechung auf dem virtuellen Computer auftreten, während die Konvertierung stattfindet.
- Verwenden von Azure PowerShell. Sie können die `ConvertTo-AzureRmVMManagedDisk` Cmdlet, um die Migration auszuführen. Wenn Sie diese Methode auswählen, müssen Sie beenden und starten den virtuellen Computer selbst.
  
> [!Note]
> Bedenken Sie, dass die Migration von nicht verwalteten Datenträgern in verwaltete Datenträger nicht rückgängig gemacht werden. Darüber hinaus wird das ursprüngliche Speicherkonto des virtuellen Computers nicht automatisch gelöscht. Sie müssen so löschen Sie die ursprüngliche VHD-Blobs, um unerwünschte Kosten zu vermeiden. 

Verwaltete Datenträger der Verwaltungsaufwand reduziert, und haben einige Funktionen, z. B. standard SSDs zu, die nicht für nicht verwaltete Datenträger zur Verfügung stehen.
