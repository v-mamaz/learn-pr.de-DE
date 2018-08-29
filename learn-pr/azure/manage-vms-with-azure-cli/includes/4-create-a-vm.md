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

| Parameter | Beschreibung |
|-----------|-------------|
| `resource-group` | Die Ressourcengruppe, die Besitzer des virtuellen Computers sein soll. |
| `name` | Der Name des virtuellen Computers – muss innerhalb der Ressourcengruppe eindeutig sein. |
| `image` | Das Betriebssystemimage, das zum Erstellen des virtuellen Computers verwendet werden soll. |

Darüber hinaus ist es hilfreich, das `--verbose`-Flag hinzuzufügen, um den Fortschritt der Erstellung des virtuellen Computers zu beobachten. 

## <a name="create-a-linux-virtual-machine"></a>Erstellen einer virtuellen Linux-Maschine

Erstellen wir jetzt einen neuen virtuellen Linux-Computer. Führen Sie in Azure Cloud Shell folgenden Befehl aus:

```azurecli
az vm create --resource-group ExerciseResources --name SampleVM --image Debian --admin-username aldis --generate-ssh-keys --verbose 
```

Dieser Befehl erstellt einen neuen virtuellen Linux-Computer unter **Debian** mit dem Namen „`SampleVM`“. Beachten Sie, dass das Azure CLI-Tool während der Erstellung des virtuellen Computers gesperrt ist. Wenn Sie nicht warten möchten, können Sie die Option „`--no-wait`“ verwenden, damit das Azure CLI-Tool sofort wieder verfügbar ist, wenn Sie den Befehl beispielsweise in einem Skript ausführen. Verwenden Sie später im Skript den Befehl „`azure vm wait --name [vm-name]`“, um zu warten, bis der virtuelle Computer vollständig erstellt wurde.

Wenn Sie sich die ausführlichen Antworten ansehen, werden Sie auch feststellen, dass der Name „`SampleVM`“ in verschiedenen Abhängigkeiten für den virtuellen Computer verwendet wird.

```
Succeeded: SampleVMNSG (Microsoft.Network/networkSecurityGroups)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMPublicIP (Microsoft.Network/publicIPAddresses)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMVNET (Microsoft.Network/virtualNetworks)
Accepted: vm_deploy_vzKnQDyyq48yPUO4VrSDfFIi81vHKZ9g (Microsoft.Resources/deployments)
```

Sie können diese automatisch generierten Ressourcennamen mithilfe von optionalen Parametern für „`vm create`“ überschreiben, z.B.: `--vnet-name` und `--public-ip-address-dns-name`.

Beachten Sie, dass wir den Namen des Administratorkontos mit dem `admin-username`-Flag zu „aldis“ ändern. Wenn Sie dies auslassen, verwendet der `vm create`-Befehl Ihren _aktuellen Benutzernamen_. Da die Regeln für Kontonamen in jedem Betriebssystem anders sind, ist es sicherer, einen bestimmten Namen anzugeben. Allgemeine Namen wie „root“ und „admin“ sind für die meisten Images nicht zulässig.

Wir verwenden auch das `generate-ssh-keys`-Flag. Dieser Parameter wird für Linux-Distributionen verwendet und erstellt ein Sicherheitsschlüsselpaar, sodass wir das `ssh`-Tool verwenden können, um remote auf den virtuellen Computer zuzugreifen. Die beiden Dateien werden in den Ordner „`.ssh`“ auf Ihrem Computer und auf dem virtuellen Computer platziert. Wenn Sie bereits über einen SSH-Schlüssel namens „`id_rsa`“ im Zielordner verfügen, wird dieser verwendet, anstatt einen neuen Schlüssel zu generieren.

Sobald der virtuelle Computer erstellt wurde, erhalten Sie eine JSON-Antwort, die den aktuellen Zustand des virtuellen Computers und seine von Azure zugewiesenen öffentlichen und privaten IP-Adressen enthält:

```json
{
  "fqdns": "",
  "id": "/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Compute/virtualMachines/SampleVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-1A-D9-74",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "168.61.54.62",
  "resourceGroup": "ExerciseResources",
  "zones": ""
}
```

