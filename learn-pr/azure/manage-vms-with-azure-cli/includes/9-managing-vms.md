<span data-ttu-id="7de6b-101">Eine der Hauptaufgaben, die Sie sollten den ausgeführten virtuellen Computern ist zum Starten und beenden sie.</span><span class="sxs-lookup"><span data-stu-id="7de6b-101">One of the main tasks you'll want to do to running virtual machines is to start and stop them.</span></span>

## <a name="stopping-a-vm"></a><span data-ttu-id="7de6b-102">Beenden eines virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="7de6b-102">Stopping a VM</span></span>

<span data-ttu-id="7de6b-103">Wir können einen ausgeführten virtuellen Computer mit Beenden der `vm stop` Befehl.</span><span class="sxs-lookup"><span data-stu-id="7de6b-103">We can stop a running VM with the `vm stop` command.</span></span> <span data-ttu-id="7de6b-104">Sie müssen den Namen und die Ressourcengruppe oder die eindeutige ID für den virtuellen Computer übergeben:</span><span class="sxs-lookup"><span data-stu-id="7de6b-104">You must pass the name and resource group, or the unique ID for the VM:</span></span>

```azurecli
az vm stop -n SampleVM -g ExerciseResources
```

<span data-ttu-id="7de6b-105">Wir können sicherstellen, es wurde von beendet, es wird versucht, die öffentliche IP-Adresse pingen, die mithilfe von `ssh`, oder über die `vm get-instance-view` Befehl.</span><span class="sxs-lookup"><span data-stu-id="7de6b-105">We can verify it has stopped by attempting to ping the public IP address, using `ssh`, or through the `vm get-instance-view` command.</span></span> <span data-ttu-id="7de6b-106">Dieser letzte Ansatz gibt die gleichen grundlegenden Daten wie `vm show` aber enthält Details über die Instanz selbst.</span><span class="sxs-lookup"><span data-stu-id="7de6b-106">This final approach returns the same basic data as `vm show` but includes details about the instance itself.</span></span> <span data-ttu-id="7de6b-107">Wiederholen Sie den folgenden Befehl eingeben, in der Cloud-Shell, um den aktuellen Ausführungsstatus des virtuellen Computers finden Sie unter:</span><span class="sxs-lookup"><span data-stu-id="7de6b-107">Try typing the following command into the Cloud Shell to see the current running state of your VM:</span></span>

```azurecli
az vm get-instance-view -n SampleVM -g ExerciseResources --query "instanceView.statuses[?starts_with(code, 'PowerState/') == `true`].displayStatus" -o tsv
```

<span data-ttu-id="7de6b-108">Dieser Befehl sollte zurückgeben `VM stopped` als Ergebnis.</span><span class="sxs-lookup"><span data-stu-id="7de6b-108">This command should return `VM stopped` as the result.</span></span>

## <a name="starting-a-vm"></a><span data-ttu-id="7de6b-109">Starten eines virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="7de6b-109">Starting a VM</span></span>

<span data-ttu-id="7de6b-110">Können wir das Gegenteil durch die `vm start` Befehl.</span><span class="sxs-lookup"><span data-stu-id="7de6b-110">We can do the reverse through the `vm start` command.</span></span>

```azurecli
az vm start -n SampleVM -g ExerciseResources
```

<span data-ttu-id="7de6b-111">Dieser Befehl startet einen angehaltenen virtuellen Computer.</span><span class="sxs-lookup"><span data-stu-id="7de6b-111">This command will start a stopped VM.</span></span> <span data-ttu-id="7de6b-112">Wir können es durch Überprüfen der `vm get-instance-view` Abfrage, die jetzt zurückgeben soll `VM running`.</span><span class="sxs-lookup"><span data-stu-id="7de6b-112">We can verify it through the `vm get-instance-view` query, which should now return `VM running`.</span></span>

## <a name="restarting-a-vm"></a><span data-ttu-id="7de6b-113">Neustarten eines virtuellen Computers</span><span class="sxs-lookup"><span data-stu-id="7de6b-113">Restarting a VM</span></span>

<span data-ttu-id="7de6b-114">Schließlich können wir einen virtuellen Computer starten, wenn wir Änderungen vorgenommen haben, die erfordern einen Neustart mit dem `vm restart` Befehl.</span><span class="sxs-lookup"><span data-stu-id="7de6b-114">Finally, we can restart a VM if we have made changes that require a reboot using the `vm restart` command.</span></span> <span data-ttu-id="7de6b-115">Sie können hinzufügen, die `--no-wait` auszugeben, wenn Sie die CLI sofort zurückgegeben, ohne zu warten, für den virtuellen Computer neu starten möchten.</span><span class="sxs-lookup"><span data-stu-id="7de6b-115">You can add the `--no-wait` flag if you want the CLI to return immediately without waiting for the VM to reboot.</span></span>

