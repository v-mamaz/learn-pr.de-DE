Da nun ein virtueller Linux-Computer in Azure vorhanden ist, können Sie diesen für die Aufgaben konfigurieren, die in Azure ausgelagert werden sollen.

Ohne Site-to-Site-VPN mit Azure kann allerdings nicht über Ihr lokales Netzwerk auf Ihre virtuellen Azure-Computer zugegriffen werden. Wenn Sie sich gerade erst mit Azure vertraut machen, haben Sie wahrscheinlich noch kein Site-to-Site-VPN eingerichtet. Im Folgenden erfahren Sie daher, wie Sie eine Verbindung mit dem virtuellen Computer herstellen.

## <a name="azure-virtual-machines-ip-addresses"></a>IP-Adressen von virtuellen Azure-Computern

Wie Sie bereits gesehen haben, kommunizieren virtuelle Azure-Computer über ein virtuelles Netzwerk. Ihnen kann auch eine optionale öffentliche IP-Adresse zugewiesen werden. Eine öffentliche IP-Adresse ermöglicht die Interaktion mit dem virtuellen Computer über das Internet. Alternativ können Sie ein virtuelles privates Netzwerk (VPN) einrichten, das Ihr lokales Netzwerk mit Azure verbindet. So können Sie eine sichere Verbindung mit dem virtuellen Computer herstellen, ohne eine öffentliche IP-Adresse verfügbar zu machen. Dieser Ansatz wird in einem anderen Modul behandelt und ist vollständig dokumentiert, sollten Sie sich für diese Option interessieren.

Noch ein Hinweis: Öffentliche IP-Adressen werden in Azure häufig dynamisch zugewiesen. Das bedeutet, dass sich die IP-Adresse im Laufe der Zeit ändern kann. Bei virtuellen Computern geschieht das, wenn der virtuelle Computer neu gestartet wird. Sie können gegen Aufpreis statische Adressen zuweisen, wenn Sie eine direkte Verbindung mit einer IP-Adresse anstatt mit einem Namen herstellen möchten und sicherstellen müssen, dass sich die IP-Adresse nicht ändert.

## <a name="connect-to-an-azure-linux-virtual-machines-with-ssh"></a>Herstellen einer SSH-Verbindung mit einem virtuellen Azure Linux-Computer

Mit einem virtuellen Computer in Azure kann ganz einfach eine SSH-Verbindung hergestellt werden. Öffnen Sie im Azure-Portal die Eigenschaften Ihres virtuellen Computers, und klicken Sie im oberen Bereich auf **Verbinden**. Dadurch werden die IP-Adressen, die dem virtuellen Computers zugewiesen sind, und die Anmeldeinformationen für SSH angezeigt. 

![SSH-Verbindungsinformationen für virtuellen Linux-Computer](../media-drafts/5-connect-ssh.png)

Mit diesen Details und dem folgenden Befehl können Sie eine Verbindung mit dem virtuellen Linux-Computer herstellen:

```bash
ssh jim@137.117.101.249
```

Bei der ersten Verbindungsherstellung macht uns das SSH-Tool auf die Authentifizierung bei einem unbekannten Host aufmerksam. SSH weist darauf hin, dass Sie noch nie eine Verbindung mit diesem Server hergestellt haben. Ist dies der Fall, ist alles in Ordnung, und Sie können mit „Ja“ antworten, um den Fingerabdruck des Servers in der Datei mit den bekannten Hosts zu speichern.

```output
The authenticity of host '137.117.101.249 (137.117.101.249)' can't be established.
ECDSA key fingerprint is SHA256:w1h08h4ie1iMq7ibIVSQM/PhcXFV7O7EEhjEqhPYMWY.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '137.117.101.249' (ECDSA) to the list of known hosts.
```

## <a name="transferring-files-to-the-vm"></a>Übertragen von Dateien an den virtuellen Computer

Eine weitere allgemeine Aufgabe besteht darin, lokale Dateien oder Daten zwischen Servern zu kopieren. In unserem Fall möchten wir letztendlich unsere Websitedaten auf unseren virtuellen Azure-Computer kopieren. Bei Verwendung von virtuellen Linux-Computern und SSH können wir den Befehl `scp` verwenden. Dieser Befehl ähnelt dem Befehl `cp` zum Kopieren lokaler Dateien. Sie müssen nun allerdings den Remotebenutzer und -host angeben. 

Wenn Sie beispielsweise `somefile.txt` aus dem aktuellen Verzeichnis in `~/folder` auf dem Linux-Computer mit der IP-Adresse `192.168.1.25` kopieren möchten, können Sie Folgendes eingeben:

```bash
scp somefile.txt someuser@192.168.1.25:~/folder/
```

Dadurch wird `someuser` auf dem Remotesystem authentifiziert, und Sie werden dazu aufgefordert, Ihr Kennwort oder Ihren privaten SSH-Schlüssel einzugeben. Dieser Benutzer muss auf dem Zielserver über Schreibberechtigungen für `~/folder/` verfügen.

> [!WARNING]
> Sollte die Befehlszeile nicht ganz korrekt sein, kopiert `scp` die Dateien lokal. Meist fehlt der Zielordner.

Als Nächstes stellen wir eine SSH-Verbindung mit unserem ausgeführten virtuellen Linux-Computer her.