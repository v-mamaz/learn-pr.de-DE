Die Größe virtueller Computer muss auf die zu erwartende Verarbeitung abgestimmt werden. Ein virtueller Computer, der nicht über ausreichend Arbeitsspeicher oder CPU-Leistung verfügt, kann überlastet oder so langsam werden, dass er nicht effektiv ist. 

Wenn Sie einen virtuellen Computer erstellen, können Sie einen Wert für die _VM-Größe_ angeben, der die Menge an Computeressourcen festlegt, die diesem virtuellen Computer zugewiesen werden. Hierzu gehören CPU-, GPU- und Arbeitsspeicherkapazitäten, die dem virtuellen Computer von Azure zur Verfügung gestellt werden.

Azure enthält eine Reihe von [vordefinierten VM-Größen](https://docs.microsoft.com/azure/virtual-machines/linux/sizes) für Linux und Windows, aus denen Sie basierend auf der erwarteten Nutzung auswählen können. 

| Typ | Größen | Beschreibung |
|------|-------|-------------|
| Allgemeiner Zweck   | Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7 | Ausgewogenes Verhältnis von CPU zu Arbeitsspeicher. Ideal für Entwicklung und Tests, kleine bis mittlere Anwendungen und Datenlösungen. |
| Computeoptimiert | Fs, F | Mehr CPU als Arbeitsspeicher. Geeignet für Anwendungen, Network Appliances und Stapelverarbeitungsvorgänge mit mittlerer Auslastung. |
| Arbeitsspeicheroptimiert  | Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D   | Mehr Arbeitsspeicher als Kerne. Hervorragend geeignet für relationale Datenbanken, mittlere bis große Caches und In-Memory-Analysen. |
| Speicheroptimiert | Ls | Datenträgerdurchsatz und -E/A auf hohem Niveau. Ideal für Big Data sowie SQL- und NoSQL-Datenbanken. |
| GPU-optimiert | NV, NC | Spezialisierte virtuelle Computer für ressourcenintensives Grafikrendering und ressourcenintensive Videobearbeitung. |
| Hohe Leistung | H, A8-11 | Unsere leistungsfähigsten CPU-VMs, die optional über Netzwerkschnittstellen mit hohem Durchsatz (RDMA) verfügen. | 

Die verfügbaren Größen hängen von der Region ab, in der Sie den virtuellen Computer erstellen. Mit dem Befehl „`vm list-sizes`“ können Sie eine Liste der verfügbaren Größen abrufen. Geben Sie Folgendes in Azure Cloud Shell ein:

```azurecli
az vm list-sizes --location eastus --output table
```

Hier finden Sie eine gekürzte Antwort für „`eastus`:

```
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          2048  Standard_B1ms                         1           1047552                    4096
                 2          1024  Standard_B1s                          1           1047552                    2048
                 4          8192  Standard_B2ms                         2           1047552                   16384
                 4          4096  Standard_B2s                          2           1047552                    8192
                 8         16384  Standard_B4ms                         4           1047552                   32768
                16         32768  Standard_B8ms                         8           1047552                   65536
                 4          3584  Standard_DS1_v2                       1           1047552                    7168
                 8          7168  Standard_DS2_v2                       2           1047552                   14336
                16         14336  Standard_DS3_v2                       4           1047552                   28672
                32         28672  Standard_DS4_v2                       8           1047552                   57344
                64         57344  Standard_DS5_v2                      16           1047552                  114688
        ....
                64       3891200  Standard_M128-32ms                  128           1047552                 4096000
                64       3891200  Standard_M128-64ms                  128           1047552                 4096000
                64       3891200  Standard_M128ms                     128           1047552                 4096000
                64       2048000  Standard_M128s                      128           1047552                 4096000
                64       1024000  Standard_M64                         64           1047552                 8192000
                64       1792000  Standard_M64m                        64           1047552                 8192000
                64       2048000  Standard_M128                       128           1047552                16384000
                64       3891200  Standard_M128m                      128           1047552                16384000
```

Wir haben beim Erstellen des virtuellen Computers keine Größe angegeben, daher hat Azure eine allgemeine Standardgröße von „`Standard_DS1_v2`“ für uns ausgewählt. Wir können jedoch die Größe mithilfe des `--size`-Parameters im `vm create`-Befehl angeben. Sie können z.B. mit dem folgenden Befehl eine VM mit 16 Kernen erstellen:

```azurecli
az vm create --resource-group ExerciseResources --name SampleVM \
  --image Debian --admin-username aldis --generate-ssh-keys --verbose \
  --size "Standard_DS5_v2"
```

> [!WARNING]
> Je nach Abonnement können Sie [unterschiedlich viele und unterschiedlich große](https://docs.microsoft.com/en-us/azure/azure-subscription-service-limits) Ressourcen erstellen. Im Pay-as-you-go-Abonnement können Sie beispielsweise bis zu **20 virtuelle CPUs** erstellen und in einem kostenlosen Abonnement nur **4 CPUs**. Die Azure CLI meldet Ihnen, wenn Sie das Kontingent überschritten haben und gibt einen **Kontingent überschritten**-Fehler aus. Wenn dieser Fehler beim Erstellen einer Architektur ausgegeben wird, können Sie eine [kostenlose Onlineanforderung](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-quota-errors) übermitteln, um das Kontingent Ihres bezahlten Abonnements auf bis zu 10.000 vCPUs zu erhöhen. 

## <a name="resizing-an-existing-vm"></a>Ändern der Größe eines vorhandenen virtuellen Computers
Wir können die Größe eines vorhandenen virtuellen Computers auch ändern, wenn sich die Workload ändert oder die Größe während der Erstellung falsch festgelegt wurde. Bevor eine Größenänderung angefordert wird, müssen wir überprüfen, ob die gewünschte Größe in dem Cluster vorhanden ist, zu dem unser virtueller Computer gehört. Hierfür können wir den Befehl „`vm list-vm-resize-options`“ verwenden:

```azurecli
az vm list-vm-resize-options --resource-group ExerciseResources --name SampleVM --output table
```

Dieser Befehl gibt eine Liste aller möglichen Größenkonfigurationen zurück, die in der Ressourcengruppe verfügbar sind. Wenn die gewünschte Größe zwar nicht in unserem Cluster, _aber_ in der Region verfügbar ist, können wir die [Zuordnung des virtuellen Computers aufheben](https://docs.microsoft.com/cli/azure/vm?view=azure-cli-latest#az-vm-deallocate). Dieser Befehl hält den ausgeführten virtuellen Computer an und entfernt ihn aus dem aktuellen Cluster, ohne dass dabei Ressourcen verloren gehen. Dann können wir die Größe ändern. Dadurch wird der virtuelle Computer in einem neuen Cluster erneut erstellt, in dem die Größenkonfiguration verfügbar ist.

Zum Ändern der Größe eines virtuellen Computers verwenden wir den Befehl „`vm resize`“. Ein Beispiel: Wir möchten unsere aktuellen VM-Ressourcen auf das absolute Minimum reduzieren: 2 GB Arbeitsspeicher, 1 CPU-Kern, 4 GB Speicherplatz auf dem Datenträger. Geben Sie folgenden Befehl in Cloud Shell ein:

```azurecli
az vm resize --resource-group ExerciseResources --name SampleVM --size "Standard_B1ms"
```

Es dauert einige Minuten, bis der Befehl die Ressourcen des virtuellen Computers reduziert hat. Sobald dieser Vorgang abgeschlossen ist, gibt der Befehl eine neue JSON-Konfiguration zurück.