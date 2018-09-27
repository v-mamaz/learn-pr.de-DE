Wir beginnen mit der offensichtlichsten Aufgabe: der Erstellung eines virtuellen Azure-Computers.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="logins-subscriptions-and-resource-groups"></a>Anmeldungen, Abonnements und Ressourcengruppen

Sie arbeiten in Azure Cloud Shell auf der rechten Seite. Nachdem Sie die Sandbox aktiviert haben, werden Sie mit einem kostenlosen Abonnement, das von Microsoft Learn verwaltet wird, bei Azure angemeldet. Sie müssen sich nicht selbst bei Azure anmelden oder ein Abonnement auswählen. Dies wird für Sie durchgeführt. Außerdem erstellen Sie hier normalerweise eine _Ressourcengruppe_ für neue Ressourcen. In diesem Modul erstellt die Azure-Sandbox für Sie eine Ressourcengruppe, die verwendet wird, um alle Befehle auszuführen.

## <a name="create-a-linux-vm-with-the-azure-cli"></a>Erstellen eines virtuellen Linux-Computers mit der Azure CLI

Die Azure CLI enthält den Befehl „`vm`“ für die Arbeit mit virtuellen Computern in Azure. Wir können verschiedene Unterbefehle bereitstellen, um bestimmte Aufgaben auszuführen. Dies sind die am häufigsten verwendeten:

| Unterbefehl | Beschreibung |
|-------------|-------------|
| `create`    | Erstellen eines neuen virtuellen Computers |
| `deallocate` | Aufheben der Zuordnung eines virtuellen Computers |
| `delete` | Löschen eines virtuellen Computers |
| `list` | Auflisten der erstellten virtuellen Computer in Ihrem Abonnement |
| `open-port` | Öffnen eines bestimmten Netzwerkports für eingehenden Datenverkehr |
| `restart` | Neustarten eines virtuellen Computers |
| `show` | Abrufen der Details für einen virtuellen Computer |
| `start` | Starten eines angehaltenen virtuellen Computers |
| `stop` | Anhalten eines ausgeführten virtuellen Computers |
| `update` | Aktualisieren der Eigenschaft eines virtuellen Computers |

> [!NOTE]
> Eine vollständige Liste der Befehle finden Sie in der [Dokumentation der Azure CLI-Referenz](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest).

Beginnen wir mit dem ersten: `az vm create`. Mit diesem Befehl wird ein virtueller Computer in einer Ressourcengruppe erstellt. Es gibt verschiedene Parameter, die Sie übergeben können, um alle Aspekte des neuen virtuellen Computers zu konfigurieren. Diese drei Parameter müssen angegeben werden:

> [!div class="mx-tableFixed"]
> | Parameter | Beschreibung |
> |-----------|-------------|
> | `resource-group` | Die Ressourcengruppe, die als Besitzer des virtuellen Computers fungiert. Verwenden Sie **<rgn>[Sandboxressourcengruppe]</rgn>**. |
> | `name` | Der Name des virtuellen Computers; muss innerhalb der Ressourcengruppe eindeutig sein. |
> | `image` | Das Betriebssystemimage, das zum Erstellen des virtuellen Computers verwendet werden soll. |
> | `location` | Die Region, in der die VM angeordnet wird. Normalerweise liegt die Region in der Nähe des VM-Benutzers. Wählen Sie in dieser Übung in der folgenden Liste einen Standort in Ihrer Nähe aus. |

<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

Darüber hinaus ist es hilfreich, das `--verbose`-Flag hinzuzufügen, um den Fortschritt der Erstellung des virtuellen Computers zu beobachten. 

## <a name="create-a-linux-virtual-machine"></a>Erstellen eines virtuellen Linux-Computers

Wir erstellen nun einen neuen virtuellen Linux-Computer. Führen Sie den folgenden Befehl in Azure Cloud Shell aus, um am Standort „USA, Westen“ einen Debian Linux-Computer zu erstellen. Ändern Sie den Standort, wenn dieser nicht in Ihrer Nähe liegt.

```azurecli
az vm create --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM --image Debian --admin-username aldis --generate-ssh-keys --location westus --verbose 
```

[!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]


Dieser Befehl erstellt einen neuen virtuellen Linux-Computer unter **Debian** mit dem Namen „`SampleVM`“. Beachten Sie, dass sich das Azure CLI-Tool während der Erstellung des virtuellen Computers im Wartezustand befindet. Sie können die Option `--no-wait` hinzufügen, um das Azure CLI-Tool anzuweisen, die Rückgabe sofort durchzuführen, und zu erreichen, dass Azure mit der Erstellung der VM im Hintergrund fortfährt. Dies ist hilfreich, wenn Sie den Befehl in einem Skript ausführen. Verwenden Sie später im Skript den Befehl „`azure vm wait --name [vm-name]`“, um zu warten, bis der virtuelle Computer vollständig erstellt wurde.

Wenn Sie sich die ausführlichen Antworten ansehen, werden Sie auch feststellen, dass der Name „`SampleVM`“ in verschiedenen Abhängigkeiten für den virtuellen Computer verwendet wird.

```output
Succeeded: SampleVMNSG (Microsoft.Network/networkSecurityGroups)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMPublicIP (Microsoft.Network/publicIPAddresses)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMVNET (Microsoft.Network/virtualNetworks)
Accepted: vm_deploy_vzKnQDyyq48yPUO4VrSDfFIi81vHKZ9g (Microsoft.Resources/deployments)
```

Sie können diese automatisch generierten Ressourcennamen mithilfe von optionalen Parametern für „`vm create`“ überschreiben, z.B. `--vnet-name` und `--public-ip-address-dns-name`.

Wir ändern den Namen des Administratorkontos mit dem `admin-username`-Flag in **„aldis“**. Wenn Sie dies auslassen, verwendet der `vm create`-Befehl Ihren _aktuellen Benutzernamen_. Da die Regeln für Kontonamen in jedem Betriebssystem anders sind, ist es sicherer, einen bestimmten Namen anzugeben. 

> [!NOTE]
> Allgemeine Namen wie „root“ und „admin“ sind für die meisten Images nicht zulässig.

Wir verwenden auch das `generate-ssh-keys`-Flag. Dieser Parameter wird für Linux-Distributionen verwendet und erstellt ein Sicherheitsschlüsselpaar, sodass wir das `ssh`-Tool verwenden können, um remote auf den virtuellen Computer zuzugreifen. Die beiden Dateien werden in den Ordner „`.ssh`“ auf Ihrem Computer und auf dem virtuellen Computer platziert. Wenn Sie bereits über einen SSH-Schlüssel namens „`id_rsa`“ im Zielordner verfügen, wird dieser verwendet, anstatt einen neuen Schlüssel zu generieren.

Sobald der virtuelle Computer erstellt wurde, erhalten Sie eine JSON-Antwort, die den aktuellen Zustand des virtuellen Computers und seine von Azure zugewiesenen öffentlichen und privaten IP-Adressen enthält:

```json
{
  "fqdns": "",
  "id": "/subscriptions/20f4b944-fc7a-4d38-b02c-900c8223c3a0/resourceGroups/2568d0d0-efe3-4d04-a08f-df7f009f822a/providers/Microsoft.Compute/virtualMachines/SampleVM",
  "location": "westus",
  "macAddress": "00-0D-3A-58-F8-45",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.83.165.85",
  "resourceGroup": "2568d0d0-efe3-4d04-a08f-df7f009f822a",
  "zones": ""
}
```
