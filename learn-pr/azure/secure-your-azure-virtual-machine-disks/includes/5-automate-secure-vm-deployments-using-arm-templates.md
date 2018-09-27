<span data-ttu-id="8bcbf-101">Angenommen, Ihr Unternehmen stellt im Rahmen ihrer Cloudmigration mehrere Server bereit.</span><span class="sxs-lookup"><span data-stu-id="8bcbf-101">Suppose your company is deploying several servers as part of their cloud transition.</span></span> <span data-ttu-id="8bcbf-102">VM-Datenträger müssen bei der Bereitstellung verschlüsselt werden, damit sie zu keinem Zeitpunkt angreifbar sind.</span><span class="sxs-lookup"><span data-stu-id="8bcbf-102">VM disks must be encrypted during the deployment, so there's no time when the disks are vulnerable.</span></span> <span data-ttu-id="8bcbf-103">Sie möchten diesen Prozess automatisieren und müssen die Azure Resource Manager-Vorlagen ändern, damit die Verschlüsselung automatisch aktiviert wird.</span><span class="sxs-lookup"><span data-stu-id="8bcbf-103">You want to automate this process, and have to modify the Azure Resource Manager templates to automatically enable encryption.</span></span>

<span data-ttu-id="8bcbf-104">Im Folgenden verwenden Sie eine Azure Resource Manager-Vorlage, um die Verschlüsselung für neue virtuelle Windows-Computer automatisch zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="8bcbf-104">Here, we'll look at how to use an Azure Resource Manager template to automatically enable encryption for new Windows VMs.</span></span>

## <a name="what-are-azure-resource-manager-templates"></a><span data-ttu-id="8bcbf-105">Was sind Azure Resource Manager-Vorlagen?</span><span class="sxs-lookup"><span data-stu-id="8bcbf-105">What are Azure Resource Manager templates?</span></span>

<span data-ttu-id="8bcbf-106">Resource Manager-Vorlagen sind JSON-Dateien zum Definieren einer Gruppe von Ressourcen, die in Azure bereitgestellt werden soll.</span><span class="sxs-lookup"><span data-stu-id="8bcbf-106">Resource Manager templates are JSON files used to define a set of resources to deploy to Azure.</span></span> <span data-ttu-id="8bcbf-107">Sie können von Grund auf neu erstellt werden. Bei einigen Ressourcen (unter anderem bei virtuellen Computern) besteht allerdings auch die Möglichkeit, sie über das Azure-Portal zu generieren.</span><span class="sxs-lookup"><span data-stu-id="8bcbf-107">You can write them from scratch, and for some Azure resources, including VMs, you can use the Azure portal to generate them.</span></span> <span data-ttu-id="8bcbf-108">Sie geben die erforderlichen Informationen für die manuelle Bereitstellung eines virtuellen Computers an, stellen den virtuellen Computer aber nicht in Azure bereit, sondern speichern die Vorlage.</span><span class="sxs-lookup"><span data-stu-id="8bcbf-108">You'll need to complete the required information for a manual VM deployment, but instead of deploying the VM to Azure, you save the template.</span></span> <span data-ttu-id="8bcbf-109">Anschließend können Sie die Vorlage _wiederverwenden_, um diese spezifische VM-Konfiguration zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="8bcbf-109">You can then _reuse_ the template to create that specific VM configuration.</span></span>

