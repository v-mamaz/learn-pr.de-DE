Bevor wir einen virtuellen Linux-Computer in Azure erstellen können, müssen wir uns Gedanken über den Remotezugriff machen. Wir möchten in der Lage, melden Sie sich an unseren Linux-Webserver, konfigurieren Sie die Software und Wartungsaufgaben ausführen. Der Standardansatz zum Verwalten von virtuellen Linux-Computern, die in Azure gehostet werden, ist SSH.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="what-is-ssh"></a>Was ist SSH?

Secure Shell (SSH) ist ein Protokoll für verschlüsselte Verbindungen, das die sichere Anmeldung über ungesicherte Verbindungen ermöglicht. SSH ermöglicht es Ihnen, über eine Netzwerkverbindung von einem Remotestandort aus eine Verbindung mit einer Terminalshell herzustellen.

Es gibt zwei Ansätze, die wir, mit denen Sie eine SSH-Verbindung zu authentifizieren: **Benutzername und Kennwort**, oder ein **SSH-Schlüsselpaar**.

> [!TIP]
> Obwohl SSH eine verschlüsselte Verbindung enthält, bewirkt, dass mit Kennwörtern für SSH-Verbindungen den virtuellen Computer anfällig für Brute-Force-Angriffe von Kennwörtern. Eine sicherere und bevorzugte Methode zum Herstellen einer Verbindung mit einer Linux-VM mit SSH ist ein öffentliches / privates kryptografisches Schlüsselpaar auch bekannt als SSH-Schlüssel.

Mit einem SSH-Schlüsselpaar können Sie sich bei Linux-basierten virtuellen Azure-Computern ohne ein Kennwort anmelden. Dies ist ein sichererer Ansatz gewählt, wenn Sie nur über eine kleine Anzahl von Computern mit dem virtuellen Computer anmelden möchten. Wenn Sie von verschiedenen Standorten aus auf den virtuellen Linux-Computer zugreifen müssen, ist eine Kombination aus Benutzername und Kennwort vielleicht die bessere Lösung. Es gibt zwei Teile einer SSH-Schlüsselpaar: einen öffentlichen Schlüssel und einen privaten Schlüssel.

* Der öffentliche Schlüssel wird auf Ihrem virtuellen Linux-Computer oder in einem anderen Dienst gespeichert, den Sie für die Verschlüsselung mit einem öffentlichen Schlüssel verwenden möchten. Dieser Schlüssel kann für beliebige Personen freigegeben werden.

* Die **privaten Schlüssel** wird präsentiert zum Überprüfen Ihrer Identität auf Ihrer Linux-VM, wenn Sie eine SSH-Verbindung herzustellen. Betrachten Sie diesen als vertrauliche Information, und schützen Sie ihn wie ein Kennwort oder andere private Daten.

Sie können das gleiche Paar aus einem öffentlichen und privaten Schlüssel verwenden, um auf mehrere virtuelle Azure-Computer und Dienste zuzugreifen.

## <a name="create-the-ssh-key-pair"></a>Erstellen des SSH-Schlüsselpaars

Unter Linux, Windows 10 und macOS können Sie den integrierten Befehl `ssh-keygen` verwenden, um die Dateien mit den öffentlichen und privaten SSH-Schlüsseln zu generieren.

