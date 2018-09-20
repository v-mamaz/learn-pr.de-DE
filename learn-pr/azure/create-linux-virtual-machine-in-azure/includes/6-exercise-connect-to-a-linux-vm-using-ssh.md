Der virtuelle Linux-Computer wurde bereitgestellt und wird ausgeführt, aber noch nicht für die Arbeit konfiguriert. Stellen wir eine Verbindung mit SSH her, und konfigurieren wir Apache, damit wir über einen Webserver verfügen, der ausgeführt wird.

## <a name="connect-to-the-vm-with-ssh"></a>Herstellen einer Verbindung mit dem virtuellen Computer mit SSH

Zum Herstellen der Verbindung eines virtuellen Azure-Computers mit einem SSH-Client benötigen Sie Folgendes:

- SSH-Clientsoftware (in den meisten modernen Betriebssystemen vorhanden)
- Die öffentliche IP-Adresse des virtuellen Computers (oder die private, wenn der virtuelle Computer dafür konfiguriert ist, eine Verbindung mit Ihrem Netzwerk herzustellen)

### <a name="get-the-public-ip-address"></a>Abrufen der öffentlichen IP-Adresse

1. Stellen Sie im [Azure-Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) sicher, dass der Bereich **Übersicht** für den zuvor erstellten virtuellen Computer geöffnet ist. Sie finden den virtuellen Computer unter **Alle Ressourcen**, falls Sie diesen öffnen müssen. Im Bereich „Übersicht“ finden Sie zahlreiche Informationen zum virtuellen Computer.

    - Sie können sehen, ob er ausgeführt wird
    - Sie können ihn beenden oder neu starten
    - Sie können die öffentliche IP-Adresse abrufen, um eine Verbindung mit dem virtuellen Computer herzustellen
    - Sie können die Aktivität von CPU, Festplatte und Netzwerk anzeigen

1. Klicken Sie oben im Bereich auf die Schaltfläche **Verbinden**.

1. Notieren Sie sich die Einstellungen für die **IP-Adresse** und die **Portnummer** auf dem Blatt **Verbindung mit virtuellem Computer herstellen**. Auf der Registerkarte **SSH** finden Sie auch den Befehl, den Sie lokal ausführen müssen, um eine Verbindung mit dem virtuellen Computer herzustellen. Kopieren Sie diesen in die Zwischenablage.

## <a name="connect-with-ssh"></a>Verbinden mit SSH

1. Fügen Sie die Befehlszeile, die Sie von der Registerkarte „SSH“ abgerufen haben, in Azure Cloud Shell ein. Das Ergebnis sollte in etwa wie folgt aussehen. Es wird jedoch eine andere IP-Adresse verwendet (und möglicherweise ein anderer Benutzername, wenn Sie nicht **jim** angegeben haben)

    ```bash
    ssh jim@137.117.101.249
    ```

1. Mit diesem Befehl wird eine Secure Shell-Verbindung geöffnet, und es wird eine herkömmliche Shell-Eingabeaufforderung für Linux angezeigt.

1. Führen Sie einige Linux-Befehle aus:
    - `ls -la /`, um den Stamm des Datenträgers anzuzeigen
    - `ps -l`, um alle ausgeführten Prozesse anzuzeigen
    - `dmesg`, um alle Kernelnachrichten aufzulisten
    - `lsblk`, um alle Blockgeräte aufzulisten. Hier werden Ihre Laufwerke angezeigt

Interessanter ist das, was in der Liste der Laufwerke _fehlt_. Beachten Sie, dass unser **Daten**laufwerk (`sdc`) zwar vorhanden, nicht aber im Dateisystem bereitgestellt ist. Azure hat eine VHD hinzugefügt, aber nicht initialisiert.

## <a name="initialize-data-disks"></a>Initialisieren von Laufwerken

Alle zusätzlichen Laufwerke, die Sie neu erstellen, müssen initialisiert und formatiert werden. Der Prozess ist der gleiche wie bei einem physischen Datenträger:

1. Identifizieren Sie zuerst den Datenträger. Dies ist weiter oben erfolgt. Sie können auch `dmesg | grep SCSI` verwenden, um alle Nachrichten aus dem Kernel für SCSI-Geräte aufzulisten.