<span data-ttu-id="8bcbf-110">In der Dokumentation stehen [Beispielvorlagen](https://azure.microsoft.com/resources/templates) zur Automatisierung verschiedenster administrativer Aufgaben zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="8bcbf-110">There are [example templates available in docs](https://azure.microsoft.com/resources/templates) to automate all sorts of administrative tasks.</span></span> <span data-ttu-id="8bcbf-111">Zur Verschlüsselung des virtuellen Computers hätten Sie anstelle der manuellen Vorgehensweise auch eine dieser Vorlagen verwenden können.</span><span class="sxs-lookup"><span data-stu-id="8bcbf-111">In fact, we could have used one of these templates to encrypt our VM that we just did manually!</span></span>

![Screenshot mit Azure-Vorlagen](../media/5-browse-templates.png)

## <a name="using-github-templates"></a><span data-ttu-id="8bcbf-113">Verwenden von GitHub-Vorlagen</span><span class="sxs-lookup"><span data-stu-id="8bcbf-113">Using GitHub templates</span></span>

<span data-ttu-id="8bcbf-114">Die Quelldateien der Vorlage sind in GitHub gespeichert.</span><span class="sxs-lookup"><span data-stu-id="8bcbf-114">The actual template source is stored in GitHub.</span></span> <span data-ttu-id="8bcbf-115">Sie können in GitHub zur Vorlage navigieren und direkt über die Seite die Bereitstellung in Azure durchführen.</span><span class="sxs-lookup"><span data-stu-id="8bcbf-115">You can browse to a template in GitHub and deploy right to Azure from the page.</span></span>

![Screenshot mit GitHub-Vorlage und hervorgehobener Schaltfläche „Deploy to Azure“ (In Azure bereitstellen)](../media/5-deploy-from-github.png)

<span data-ttu-id="8bcbf-117">Bei der Bereitstellung der Vorlage wird in Azure eine Liste der Pflichteingabefelder angezeigt.</span><span class="sxs-lookup"><span data-stu-id="8bcbf-117">When the template is deployed, Azure will display a list of required input fields.</span></span>

![Screenshot mit Vorlage im Azure-Portal](../media/5-fill-in-template.png)

<span data-ttu-id="8bcbf-119">Anschließend können Sie die Vorlage ausführen, um Ressourcen zu erstellen, anzupassen oder zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="8bcbf-119">You can then execute the template to create, modify, or remove resources.</span></span>

### <a name="running-templates-in-the-azure-portal"></a><span data-ttu-id="8bcbf-120">Ausführen von Vorlagen im Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="8bcbf-120">Running templates in the Azure portal</span></span>

<span data-ttu-id="8bcbf-121">Wenn Sie bereits wissen, welche Vorlage Sie verwenden möchten, oder Vorlagen in Ihrem Azure-Konto gespeichert haben, können Sie über **Ressource erstellen** > **Vorlagenbereitstellung** nach definierten Vorlagen im Portal suchen und diese ausführen.</span><span class="sxs-lookup"><span data-stu-id="8bcbf-121">If you already know the template you want to use, or you have saved templates in your Azure account, you can use the **Create a resource** > **Template Deployment** resource to locate and run defined templates in the portal.</span></span> <span data-ttu-id="8bcbf-122">Sie können anhand des Namens nach Vorlagen suchen, eine Vorlage bearbeiten, um die Parameter oder das Verhalten zu ändern, und die Vorlage direkt über die grafische Benutzeroberfläche ausführen.</span><span class="sxs-lookup"><span data-stu-id="8bcbf-122">You can search through templates by name, edit a template to change the parameters or behavior, and execute the template right from the GUI.</span></span>

### <a name="running-templates-from-the-command-line"></a><span data-ttu-id="8bcbf-123">Ausführen von Vorlagen über die Befehlszeile</span><span class="sxs-lookup"><span data-stu-id="8bcbf-123">Running templates from the command line</span></span>

<span data-ttu-id="8bcbf-124">Mit einer Vorlagen-URL können Sie die Vorlage in Azure PowerShell ausführen.</span><span class="sxs-lookup"><span data-stu-id="8bcbf-124">Given a URL to a template, you can execute it with Azure PowerShell.</span></span> <span data-ttu-id="8bcbf-125">Beispielsweise könnten Sie die Verschlüsselungsvorlage für Datenträger mit dem folgenden PowerShell-Befehl ausführen:</span><span class="sxs-lookup"><span data-stu-id="8bcbf-125">For example, we could run the disk encryption template with the following PowerShell command:</span></span>

```powershell
New-AzureRmResourceGroupDeployment `
    -Name encrypt-disk `
    -ResourceGroupName <resource-group-name> `
    -TemplateUri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-encrypt-running-windows-vm-without-aad/azuredeploy.json
```

<span data-ttu-id="8bcbf-126">Alternativ können Sie auch die Azure CLI und den Befehl `group deployment create` verwenden.</span><span class="sxs-lookup"><span data-stu-id="8bcbf-126">Or, if you prefer the Azure CLI, with the `group deployment create` command.</span></span>

```azurecli
azure config mode arm
azure group deployment create <my-resource-group> <my-deployment-name> \ 
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-encrypt-running-windows-vm-without-aad/azuredeploy.json
```