> [!TIP]
> Windows 10 bietet mit dem **Fall Creators Update** einen SSH-Client. Frühere Versionen von Windows erfordern zusätzlichen Software zum Verwenden von SSH an. [finden Sie in der Dokumentation ausführliche](https://docs.microsoft.com/azure/virtual-machines/linux/ssh-from-windows). Alternativ können Sie SSH auch dann nutzen, wenn Sie das Linux-Subsystem für Windows installieren.

> [!NOTE]
> Wir verwenden Azure Cloud Shell, der die generierten Schlüssel in Azure in Ihr privates Speicherkonto gespeichert wird. Sie können diese Befehle auch direkt in Ihre lokale Shell eingeben, wenn Sie möchten. Sie müssen die Anweisungen in diesem Modul so anpassen, dass sie einer lokalen Sitzung entsprechen, wenn Sie diesen Ansatz verfolgen.

[!include[](../../../includes/azure-sandbox-activate.md)]

Bei dem folgenden Befehl handelt es sich um die kürzeste Anweisung, um das Schlüsselpaar für einen virtuellen Azure-Computer zu generieren. Dadurch wird ein SSH-Protokoll 2 (SSH-2) RSA öffentlichen / privaten Schlüsselpaar mit einem 2048-Bit-Länge (die minimale Länge) erstellt.

Geben Sie diesen Befehl in Cloud Shell ein:

```bash
ssh-keygen -t rsa -b 2048
```

Das Tool werden für die Namen und eine optionale Passphrase aufgefordert. Verwenden Sie einfach die Standardeinstellungen. Es werden zwei Dateien erstellt: `id_rsa` und `id_rsa.pub` im Verzeichnis `~/.ssh`. Die Dateien werden ggf. überschrieben. Es gibt verschiedene Optionen, die Sie verwenden können, geben Sie den Dateinamen oder eine Passphrase für die Aufforderung zu vermeiden.

### <a name="private-key-passphrase"></a>Passphrase für den privaten Schlüssel

Sie können optional eine Passphrase angeben, während Sie Ihren privaten Schlüssel generieren. Dies ist ein Kennwort, das Sie eingeben müssen, wenn Sie den Schlüssel verwenden. Diese Passphrase wird für den Zugriff auf die private SSH-Schlüsseldatei verwendet und ist nicht das Kennwort für das Benutzerkonto.

Wenn Sie Ihren SSH-Schlüssel eine Passphrase hinzuzufügen, verschlüsselt den privaten Schlüssel mit AES 128 Bit, sodass der private Schlüssel ohne die Passphrase für die Entschlüsselung nutzlos ist.

> [!IMPORTANT]
> Es wird **dringend** empfohlen, eine Passphrase hinzuzufügen. Falls ein Angreifer Ihren privaten Schlüssel entwendet und dafür keine Passphrase konfiguriert wurde, kann sich der Angreifer mithilfe des privaten Schlüssels bei jedem Server anmelden, der über den entsprechenden öffentlichen Schlüssel verfügt. Wenn Sie eine Passphrase einen privaten Schlüssel schützt, kann es durch Angreifer verwendet werden. Dies stellt eine zusätzliche Sicherheitsebene für Ihre Infrastruktur unter Azure bereit.

Das folgende Beispiel zeigt, wie die Passphrase festgelegt wird. Sie müssen diesen Befehl ausführen (obwohl dies möglich, wenn Sie möchten):

```bash
ssh-keygen -t rsa -b 4096 \
    -C "azureuser@myserver" \
    -f ~/.ssh/mykeys/myprivatekey \
    -N someReallySecurePhraseYouWillRemember
```

| Parameter | Funktionsbeschreibung |
|-----------|--------------|
| `-t` | Der Typ des zu erstellenden Schlüssels. Muss **rsa** sein. |
| `-b` | Die Anzahl der Bits im Schlüssel. Die Mindestlänge beträgt 2.048 Bits, die Höchstlänge 4.096 Bits. |
| `-C` | Ein optionaler Kommentar, der an den öffentlichen Schlüssel angefügt wird und verwendet werden kann, um ihn zu identifizieren. Dies ist eine e-Mail-Adresse, normalerweise einfacher Text ist. Daher können Sie die ID-Methode verwenden, Sie bevorzugen. |
| `-f` | Der Speicherort und den Dateinamen der Name der Datei des privaten Schlüssels. Eine entsprechende Datei für den öffentlichen Schlüssel mit der Erweiterung **.pub** wird im gleichen Verzeichnis generiert. Das Verzeichnis muss vorhanden sein. |
| `-N` | Die Passphrase, die zum Verschlüsseln des privaten Schlüssels verwendet wird. |

## <a name="use-the-ssh-key-pair-with-an-azure-linux-vm"></a>Verwenden des SSH-Schlüsselpaars mit einem virtuellen Linux-Computer in Azure

Nachdem Sie das Schlüsselpaar generiert haben, können Sie es mit einem virtuellen Linux-Computer in Azure verwenden. Den öffentlichen Schlüssel während der Erstellung des virtuellen Computers geben kann oder fügen Sie es hinzu, nachdem der virtuelle Computer erstellt wurde.

Sie können den Inhalt der Datei in Azure Cloud Shell mit dem folgenden Befehl anzeigen:

```bash
cat ~/.ssh/id_rsa.pub
```

Es handelt sich um eine einzelne Zeile, die ungefähr wie das folgende Beispiel aussieht:

```output
ssh-rsa XXXXXXXXXXc2EAAAADAXABAAABAXC5Am7+fGZ+5zXBGgXS6GUvmsXCLGc7tX7/rViXk3+eShZzaXnt75gUmT1I2f75zFn2hlAIDGKWf4g12KWcZxy81TniUOTjUsVlwPymXUXxESL/UfJKfbdstBhTOdy5EG9rYWA0K43SJmwPhH28BpoLfXXXXXGX/ilsXXXXXKgRLiJ2W19MzXHp8z3Lxw7r9wx3HaVlP4XiFv9U4hGcp8RMI1MP1nNesFlOBpG4pV2bJRBTXNXeY4l6F8WZ3C4kuf8XxOo08mXaTpvZ3T1841altmNTZCcPkXuMrBjYSJbA8npoXAXNwiivyoe3X2KMXXXXXdXXXXXXXXXXCXXXXX/ azureuser@myserver
```

Kopieren Sie diesen Wert an, damit Sie sie in der nächsten Übung verwenden können.

### <a name="use-the-ssh-key-when-creating-a-linux-vm"></a>Verwenden des SSH-Schlüssels beim Erstellen eines virtuellen Linux-Computers

Um den SSH-Schlüssel beim Erstellen eines neuen virtuellen Linux-Computers anzuwenden, müssen Sie den Inhalt des öffentlichen Schlüssels kopieren und im Azure-Portal zur Verfügung stellen, _oder_ stellen Sie die Datei mit dem öffentlichen Schlüssel in der Azure CLI oder mit einem Azure PowerShell-Befehl bereit. Wir verwenden diesen Ansatz, wenn wir den virtuellen Linux-Computer erstellen.

### <a name="add-the-ssh-key-to-an-existing-linux-vm"></a>Hinzufügen des SSH-Schlüssels zu einem vorhandenen virtuellen Linux-Computer

Wenn Sie bereits einen virtuellen Computer erstellt haben, können Sie den öffentlichen Schlüssel auf dem virtuellen Linux-Computer mit dem Befehl `ssh-copy-id` installieren. Nachdem der Schlüssel für SSH autorisiert wurde, gewährt er ohne Angabe eines Kennworts Zugriff auf den Server.

Übergeben Sie sie aus, eine Datei mit dem öffentlichen Schlüssel und den Benutzernamen, den Schlüssel zugeordnet werden soll:

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub azureuser@myserver
```

Nun, da wir unsere öffentlichen Schlüssel haben, lassen Sie uns beim Azure-Portal wechseln, und Erstellen einer Linux-VM.
