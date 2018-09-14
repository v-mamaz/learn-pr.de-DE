Ihr Server benötigt genügend Ressourcen zum Verarbeiten der täglichen Nachfrage. Eine typische Strategie ist, wählen Sie eine VM-Größe, bei der Erstellung, die für den typischen arbeitsauslastungen ausreichend ist, und klicken Sie dann ändern Sie die Größe bei wechselnden.

Im Szenario Unternehmen Spielzeug wäre diese Strategie nützlich, um die Ressourcen für Ihr Mittel-und langfristige Wachstum zu verwalten. Sie können die Größe Ihres virtuellen Computers, um die hinzugefügten Nachfrage zu bewältigen, während Ihr Business wächst erhöhen.

## <a name="what-is-virtual-machine-size"></a>Was ist die Größe des virtuellen Computers?

Die _Größe_ eines virtuellen Computers ist ein Maß für die CPU, Arbeitsspeicher, Datenträger und erwartete Netzwerkbandbreite. Virtuelle Computer sind in einer vorbestimmten Anzahl von Größen verfügbar. Z. B. die **Standard_F32s_v2** Größe hat, 32 virtuellen CPUs, 64 GiB Arbeitsspeicher, einer 256 GiB lokalen SSD-Speicher und 14.000 MBit/s der erwartete Netzwerkbandbreite.

Wenn Sie einen neuen virtuellen Computer in Azure erstellen, müssen Sie eine Größe auswählen. Größere Kosten mehr an. Ziel ist es, eine Größe auswählen, die Ihre Workload ohne Konfiguration leistungsfähiger, als Sie benötigen verarbeiten kann.

## <a name="what-is-virtual-machine-type"></a>Was ist der Typ des virtuellen Computers?

Die _Typ_ eines virtuellen Computers wird die arbeitsauslastung für die der virtuelle Computer optimiert wurde. Einige virtuelle Computer sind z. B. CPU-Intensive Aufgaben, z. B. einen Webserver bestimmt. Andere beabsichtigen für Aufträge sich auf speicherlösungen konzentrieren, wie eine Datenbank ausgeführt.

Es gibt _Typen_ , die jede Core Hardwarekomponente in einer modernen Computers entsprechen: **compute**, **Arbeitsspeicher**, **Storage**, und  **GPU**. Es gibt auch eine **allgemeiner** Geben Sie bei Bedarf eine ausgewogene Kombination von Ressourcen. Die folgende Tabelle enthält die Typen und die VM-Größen, die Teil jedes Typs, zusammen mit einer kurzen Beschreibung der angestrebten arbeitsauslastung sind.

|Typ|Größen|Beschreibung|
|---|---|---|
|Allgemeiner Zweck|B, Ds_v3, D_v3, einige DS_v2, einige D_v2, A_v2|Allgemeine Computer haben ein ausgewogene Verhältnis von CPU zu Arbeitsspeicher. Allgemeine Computer eignen sich für Test- oder Entwicklungszwecken mit Servern, kleine bis mittlere Datenbanken sowie Webserver mit geringem bis mittlerem Datenverkehr zu.|
|Computeoptimiert|Fs_v2, Fs, F|Optimiert für Compute – virtuelle Computer haben ein höheres Verhältnis von CPU zu Arbeitsspeicher als allgemeines Computer für Aufgaben, die zusätzliche verarbeitungsleistung, z. B. Application Server, Netzwerkgeräte oder Webserver mittlerer Auslastung erfordern.|
|Arbeitsspeicheroptimiert|Es_v3 "," E_v3 "," M "," GS "," G "," einige DS_v2 "," einige D_v2|Speicheroptimierte virtuelle Computer haben ein hohes Verhältnis von Speicher zu CPU. Diese Computer eignen sich für relationale Datenbankserver, Server, die erfordern, oder führen Sie einen Großteil der Zwischenspeicherung oder Server, die in-Memory-Analysen ausführen.|
|Speicheroptimiert|Ls|Diese virtuellen Computer werden konfiguriert, hoher Durchsatz und e/a-Vorgänge gemäß der big Data und SQL und NoSQL-Datenbanken.|
|GPU|NV, NC, NC_v2, NC_v3, ND|GPU-Computer sind für Aufgaben wie z. B. komplexe Grafikrendering oder videobearbeitung, sowie das Modelltraining und Rückschlüsse (ND-Serie) mit deep Learning spezialisiert. Sie können einer oder mehreren GPUs für diese Computer auswählen.|
|High Performance Computing|H|Der schnellsten, sind die leistungsstärksten CPUs in diesen virtuellen Computern verfügbar. Sie können auch die Netzwerkschnittstellen von hohem Durchsatz (RDMA) hinzufügen.|

## <a name="clusters"></a>Cluster