1. Sobald Sie das Laufwerk (`sdc`) kennen, das initialisiert werden muss, können Sie `fdisk` zu diesem Zweck verwenden. Sie müssen den Befehl mit `sudo` ausführen und den Datenträger angeben, der partitioniert werden soll. Wir können den folgenden Befehl verwenden, um eine neue primäre Partition zu erstellen:

    ```bash
    (echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
    ```

1. Im nächsten Schritt schreiben Sie jetzt mit dem Befehl `mkfs` ein Dateisystem auf die Partition.

    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```

1. Abschließend müssen wir das Laufwerk im Dateisystem bereitstellen. Angenommen, es ist ein Ordner `data` vorhanden. Wir erstellen den Bereitstellungspunktordner und stellen das Laufwerk bereit.

    ```bash
    sudo mkdir /data & sudo mount /dev/sdc1 /data
    ```

    > [!TIP]
    > Wir haben den Datenträger initialisiert und bereitgestellt. Falls Sie an weiteren Informationen zu diesem Prozess interessiert sind, können Sie das Modul **Hinzufügen und Ändern der Größe von Datenträgern in Azure Virtual Machines** verwenden. Darin wird diese Aufgabe ausführlicher behandelt.

## <a name="install-software-onto-the-vm"></a>Installieren von Software auf dem virtuellen Computer

Wie Sie sehen können, erlaubt SSH Ihnen die Arbeit mit dem virtuellen Linux-Computer wie mit einem lokalen Computer. Sie können diesen virtuellen Computer wie jeden anderen Linux-Computer verwalten: Sie können Software installieren, Rollen konfigurieren, Features anpassen und andere alltägliche Aufgaben ausführen. Wir beschäftigen uns hier erst einmal mit dem Installieren der Software.

Es gibt mehrere Optionen zum Installieren von Software auf dem virtuellen Computer. Zunächst können Sie (wie bereits erwähnt) `scp` zum Kopieren lokaler Dateien von Ihrem Computer auf den virtuellen Computer verwenden. Damit können Sie Daten oder benutzerdefinierte Anwendungen kopieren, die Sie ausführen möchten.

Sie können Software auch über Secure Shell installieren. Azure-Computer sind standardmäßig mit dem Internet verbunden. Sie können die Standardbefehle verwenden, um beliebte Softwarepakete direkt aus Standardrepositorys zu installieren. Wir verwenden diesen Ansatz hier zum Installieren von Apache.

### <a name="install-the-apache-web-server"></a>Installieren des Apache-Webservers

Apache ist in den Standardsoftwarerepositorys von Ubuntu verfügbar. Daher erfolgt die Installation mit herkömmlichen Paketverwaltungstools:

1. Starten Sie, indem Sie den lokalen Paketindex aktualisieren, um die neuesten Upstreamänderungen widerzuspiegeln:

    ```bash
    sudo apt-get update
    ```
    
1. Installieren Sie im nächsten Schritt Apache:

    ```bash
    sudo apt-get install apache2 -y
    ```

1. Der Start sollte automatisch erfolgen. Sie können den Status mit `systemctl` überprüfen:

    ```bash
    sudo systemctl status apache2 --no-pager
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
    > Die Ausführung dieser Art von Befehlen ist einfach, aber es handelt sich um einen manuellen Prozess. Wenn Sie häufig Software installieren müssen, sollten Sie die Automatisierung des Prozesses mithilfe von Skripts in Betracht ziehen.
    
1. Schließlich können wir versuchen, die Standardseite über die öffentliche IP-Adresse abzurufen. Aber obwohl der Webserver auf der VM ausgeführt wird, erhalten Sie keine gültige Verbindung oder Antwort. Kennen Sie den Grund?

Wir müssen einen weiteren Schritt ausführen, um mit dem Webserver interagieren zu können. Unser virtuelles Netzwerk blockiert die eingehende Anforderung. Dies ist das Standardverhalten. Wir können dies über die Konfiguration ändern. Dies sehen wir uns als Nächstes an.