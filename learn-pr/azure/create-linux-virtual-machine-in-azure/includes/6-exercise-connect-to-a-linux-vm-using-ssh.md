Der virtuelle Linux-Computer wurde bereitgestellt und wird ausgeführt, aber noch nicht für die Arbeit konfiguriert. Stellen wir eine Verbindung mit SSH her, und konfigurieren wir Apache, damit wir über einen Webserver verfügen, der ausgeführt wird.

## <a name="connect-to-the-vm-with-ssh"></a>Herstellen einer Verbindung mit dem virtuellen Computer mit SSH

Zum Herstellen der Verbindung eines virtuellen Azure-Computers mit einem SSH-Client benötigen Sie Folgendes:

- SSH-Clientsoftware (in den meisten modernen Betriebssystemen vorhanden)
- Die öffentliche IP-Adresse des virtuellen Computers (oder die private, wenn der virtuelle Computer dafür konfiguriert ist, eine Verbindung mit Ihrem Netzwerk herzustellen)

### <a name="get-the-public-ip-address"></a>Abrufen der öffentlichen IP-Adresse

1. Stellen Sie im [Azure-Portal](https://portal.azure.com?azure-portal=true) sicher, dass der Bereich **Übersicht** für den zuvor erstellten virtuellen Computer geöffnet ist. Sie finden den virtuellen Computer unter **Alle Ressourcen**, falls Sie diesen öffnen müssen. Im Bereich „Übersicht“ finden Sie zahlreiche Informationen zum virtuellen Computer.

    - Sie können sehen, ob er ausgeführt wird
    - Sie können ihn beenden oder neu starten
    - Sie können die öffentliche IP-Adresse abrufen, um eine Verbindung mit dem virtuellen Computer herzustellen
    - Sie können die Aktivität von CPU, Festplatte und Netzwerk anzeigen

1. Klicken Sie oben im Bereich auf die Schaltfläche **Verbinden**.

1. Notieren Sie sich die Einstellungen für die **IP-Adresse** und die **Portnummer** auf dem Blatt **Verbindung mit virtuellem Computer herstellen**. Auf der Registerkarte **SSH** finden Sie auch den Befehl, den Sie lokal ausführen müssen, um eine Verbindung mit dem virtuellen Computer herzustellen. Kopieren Sie diesen in die Zwischenablage.

## <a name="connect-with-ssh"></a>Verbinden mit SSH

1. Fügen Sie der Befehlszeile, die Sie aus der Registerkarte "SSH" in Azure Cloud Shell abgerufen haben. Es sollte in etwa wie folgt aussehen; Sie müssen jedoch eine andere IP-Adresse (und möglicherweise einen anderen Benutzernamen bei Verwendung von nicht **Jim**!):

    ```bash
    ssh jim@137.117.101.249
    ```

1. Mit diesem Befehl wird eine Secure Shell-Verbindung öffnen, und platzieren Sie an einer herkömmlichen Shell-Eingabeaufforderung für Linux.

1. Führen Sie einige Linux-Befehle aus
    - `ls -la /`, um den Stamm des Datenträgers anzuzeigen
    - `ps -l`, um alle ausgeführten Prozesse anzuzeigen
    - `dmesg`, um alle Kernelnachrichten aufzulisten
    - `lsblk`, um alle Blockgeräte aufzulisten. Hier werden Ihre Laufwerke angezeigt

Interessanter ist das, was in der Liste der Laufwerke _fehlt_. Beachten Sie, dass unser **Daten**laufwerk (`sdc`) zwar vorhanden, nicht aber im Dateisystem bereitgestellt ist. Azure hat eine VHD hinzugefügt, aber nicht initialisiert.

## <a name="initialize-data-disks"></a>Initialisieren von Laufwerken

Alle zusätzlichen Laufwerke, die Sie neu erstellen, müssen initialisiert und formatiert werden. Die Verfahrensweise für diesen Vorgang ist identisch mit einer physischen Festplatte:

1. Identifizieren Sie zuerst den Datenträger. Dies ist weiter oben erfolgt. Außerdem können Sie `dmesg | grep SCSI`, die werden alle Nachrichten aus dem Kernel für SCSI-Geräte aufgelistet.

1. Sobald Sie das Laufwerk (`sdc`) kennen, das initialisiert werden muss, können Sie `fdisk` zu diesem Zweck verwenden. Sie müssen zum Ausführen des Befehls mit `sudo` , und geben Sie den Datenträger, die Sie möchten die Partition:

    ```bash
    sudo fdisk /dev/sdc
    ```
1. Verwenden Sie den Befehl `n`, um eine neue Partition hinzuzufügen. In diesem Beispiel wählen wir auch **p** für eine primäre partition, und akzeptieren Sie die übrigen Standardwerte. Die Ausgabe entspricht etwa folgendem Beispiel:   

    ```output
    Device does not contain a recognized partition table.
    Created a new DOS disklabel with disk identifier 0x1f2d0c46.

    Command (m for help): n
    Partition type
       p   primary (0 primary, 0 extended, 4 free)
       e   extended (container for logical partitions)
    Select (default p): p
    Partition number (1-4, default 1): 1
    First sector (2048-2145386495, default 2048):
    Last sector, +sectors or +size{K,M,G,T,P} (2048-2145386495, default 2145386495):

    Created a new partition 1 of type 'Linux' and of size 1023 GiB.
    ```

1. Geben Sie die Partitionstabelle mit dem Befehl `p` aus. Das sollte in etwa so aussehen:

    ```output
    Disk /dev/sdc: 1023 GiB, 1098437885952 bytes, 2145386496 sectors
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 4096 bytes
    I/O size (minimum/optimal): 4096 bytes / 4096 bytes
    Disklabel type: dos
    Disk identifier: 0x1f2d0c46

    Device     Boot Start        End    Sectors  Size Id Type
    /dev/sdc1        2048 2145386495 2145384448 1023G 83 Linux
    ```

1. Schreiben Sie die Änderungen mit dem Befehl `w`. Dadurch wird das Tool beendet.

1. Im nächsten Schritt schreiben Sie jetzt mit dem Befehl `mkfs` ein Dateisystem auf die Partition. Wir müssen den Namen und Gerätename Datei angeben, die wir aus haben die `fdisk` Ausgabe:
    - Übergeben Sie `-t ext4`, um ein _ext4_-Dateisystem zu erstellen.
    - Der Gerätename ist `/dev/sdc`.

    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
    
    Die Ausführung dieses Befehls kann einige Minuten dauern.

    ```output
    mke2fs 1.44.1 (24-Mar-2018)
    Discarding device blocks: done
    Creating filesystem with 268173056 4k blocks and 67043328 inodes
    Filesystem UUID: e311c905-e0d9-43ab-af63-7f4ee4ef108e
    Superblock backups stored on blocks:
            32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
            4096000, 7962624, 11239424, 20480000, 23887872, 71663616, 78675968,
            102400000, 214990848

    Allocating group tables: done
    Writing inode tables: done
    Creating journal (262144 blocks): done
    Writing superblocks and filesystem accounting information: done
    ```

1. Als Nächstes erstellen Sie ein Verzeichnis, die wir als unser Bereitstellungspunkt verwenden. Angenommen, wir haben eine `data` Ordner:

    ```bash
    sudo mkdir /data
    ```
1. Verwenden Sie abschließend `mount` zum Anfügen der auf den Bereitstellungspunkt:

    ```bash
    sudo mount /dev/sdc1 /data
    ```
    Sie sollten möglicherweise verwenden Sie `lsblk` auf das bereitgestellte Laufwerk zu sehen:
    
    ```output
    NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
    sda       8:0    0   30G  0 disk
    ├─sda1    8:1    0 29.9G  0 part /
    ├─sda14   8:14   0    4M  0 part
    └─sda15   8:15   0  106M  0 part /boot/efi
    sdb       8:16   0   16G  0 disk
    └─sdb1    8:17   0   16G  0 part /mnt
    sdc       8:32   0 1023G  0 disk
    └─sdc1    8:33   0 1023G  0 part /data
    sr0      11:0    1  628K  0 rom
    ```

### <a name="mounting-the-drive-automatically"></a>Automatisches Bereitstellen des Laufwerks

Um sicherzustellen, dass das Laufwerk nach einem Neustart automatisch bereitgestellt wird, muss es der Datei `/etc/fstab` hinzugefügt werden. Es wird auch dringend empfohlen, der UUID (universally unique Identifier) in verwenden, `/etc/fstab` zum Verweisen auf das Laufwerk und nicht auf den Gerätenamen (z. B. `/dev/sdc1`). Wenn das Betriebssystem während des Starts einen Datenträgerfehler erkennt, wird durch den UUID verhindert, dass an einem bestimmten Ort der falsche Datenträger bereitgestellt wird. Die verbleibenden Datenträger werden dann diesen Geräte-IDs zugewiesen. Verwenden Sie das Hilfsprogramm `blkid`, um den UUID des neuen Laufwerks herauszufinden:

```bash
sudo -i blkid
```

Die Rückgabe ähnelt dem folgenden Beispiel:

```output
/dev/sda1: UUID="36a59c42-c04c-4632-b83f-7015abd10358" TYPE="ext4"
/dev/sdb1: UUID="21092a62-79d4-4d8c-91de-4dd4e8b97d83" TYPE="ext4"
/dev/sdc1: UUID="e311c905-e0d9-43ab-af63-7f4ee4ef108e" TYPE="ext4"
```

1. Kopieren Sie die UUID für die `/dev/sdc1` Laufwerk, und öffnen Sie die `/etc/fstab` -Datei in einem Text-Editor:

    ```bash
    sudo vi /etc/fstab
    ```

> [!WARNING]
> Eine fehlerhafte Bearbeitung der Datei `/etc/fstab` könnte zu einem nicht startfähigen System führen. Wenn Sie sich nicht sicher sind, helfen Ihnen die Informationen zur richtigen Bearbeitung dieser Datei in der Dokumentation weiter. Außerdem wird empfohlen, eine Sicherung der Datei zu erstellen, bevor Sie sie bearbeiten, wenn Sie mit Produktionssystemen arbeiten.

1. Drücken Sie **G**, um zur letzten Zeile in der Datei zu gelangen.

1. Drücken Sie **I**, um in den Einfügemodus zu wechseln. Der Modus sollte am unteren Rand des Bildschirms angegeben werden.

1. Drücken Sie die **ENDE**-TASTE, um an das Ende der Zeile zu gelangen. Alternativ können Sie auch die Pfeiltasten verwenden. Drücken Sie die **EINGABETASTE**, um in eine neue Zeile zu wechseln.

1. Geben Sie die folgende Zeile in den Editor ein. Die Werte können durch Leerzeichen oder Tabstopps getrennt werden. Überprüfen Sie die Dokumentation für Weitere Informationen zu einzelnen Spalten:

    ```output
    UUID=<uuid-goes-here>    /data    ext4    defaults,nofail    1    2
    ```
1. Drücken Sie **ESC**, und geben Sie dann **:w!** ein, um die Datei schreiben und **: Q** um den Editor zu beenden.

1. Wir aktivieren Sie zum Schluss stellen Sie sicher, dass der Eintrag richtig ist, werden aufgefordert, das Betriebssystem auf, die Bereitstellungspunkte aktualisieren:

    ```bash
    sudo mount -a
    ```

    Wenn ein Fehler zurückgegeben wird, bearbeiten Sie die Datei, um das Problem zu ermitteln.

> [!TIP]
> Einige Linux-Kernel unterstützen TRIM zum Verwerfen ungenutzter Blöcke auf dem Datenträger. Dieses Feature ist für Azure-Datenträger verfügbar und kann Ihnen Geld sparen, wenn Sie große Dateien erstellen und diese dann löschen. Erfahren Sie in unserer Dokumentation, wie [dieses Feature aktiviert wird](https://docs.microsoft.com/azure/virtual-machines/linux/attach-disk-portal#trimunmap-support-for-linux-in-azure).

## <a name="install-software-onto-the-vm"></a>Installieren von Software auf dem virtuellen Computer

Wie Sie sehen können, erlaubt SSH Ihnen die Arbeit mit dem virtuellen Linux-Computer wie mit einem lokalen Computer. Sie können diesen virtuellen Computer verwalten, wie alle anderen Linux-Computer: Software installieren, Konfigurieren von Rollen, Anpassen der Features und andere alltäglichen Aufgaben. Konzentrieren wir uns zum Installieren von Software für einen Moment.

Es gibt mehrere Optionen zum Installieren von Software auf dem virtuellen Computer. Zunächst können Sie (wie bereits erwähnt) `scp` zum Kopieren lokaler Dateien von Ihrem Computer auf den virtuellen Computer verwenden. Dadurch können Sie das Kopieren von Daten oder benutzerdefinierten Anwendungen, die Sie ausführen möchten.

Sie können auch Software über Secure Shell installieren. Azure-Computern sind standardmäßig Internet verbunden. Sie können die Standardbefehle verwenden, um beliebte Softwarepakete direkt aus den Standardrepositorys zu installieren. Wir verwenden diesen Ansatz hier zum Installieren von Apache.

### <a name="install-the-apache-web-server"></a>Installieren des Apache-Webservers

Apache ist in Ubuntus Standard-Software-Repositorys, verfügbar, damit sie mit der konventionellen paketverwaltungstools installiert wird:

1. Starten Sie mit dem Aktualisieren des Indexes lokales Paket, um die neuesten upstream Änderungen widerzuspiegeln:

    ```bash
    sudo apt-get update
    ```
    
1. Als Nächstes installieren Sie Apache:

    ```bash
    sudo apt-get install apache2 -y
    ```

1. Der Start sollte automatisch erfolgen. Sie können den Status mit `systemctl` überprüfen:

    ```bash
    sudo systemctl status apache2
    ```

    Die Rückgabe sollte dem folgenden Beispiel ähneln:

    ```output
    apache2.service - The Apache HTTP Server
       Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
      Drop-In: /lib/systemd/system/apache2.service.d
               └─apache2-systemd.conf
       Active: active (running) since Mon 2018-09-03 21:00:03 UTC; 1min 34s ago
     Main PID: 11156 (apache2)
        Tasks: 55 (limit: 4915)
       CGroup: /system.slice/apache2.service
               ├─11156 /usr/sbin/apache2 -k start
               ├─11158 /usr/sbin/apache2 -k start
               └─11159 /usr/sbin/apache2 -k start

    test-web-eus-vm1 systemd[1]: Starting The Apache HTTP Server...
    test-web-eus-vm1 apachectl[11129]: AH00558: apache2: Could not reliably determine the server's fully qua
    test-web-eus-vm1 systemd[1]: Started The Apache HTTP Server.
    ```
    > [!NOTE]
    > Es ist zum Ausführen von Befehlen, wie die folgende, einfache, jedoch ein manueller Prozess – ist Falls wir immer einige Softwarekomponenten installieren müssen, sollten Sie ggf. Automatisierung des Prozesses mithilfe von Skripts.
    
1. Schließlich können wir versuchen, die Standardseite über die öffentliche IP-Adresse abzurufen. Allerdings auch, wenn der Webserver auf dem virtuellen Computer ausgeführt wird, wird nicht Sie eine gültige Verbindung oder eine Antwort erhalten. Wissen Sie Warum?

Ein weiterer Schritt, um für die Interaktion mit dem Webserver können ausführen müssen. Unser virtuelle Netzwerk die eingehende Anforderung blockiert wird – dies ist das Standardverhalten. Wir können dies über die Konfiguration ändern. Sehen wir uns als Nächstes an.