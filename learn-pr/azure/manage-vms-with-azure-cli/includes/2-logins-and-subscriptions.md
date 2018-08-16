<span data-ttu-id="73545-101">Bevor wir beginnen, können die Syntax für das Azure-CLI-Tool zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="73545-101">Before we start, lets review the syntax for the Azure CLI tool.</span></span> <span data-ttu-id="73545-102">Wenn Sie ergriffen haben, die **Steuerelement Azure-Dienste mit der Azure-Befehlszeilenschnittstelle** -Modul, dann wissen Sie, dass es sich bei Azure CLI-Befehle in Form einer erfolgen:</span><span class="sxs-lookup"><span data-stu-id="73545-102">If you've taken the **Control Azure services with the Azure CLI** module, then you know that Azure CLI commands take the form of:</span></span>

```azurecli
az [command] [subcommand] [--parameter --parameter]
```

<span data-ttu-id="73545-103">Die `[command]` identifiziert den bestimmten Bereich von Azure, die Sie steuern möchten.</span><span class="sxs-lookup"><span data-stu-id="73545-103">The `[command]` identifies the specific area of Azure you want to control.</span></span> <span data-ttu-id="73545-104">Sie können z. B. Abonnementinformationen mit verwalten die `account` Befehls oder einer SQL-Datenbanken mit der `sql` Befehl.</span><span class="sxs-lookup"><span data-stu-id="73545-104">For example, you can manage subscription information with the `account` command, or SQL databases with the `sql` command.</span></span> <span data-ttu-id="73545-105">Die `[subcommand]` und `[--parameters]` sind abhängig von den Befehl mit dem Sie arbeiten.</span><span class="sxs-lookup"><span data-stu-id="73545-105">The `[subcommand]` and `[--parameters]` are then dependent upon the command you're working with.</span></span> 

<span data-ttu-id="73545-106">Sie können eine Liste der Befehle, Unterbefehle und Parameter anzeigen, geben Sie in einem Teilbefehl.</span><span class="sxs-lookup"><span data-stu-id="73545-106">You can view a list of commands, subcommands, and parameters by typing in a partial command.</span></span> <span data-ttu-id="73545-107">Geben z. B. `az` in der Befehlszeile erhalten Sie den Bildschirm Hilfe auf oberster Ebene, und geben `az vm` erhalten Sie alle die Unterbefehle für virtuelle Computer.</span><span class="sxs-lookup"><span data-stu-id="73545-107">For example typing `az` at the command line will give you the top-level help screen, and typing `az vm` will give you all the subcommands for virtual machines.</span></span> <span data-ttu-id="73545-108">Dieser Ansatz kann eine hervorragende Möglichkeit, untersuchen das CLI-Tool sein.</span><span class="sxs-lookup"><span data-stu-id="73545-108">This approach can be a great way to explore the CLI tool.</span></span>

> [!NOTE]
> <span data-ttu-id="73545-109">Wir werden im Browser gehostete Cloud Shell verwenden, um mit der Azure CLI zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="73545-109">We will be using the browser-hosted Cloud Shell to work with the Azure CLI.</span></span> <span data-ttu-id="73545-110">Wenn Sie von Ihrem lokalen Computer arbeiten möchten, alle geht es um Befehle können auch ausgeführt werden über die Befehlszeile [Installieren der Azure-Befehlszeilenschnittstelle](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="73545-110">If you prefer to work from your local machine, all of the commands we cover can also be executed from the command line by [installing the Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest).</span></span>

## <a name="log-into-azure"></a><span data-ttu-id="73545-111">Anmelden bei Azure</span><span class="sxs-lookup"><span data-stu-id="73545-111">Log into Azure</span></span>

<span data-ttu-id="73545-112">Das erste, was Sie tun, bei der Arbeit mit der Azure-Befehlszeilenschnittstelle ist die Anmeldung beim Azure-Konto.</span><span class="sxs-lookup"><span data-stu-id="73545-112">The first thing you'll do when working with the Azure CLI is to login to your Azure account.</span></span> <span data-ttu-id="73545-113">Dies erfolgt mit der `login` Befehl.</span><span class="sxs-lookup"><span data-stu-id="73545-113">This is done with the `login` command.</span></span> <span data-ttu-id="73545-114">Wenn Sie Cloud Shell verwenden, fallen in eine Schaltfläche, um sich bei Azure anmelden.</span><span class="sxs-lookup"><span data-stu-id="73545-114">If you're using the Cloud Shell, there will be a button to sign in to Azure.</span></span>

```azurecli
az login
```

<span data-ttu-id="73545-115">Dieser Befehl startet ein Browserfenster und ermöglichen es Ihnen, das Microsoft-Konto auswählen, die, das Sie verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="73545-115">This command will launch a browser window and allow you to select the Microsoft account you want to use.</span></span>

## <a name="working-with-subscriptions"></a><span data-ttu-id="73545-116">Arbeiten mit Abonnements</span><span class="sxs-lookup"><span data-stu-id="73545-116">Working with subscriptions</span></span>

<span data-ttu-id="73545-117">In diesem Modul wir in ein temporäres Abonnement erstellt haben, als einen Playground arbeiten, aber ein Abonnement in der Regel von Ihrem eigenen Konto verwenden.</span><span class="sxs-lookup"><span data-stu-id="73545-117">In this module, we will work in a temporary subscription created as a playground, but you will normally use a subscription from your own account.</span></span> <span data-ttu-id="73545-118">Wenn Sie über mehrere Abonnements verfügen, erhalten Sie eine eindeutig formatierte Liste von Abonnements unter Verwendung der `az account list --output table` Anweisung.</span><span class="sxs-lookup"><span data-stu-id="73545-118">If you have more than one subscription, you can get a clearly formatted list of subscriptions using the `az account list --output table` statement.</span></span>

```
Name                                  CloudName    SubscriptionId                        State    IsDefault
------------------------------------  -----------  ------------------------------------  -------  -----------
Contoso Legacy Resources              AzureCloud   abc13b0c-d2c4-64b2-9ac5-2f4cb819b752  Enabled  True
Visual Studio Enterprise              AzureCloud   233aebce-23c2-4572-c056-c029449e93ed  Enabled  False
```

<span data-ttu-id="73545-119">Beachten Sie, die der Befehl auch identifiziert den _Standard_ Abonnement, in dem alle Ihre Befehle gelten.</span><span class="sxs-lookup"><span data-stu-id="73545-119">Notice that the command also identifies the _default_ subscription where all your commands will apply.</span></span> <span data-ttu-id="73545-120">Wenn Sie in einem anderen Abonnement arbeiten lieber, können Sie mithilfe der `az account set --subscription "[name]"` Befehl.</span><span class="sxs-lookup"><span data-stu-id="73545-120">If you would prefer to work in a different subscription, you can use the `az account set --subscription "[name]"` command.</span></span> <span data-ttu-id="73545-121">Beispielsweise konnte wir unsere aktuelle Abonnement sein festgelegt `Visual Studio Enterprise` in der obigen Liste durch den folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="73545-121">For example, we could set our current subscription to be `Visual Studio Enterprise` from the above list through the following command:</span></span>

```azurecli
az account set --subscription "Visual Studio Enterprise"
```