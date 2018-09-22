Wir haben die Größe einiger der Uploads unterschätzt, weshalb unser Datenträger für Uploads keinen Speicherplatz mehr hat. Sie beschließen, den Speicherplatz zu verdoppeln und ihn von 64 GB auf 128 GB zu vergrößern.

## <a name="resize-the-data-disk"></a>Ändern der Größe des Datenträgers

Zum Ändern der Größe eines Datenträgers benötigen wir die ID oder den Namen des Datenträgers. In diesem Fall kennen wir den Namen (uploadDataDisk1) bereits. Aber für den Fall, dass Sie sich nicht daran erinnern oder er von jemand anderem festgelegt wurde, können wir mit dem Befehl `az disk list` eine Liste der Datenträger abrufen.

1. Beginnen Sie, indem Sie eine Liste der verwalteten Datenträger in der Ressourcengruppe abrufen. Dies kann auch andere Datenträger umfassen, wenn in einer einzelnen Ressourcengruppe mehrere VMs vorhanden sind. Bei unserem Beispiel sollte es nur unseren Webserver geben.

    ```azurecli
    az disk list \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

1. Beenden Sie als Nächstes die VM, und heben Sie mit `az vm deallocate` ihre Zuordnung auf. 

    ```azurecli
    az vm deallocate --name support-web-vm01
    ```
1. Nun können wir die Größe des Datenträgers mit dem Befehl `az disk update` ändern.

    ```azurecli
    az disk update --name uploadDataDisk1 --size-gb 128
    ```
    
1. Starten Sie die VM nach Abschluss der Größenänderung neu.

    ```azurecli
    az vm start --name support-web-vm01
    ```

## <a name="expand-the-disk-partition"></a>Erweitern der Datenträgerpartition

Der letzte Schritt besteht darin, das Betriebssystem über den verfügbaren Speicherplatz zu informieren. Genau wie bei den vorherigen Partitionierungs- und Formatierungsschritten ist dieser Prozess für die Erweiterung lokaler Datenträger identisch. 

1. Rufen Sie zunächst die öffentliche IP-Adresse Ihrer VM ab. Da sie neu gestartet wurde, hat sie sich wahrscheinlich geändert. Versuchen wir es diesmal mit einem anderen Ansatz, indem wir `az vm show` mit einem Filter verwenden, um die öffentliche IP-Adresse zurückzugeben.

    > [!TIP]
    > IP-Adressen sind standardmäßig dynamisch. Azure DNS gleicht die Änderung der IP-Adresse automatisch aus, oder Sie können das Verhalten ändern, indem Sie statische IP-Adressen verwenden.

    ```azurecli
    az vm show --name support-web-vm01 -d --query [publicIps] --o tsv
    ```
    
1. Verbinden Sie sich per SSH mit der Linux-VM. Sie müssen die richtige IP-Adresse angeben.

    ```bash
    ssh azureuser@40.76.193.249
    ```

1. Heben Sie die Bereitstellung des Datenträgers auf. Zur Erinnerung: Der Name war `/dev/sdc1`.

    ```bash
    sudo umount /dev/sdc1
    ```

1. Starten Sie `parted` in einer Shell mit erhöhten Rechten.

    ```bash
    sudo parted /dev/sdc
    ```
    
1. Erweitern Sie die Partition mit dem Befehl `resizepart`. Geben Sie Partition 1 und die neue Größe (128 GB) ein.

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [64GB]? 128GB
    ```

    > [!WARNING]
    > Achten Sie auf die Größe. Die Größenänderung der Partition ermöglicht Ihnen, auch eine Partition zu verkleinern, was wahrscheinlich zu Datenverlust führen wird.
    
1. Beenden Sie das Tool durch Eingabe von `quit`.

1. Das Partitionierungstool stellt das Laufwerk automatisch _erneut bereit_. Heben Sie deshalb die Bereitstellung erneut auf, damit es formatiert werden kann.

    ```bash
    sudo umount /dev/sdc1
    ```
    
1. Überprüfen Sie die Partitionskonsistenz mit `e2fsck`. Dieser Schritt ist absolut notwendig, aber auch immer dann eine gute Idee, wenn Sie Größen auf einem Datenträgervolume ändern.

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

1. Ändern Sie die Größe des Dateisystems mit `resize2fs`.

    ```bash
    sudo resize2fs /dev/sdc1
    ```

1. Stellen Sie das Laufwerk schließlich wieder am Bereitstellungspunkt bereit.

    ```bash
    sudo mount /dev/sdc1 /uploads
    ```

Verwenden Sie `df -h`, um zu überprüfen, ob die Größe des Betriebssystem-Datenträgers geändert wurde. Sie sollte nun mit 128 GB angezeigt werden.
