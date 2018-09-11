<span data-ttu-id="ea51b-101">Sie haben mit der Azure CLI einen neuen virtuellen Linux-Computer erstellt, seine Größe geändert, ihn angehalten und gestartet und die Konfiguration aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="ea51b-101">You've created a new Linux virtual machine, changed its size, stopped and started it, and updated the configuration with the Azure CLI.</span></span>

## <a name="cleanup"></a><span data-ttu-id="ea51b-102">Bereinigen</span><span class="sxs-lookup"><span data-stu-id="ea51b-102">Cleanup</span></span>

<span data-ttu-id="ea51b-103">Jetzt sind wir mit dem Bearbeiten des virtuellen Computers fertig und benötigen ihn nicht mehr. Also löschen wir die Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="ea51b-103">Now that we're finished with the VM and no longer need it, let's delete the resources.</span></span> <span data-ttu-id="ea51b-104">Diese Bereinigung ist wichtig, damit die Compute- und Speicherressourcen nicht weiter für Ihr Konto abgerechnet werden.</span><span class="sxs-lookup"><span data-stu-id="ea51b-104">Cleanup is important for compute and storage resources that can continue to be billed against your account.</span></span> 

<span data-ttu-id="ea51b-105">Sie können mit dem Befehl „`delete`“ einzelne Ressourcen löschen. Die einfachste Methode besteht aber darin, mit „`az group delete`“ alles zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="ea51b-105">You can delete individual resources with the `delete` command, but the easiest way to remove everything is with `az group delete`.</span></span> <span data-ttu-id="ea51b-106">Führen Sie in der Azure CLI folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="ea51b-106">Execute the following command in the Azure CLI:</span></span>

```azurecli
az group delete --name ExerciseResources --no-wait
```

<span data-ttu-id="ea51b-107">Wenn Sie dazu aufgefordert werden, antworten Sie mit „yes“, oder verwenden Sie den `--yes`-Parameter, um die Antwort automatisch zu geben.</span><span class="sxs-lookup"><span data-stu-id="ea51b-107">Answer "yes" to the prompt when shown, or use the `--yes` parameter to auto-answer the prompt.</span></span>

<span data-ttu-id="ea51b-108">Dieser Befehl löscht alle der Ressourcengruppe zugeordneten Ressourcen und hebt ihre Zuordnung garantiert in der richtigen Reihenfolge auf.</span><span class="sxs-lookup"><span data-stu-id="ea51b-108">This command deletes all of the resources associated with the resource group, and is guaranteed to deallocate them in the correct order.</span></span> <span data-ttu-id="ea51b-109">Der Parameter „`--no-wait`“ verhindert eine Blockierung durch die Azure CLI, während der Löschvorgang ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="ea51b-109">The `--no-wait` parameter keeps the Azure CLI from blocking while the deletion takes place.</span></span> <span data-ttu-id="ea51b-110">Lassen Sie den Parameter deaktiviert, um zu warten, bis die Ressourcen gelöscht wurden.</span><span class="sxs-lookup"><span data-stu-id="ea51b-110">Leave it off to wait for the resources to be deleted.</span></span> <span data-ttu-id="ea51b-111">Sie können auch den `az group wait -n ExerciseResources --deleted`-Befehl später im Skript verwende, um darauf zu warten, dass der Löschvorgang beendet wird.</span><span class="sxs-lookup"><span data-stu-id="ea51b-111">Or use the `az group wait -n ExerciseResources --deleted` command later in your script to wait for the deletion to finish.</span></span>


## <a name="further-reading"></a><span data-ttu-id="ea51b-112">Weitere nützliche Informationen</span><span class="sxs-lookup"><span data-stu-id="ea51b-112">Further reading</span></span>

- [<span data-ttu-id="ea51b-113">Übersicht über die Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ea51b-113">Azure CLI overview</span></span>](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)
- [<span data-ttu-id="ea51b-114">Azure CLI-Befehlsreferenz</span><span class="sxs-lookup"><span data-stu-id="ea51b-114">Azure CLI command reference</span></span>](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest)
