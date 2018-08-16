Virtuelle Computer müssen entsprechend für die Verarbeitung der erwarteten Größe angepasst werden. Ein virtueller Computer ohne die richtige Menge an Arbeitsspeicher oder CPU werden ein unter Last oder zu langsam ausgeführt werden, um effektiv zu sein. 

Wenn Sie einen virtuellen Computer erstellen, können Sie angeben einer _VM-Größe_ -Wert, der die Anzahl der computeressourcen bestimmt, die mit dem virtuellen Computer verwendet werden wird. Dies schließt die CPU, zur GPU sowie Speicher, die mit dem virtuellen Computer in Azure verfügbar sind.

Azure definiert einen Satz von [vordefinierte VM-Größen](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/sizes) für Linux und Windows wählen Sie auf Grundlage der erwarteten Nutzung. 

| Typ | Größen | Beschreibung |
|------|-------|-------------|
| Allgemeiner Zweck   | Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7 | Ausgewogenes Verhältnis von CPU zu Arbeitsspeicher. Ideal für Entwicklung und Tests, kleine bis mittlere Anwendungen und Datenlösungen. |
| Computeoptimiert | Fs, F | Hohes Verhältnis von CPU zu Arbeitsspeicher. Geeignet für Anwendungen, Network Appliances und Stapelverarbeitungsvorgänge mit mittlerer Auslastung. |
| Arbeitsspeicheroptimiert  | Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D   | Hohes Verhältnis von Speicher zu Kern. Hervorragend geeignet für relationale Datenbanken, mittlere bis große Caches und In-Memory-Analysen. |
| Speicheroptimiert | Ls | Datenträgerdurchsatz und -E/A auf hohem Niveau. Ideal für big Data, SQL- und NoSQL Datenbanken. |
| GPU-optimiert | NV, NC | Spezialisierte virtuelle Computer für intensives Grafikrendering und intensive Videobearbeitung. |
| Hohe Leistung | H, A8-11 | Unsere virtuellen Computer mit den leistungsfähigsten CPUs, die optional über Netzwerkschnittstellen mit hohem Durchsatz (RDMA) verfügen. | 

Die verfügbaren Größen ändert sich je nach der Region erstellen Sie den virtuellen Computer im. Sie erhalten eine Liste der verfügbaren Größen mithilfe der `vm list-sizes` , versuchen Sie dies in der Cloud Shell eingeben:

```azurecli
az vm list-sizes --location eastus --output table
```

Hier ist eine verkürzte Antwort für `eastus`:

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

Wenn wir unsere VM - erstellt haben, damit Azure eine allgemeine Standardgröße von ausgewählt, legen wir nicht haben eine Größe `Standard_DS1_v2`. Allerdings können wir die Größe angeben, als Teil der `vm create` Befehl mithilfe der `--size` Parameter.

```azurecli
az vm create --resource-group ExerciseResources --name SampleVM \
  --image Debian --admin-username aldis --generate-ssh-keys --verbose \
  --size "Standard_DS5_v2"
```

## <a name="resizing-an-existing-vm"></a>Ändern der Größe eines vorhandenen virtuellen Computers
Wir können auch einen vorhandenen virtuellen Computer ändern, wenn die Workload ändert oder wenn es nicht ordnungsgemäß bei der Erstellung angepasst wurde. Vor der Größenänderung ein angefordert wird, müssen wir überprüfen, um festzustellen, ob die gewünschte Größe im Cluster verfügbar ist, die der virtuellen Computer gehört. Wir erreichen dies mit der `vm list-vm-resize-options` Befehl:

```azurecli
az vm list-vm-resize-options --resource-group ExerciseResources --name SampleVM --output table
```

Dadurch wird eine Liste aller möglichen Größe-Konfigurationen zur Verfügung, in der Ressourcengruppe zurückgegeben. Wenn die Größe, sollten nicht in Ihrem Cluster verfügbar ist, aber _ist_ in der Region verfügbar ist, können wir [Aufheben der Zuordnung der VM](https://docs.microsoft.com/en-us/cli/azure/vm?view=azure-cli-latest#az-vm-deallocate). Mit diesem Befehl wird die ausgeführte VM zu beenden und ohne Verlust von Ressourcen aus dem aktuellen Cluster entfernt. Klicken Sie dann können wir sie ändern den virtuellen Computer in einem neuen Cluster erneut erstellt wird, in denen die Größenkonfiguration verfügbar ist.

Zum Ändern der Größe eines virtuellen Computers verwenden wir die `vm resize` Befehl. Unsere aktuelle VM-Ressourcen z. B. lassen Sie uns auf das absolute Minimum zu reduzieren: 2G Arbeitsspeicher 1 CPU-Kerne und 4G der Speicherplatz auf dem Datenträger. Geben Sie diesen Befehl in Cloud Shell ein:

```azurecli
az vm resize --resource-group ExerciseResources --name SampleVM --size "Standard_B1ms"
```

Mit diesem Befehl dauert einige Minuten, bis die Ressourcen des virtuellen Computers zu reduzieren, und anschließend wird eine neue JSON-Konfiguration zurückgegeben.