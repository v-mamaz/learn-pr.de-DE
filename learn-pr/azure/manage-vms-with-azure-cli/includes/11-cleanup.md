<span data-ttu-id="80129-101">Sie haben einen neuen virtuellen Linux-Computer erstellt, seine Größe geändert, beendet und gestartet und aktualisiert die Konfiguration mit der Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="80129-101">You've created a new Linux virtual machine, changed its size, stopped and started it, and updated the configuration with the Azure CLI.</span></span>

## <a name="cleanup"></a><span data-ttu-id="80129-102">Cleanup</span><span class="sxs-lookup"><span data-stu-id="80129-102">Cleanup</span></span>

<span data-ttu-id="80129-103">Nun, wir sind nun mit dem virtuellen Computer fertig, und ihn nicht mehr benötigen, löschen wir die Ressourcen an.</span><span class="sxs-lookup"><span data-stu-id="80129-103">Now that we're finished with the VM and no longer need it, let's delete the resources.</span></span> <span data-ttu-id="80129-104">Bereinigung ist wichtig für Compute und Speicher-Ressourcen, die über Ihr Konto abgerechnet werden fortgesetzt werden können.</span><span class="sxs-lookup"><span data-stu-id="80129-104">Cleanup is important for compute and storage resources that can continue to be billed against your account.</span></span> 

<span data-ttu-id="80129-105">Sie können einzelne Ressourcen Löschen der `delete` Befehl, doch die einfachste Möglichkeit, alles zu entfernen ist `az group delete`.</span><span class="sxs-lookup"><span data-stu-id="80129-105">You can delete individual resources with the `delete` command, but the easiest way to remove everything is with `az group delete`.</span></span> <span data-ttu-id="80129-106">Führen Sie den folgenden Befehl in der Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="80129-106">Execute the following command in the Azure CLI:</span></span>

```azurecli
az group delete --name ExerciseResources --no-wait
```

<span data-ttu-id="80129-107">Beantworten Sie "Ja", auf die Aufforderung, wenn Sie angezeigt werden soll, oder verwenden Sie die `--yes` Parameter an der Eingabeaufforderung automatische Antworten.</span><span class="sxs-lookup"><span data-stu-id="80129-107">Answer "yes" to the prompt when shown, or use the `--yes` parameter to auto-answer the prompt.</span></span>

<span data-ttu-id="80129-108">Dieser Befehl löscht alle Ressourcen der Ressourcengruppe zugeordnet und ist garantiert, sie in der richtigen Reihenfolge aufgehoben.</span><span class="sxs-lookup"><span data-stu-id="80129-108">This command deletes all of the resources associated with the resource group, and is guaranteed to deallocate them in the correct order.</span></span> <span data-ttu-id="80129-109">Der Parameter `--no-wait` verhindert eine Blockierung durch die CLI, während der Löschvorgang ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="80129-109">The `--no-wait` parameter keeps the CLI from blocking while the deletion takes place.</span></span> <span data-ttu-id="80129-110">Lassen Sie sie aus, warten, bis die Ressourcen gelöscht werden soll.</span><span class="sxs-lookup"><span data-stu-id="80129-110">Leave it off to wait for the resources to be deleted.</span></span> <span data-ttu-id="80129-111">Oder verwenden Sie die `az group wait -n ExerciseResources --deleted` Befehl später im Skript zu warten, bis der Löschvorgang abgeschlossen.</span><span class="sxs-lookup"><span data-stu-id="80129-111">Or use the `az group wait -n ExerciseResources --deleted` command later in your script to wait for the deletion to complete.</span></span>


## <a name="further-reading"></a><span data-ttu-id="80129-112">Weitere Informationen</span><span class="sxs-lookup"><span data-stu-id="80129-112">Further reading</span></span>

* [<span data-ttu-id="80129-113">Übersicht über die Azure CLI</span><span class="sxs-lookup"><span data-stu-id="80129-113">Azure CLI Overview</span></span>](https://docs.microsoft.com/en-us/cli/azure/?view=azure-cli-latest)
* [<span data-ttu-id="80129-114">Azure CLI-Befehlsreferenz</span><span class="sxs-lookup"><span data-stu-id="80129-114">Azure CLI command reference</span></span>](https://docs.microsoft.com/en-us/cli/azure/reference-index?view=azure-cli-latest)
