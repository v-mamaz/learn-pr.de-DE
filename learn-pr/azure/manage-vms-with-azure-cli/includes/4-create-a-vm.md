Die Azure CLI enthält die `vm` Befehl aus, um die Arbeit mit virtuellen Computern in Azure. Wir können mehrere Unterbefehle spezifischer Aufgaben angeben, die am häufigsten verwendeten gehören:

| Unterbefehl | Beschreibung |
|-------------|-------------|
| `create`    | Erstellen eines neuen virtuellen Computers |
| `deallocate` | Aufheben der Zuordnung eines virtuellen Computers |
| `delete` | Löschen eines virtuellen Computers |
| `list` | Auflisten der erstellten virtuellen Computer in Ihrem Abonnement |
| `open-port` | Öffnen Sie einen bestimmten Netzwerkport für eingehenden Datenverkehr |
| `restart` | Neustarten eines virtuellen Computers |
| `show` | Rufen Sie die Details für einen virtuellen Computer |
| `start` | Starten eines beendeten virtuellen Computers |
| `stop` | Beenden einer ausgeführten virtuellen Maschine |
| `update` | Aktualisieren Sie eine Eigenschaft eines virtuellen Computers |

> [!NOTE]
> Eine vollständige Liste der Befehle, sehen Sie sich die [Referenzdokumentation für Azure-Befehlszeilenschnittstelle](https://docs.microsoft.com/en-us/cli/azure/reference-index?view=azure-cli-latest)

Beginnen wir mit der ersten Anweisung: `az vm create`. Mit diesem Befehl wird verwendet, um einen virtuellen Computer in einer Ressourcengruppe zu erstellen. Es gibt mehrere Parameter, die Sie übergeben können, um alle Aspekte von den neuen virtuellen Computer zu konfigurieren. Die drei Parameter, die angegeben werden müssen, sind:

| Parameter | Beschreibung |
|-----------|-------------|
| `resource-group` | Die Ressourcengruppe aus, die die virtuelle Maschine besitzt |
| `name` | Der Name des virtuellen Computers – muss innerhalb der Ressourcengruppe eindeutig sein |
| `image` | Das Betriebssystemabbild zu verwenden, um den virtuellen Computer erstellen |

Darüber hinaus ist es hilfreich sein, fügen die `--verbose` Flag Fortschritt verfolgen, während die VM erstellt wird. 

## <a name="create-a-linux-virtual-machine"></a>Erstellen einer virtuellen Linux-Maschine

Wir erstellen einen neuen virtuellen Linux-Computer. Führen Sie den folgenden Befehl in Cloud Shell ein:

```azurecli
az vm create --resource-group ExerciseResources --name SampleVM --image Debian --admin-username aldis --generate-ssh-keys --verbose 
```

Dieser Befehl erstellt ein neues **Debian** virtuellen Linux-Computer mit dem Namen `SampleVM`. Beachten Sie, dass das CLI-Tool blockiert wird, während die VM erstellt wird. Wenn Sie nicht warten möchten, können Sie mithilfe der `--no-wait` Option aus, um das Teilen der CLI-Tool sofort zurückkehren, z. B. Wenn Sie den Befehl in einem Skript ausführen. Verwenden Sie später im Skript, das `azure vm wait --name [vm-name]` Befehl aus, um zu warten, bis der virtuelle Computer beendet, erstellt wird.

Wenn Sie die ausführlichen Antworten betrachten, Sie werden auch angezeigt, die `SampleVM` Name wird verwendet, um verschiedene Abhängigkeiten für den virtuellen Computer zu benennen.

```
Succeeded: SampleVMNSG (Microsoft.Network/networkSecurityGroups)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMPublicIP (Microsoft.Network/publicIPAddresses)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMVNET (Microsoft.Network/virtualNetworks)
Accepted: vm_deploy_vzKnQDyyq48yPUO4VrSDfFIi81vHKZ9g (Microsoft.Resources/deployments)
```

Sie können diese automatisch generierten Ressourcennamen mithilfe optionaler Parameter zum Überschreiben `vm create` wie z. B. `--vnet-name` und `--public-ip-address-dns-name`.

Beachten Sie, dass wir den Namen des Admin-Konto durch Angeben der `admin-username` Flag "Aldis" sein. Wenn Sie nicht angeben, die `vm create` -Befehl Ihrem _aktuellen Benutzernamen_. Da die Regeln für den Kontonamen für jedes Betriebssystem unterschiedlich sind, ist es sicherer, die einen bestimmten Namen zu geben. Allgemeine Namen, z. B. "Root" und "Admin" sind für die meisten Images nicht zulässig.

Wir verwenden zudem die `generate-ssh-keys` Flag. Dieser Parameter wird für Linux-Distributionen verwendet und ein Paar von Sicherheitsschlüsseln erstellt, sodass wir nutzen können die `ssh` Tool, um den Remotezugriff auf den virtuellen Computer. Die beiden Dateien befinden sich in der `.ssh` Ordner auf Ihrem Computer und auf dem virtuellen Computer. Wenn Sie bereits über einen SSH-Schlüssel mit dem Namen verfügen `id_rsa` im Zielordner, dann wird dieser verwendet statt einen neuen Schlüssel generiert.

Nach der Erstellung des virtuellen Computers abgeschlossen wurde, erhalten Sie eine JSON-Antwort, die den aktuellen Status des virtuellen Computers enthält, und es die öffentlichen und privaten IP-Adressen, die von Azure zugewiesen ist:

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

