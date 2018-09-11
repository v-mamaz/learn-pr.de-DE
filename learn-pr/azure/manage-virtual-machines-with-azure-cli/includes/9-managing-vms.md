<span data-ttu-id="24f86-101">Eine der Hauptaufgaben, die bei der Ausführung virtueller Computer anfällt, ist deren Starten und Beenden.</span><span class="sxs-lookup"><span data-stu-id="24f86-101">One of the main tasks you'll want to do while running virtual machines is to start and stop them.</span></span>

## <a name="stopping-a-vm"></a><span data-ttu-id="24f86-102">Beenden einer VM</span><span class="sxs-lookup"><span data-stu-id="24f86-102">Stopping a VM</span></span>

<span data-ttu-id="24f86-103">Wir können einen ausgeführten virtuellen Computer mit dem Befehl `vm stop` beenden.</span><span class="sxs-lookup"><span data-stu-id="24f86-103">We can stop a running VM with the `vm stop` command.</span></span> <span data-ttu-id="24f86-104">Sie müssen den Namen und die Ressourcengruppe oder die eindeutige ID der VM übergeben:</span><span class="sxs-lookup"><span data-stu-id="24f86-104">You must pass the name and resource group, or the unique ID for the VM:</span></span>

```azurecli
az vm stop -n SampleVM -g ExerciseResources
```

<span data-ttu-id="24f86-105">Wir können überprüfen, ob die VM beendet wurde, indem wir versuchen, die öffentliche IP-Adresse mit `ssh` oder über den Befehl `vm get-instance-view` zu pingen.</span><span class="sxs-lookup"><span data-stu-id="24f86-105">We can verify it has stopped by attempting to ping the public IP address, using `ssh`, or through the `vm get-instance-view` command.</span></span> <span data-ttu-id="24f86-106">Dieser letzte Ansatz liefert die gleichen grundlegenden Daten wie `vm show`, enthält aber Details zur Instanz selbst.</span><span class="sxs-lookup"><span data-stu-id="24f86-106">This final approach returns the same basic data as `vm show` but includes details about the instance itself.</span></span> <span data-ttu-id="24f86-107">Geben Sie den folgenden Befehl in Azure Cloud Shell ein, um den aktuellen Status Ihrer VM einzusehen:</span><span class="sxs-lookup"><span data-stu-id="24f86-107">Try typing the following command into Azure Cloud Shell to see the current running state of your VM:</span></span>

```azurecli
az vm get-instance-view -n SampleVM -g ExerciseResources --query "instanceView.statuses[?starts_with(code, 'PowerState/')].displayStatus" -o tsv
```

<span data-ttu-id="24f86-108">Dieser Befehl sollte `VM stopped` als Ergebnis zurückgeben.</span><span class="sxs-lookup"><span data-stu-id="24f86-108">This command should return `VM stopped` as the result.</span></span>

## <a name="starting-a-vm"></a><span data-ttu-id="24f86-109">Starten einer VM</span><span class="sxs-lookup"><span data-stu-id="24f86-109">Starting a VM</span></span>

<span data-ttu-id="24f86-110">Den umgekehrten Vorgang können wir mit dem Befehl `vm start` auslösen.</span><span class="sxs-lookup"><span data-stu-id="24f86-110">We can do the reverse through the `vm start` command.</span></span>

```azurecli
az vm start -n SampleVM -g ExerciseResources
```

<span data-ttu-id="24f86-111">Dieser Befehl startet eine beendete VM.</span><span class="sxs-lookup"><span data-stu-id="24f86-111">This command will start a stopped VM.</span></span> <span data-ttu-id="24f86-112">Wir können dies durch die Abfrage `vm get-instance-view` überprüfen, die nun `VM running` zurückgeben sollte.</span><span class="sxs-lookup"><span data-stu-id="24f86-112">We can verify it through the `vm get-instance-view` query, which should now return `VM running`.</span></span>

## <a name="restarting-a-vm"></a><span data-ttu-id="24f86-113">Neustarten einer VM</span><span class="sxs-lookup"><span data-stu-id="24f86-113">Restarting a VM</span></span>

<span data-ttu-id="24f86-114">Schließlich können wir eine VM mit dem Befehl `vm restart` neu starten, nachdem wir Änderungen vorgenommen haben, die einen Neustart erfordern.</span><span class="sxs-lookup"><span data-stu-id="24f86-114">Finally, we can restart a VM if we have made changes that require a reboot using the `vm restart` command.</span></span> <span data-ttu-id="24f86-115">Sie können das Flag `--no-wait` hinzufügen, wenn Sie möchten, dass die Azure CLI sofort wieder verfügbar ist, ohne auf den Neustart der VM zu warten.</span><span class="sxs-lookup"><span data-stu-id="24f86-115">You can add the `--no-wait` flag if you want the Azure CLI to return immediately without waiting for the VM to reboot.</span></span>