Die physischen Serverhardware in Azure-Regionen wird in Clustern gruppiert. Jeder Cluster kann mehrere verschiedene VM-Größen, die basierend auf der physischen Hardware unterstützen.

Wenn Sie einen virtuellen Computer erstellen und eine bestimmte Größe entscheiden, wird der virtuelle Computer mit einem geeigneten Hardware-Cluster für die Größe bereitgestellt. Auch wenn Sie virtuelle Computer nach der Erstellung die Größe ändern, können die Optionen beim Ändern der Größe von dem Hardwarecluster für die anfängliche Größe ausgewählt eingeschränkt werden.

## <a name="what-is-vertical-scaling"></a>Was ist die vertikale Skalierung?

_Die vertikale Skalierung_ versteht man das Ändern der _Größe_ eines virtuellen Computers. Sie können _zentral hochskalieren_ durch Auswahl einer leistungsfähigeren Größe, höhere Nachfrage zu behandeln oder _zentral Herunterskalieren,_ belegen weniger Ressourcen und Kosten reduzieren. Die folgende Abbildung zeigt ein Beispiel zum Ändern der Größe eines virtuellen Computers.

![Eine Abbildung, zeigt der vertikalen und horizontalen Herunterskalieren einer VM so ändern Sie die Leistungsfähigkeit.](../media/2-ScaleUpDown.png)

Sie können einen virtuellen Computer mithilfe von Azure-Portal, Azure PowerShell oder der Azure CLI ändern.

### <a name="resize-in-the-portal"></a>Ändern der Größe im portal

Im Azure-Portal können Sie die Größe ein virtuellen Computers ändern, indem Sie den virtuellen Computer auswählen, auf die **Größe** Eintrag, und wählen einen Eintrag aus der **wählen Sie eine Größe** Blatt. 

Wenn der virtuelle Computer zum Zeitpunkt ausgeführt wird, hängen die verfügbaren Größen, die Sie aus den verfügbaren Größen in Ihrer Region. Wird nur angezeigt, ändern Sie die Optionen, die kompatibel mit dem gleichen Hardwarecluster, das den virtuellen Computer ausgeführt wird, Größe Dies wird mitunter bezeichnet ein *Größe Familie*. Wenn Sie eine neue Größe auswählen, während die virtuelle Maschine ausgeführt wird, wird der virtuelle Computer automatisch neu gestartet werden zum Anwenden der neuen Größe.

Ist die Größe, die gesuchte nicht im Portal angezeigt, wenn der virtuelle Computer ausgeführt wird, können Sie Herunterfahren, bis dem virtuellen Computer, um weitere Optionen anzuzeigen ist. Wenn der Computer befindet sich in der **beendet (Zuordnung aufgehoben)** aufweist, können andere Hardware in der gleichen Region Größen aus.

### <a name="resize-with-powershell"></a>Ändern der Größe mit PowerShell

Sie können PowerShell verwenden, führen Sie die vertikale Skalierung interaktiv oder mit Skripts. Skripts sind gut für komplexe Szenarien. beispielsweise wenn Sie mehrere virtuelle Computer gleichzeitig die Größe ändern möchten. Sie sind auch praktisch, wenn Sie zum vornehmen der Größenänderung während der arbeitsfreien Zeit, um Störungen für die Benutzer zu vermeiden müssen.

Das folgende Cmdlet listet VM-Größen, von der gleichen größenfamilie als die aktuelle Hardware:

```PowerShell
Get-AzureRmVMSize -ResourceGroupName "myResourceGroup" -VMName "MyVM"
```

Wenn die gewünschte Größe angezeigt wird, verwenden Sie das folgende Cmdlet, um die Größe des virtuellen Computers zu ändern:

```PowerShell
$vm = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -VMName "MyVM"
$vm.HardwareProfile.VmSize = "<newVMsize>"
Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
```

Wenn die gewünschte Größe nicht mit dem Computer angezeigt wird, verwenden Sie die folgenden Befehle zum Aufheben der Zuordnung der VM, ändern Sie die Größe des Computers und starten Sie den Computer erneut ein:

```PowerShell
Stop-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "MyVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -VMName "MyVM"
$vm.HardwareProfile.VmSize = "<newVMSize>"
Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "MyVM"
```

Virtuelle Computer in Azure kann geändert werden, nach Bedarf, um die Leistung zu erhöhen oder Verringern der Kosten. Ändern der Größe des manuellen durchführen, mit dem Portal oder ein Skript ist nützlich, schrittweise Geschäftswachstum Handle oder, wenn Sie über eine Änderung bei Bedarf vorab wissen. In diesem Szenario Spielzeughersteller können sie zentral hochskalieren vor einem Feiertag behandeln die Spitze in der Anforderung, und klicken Sie dann später zentral Herunterskalieren.
