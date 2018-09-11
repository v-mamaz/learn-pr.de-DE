<span data-ttu-id="45305-101">Bevor wir starten, sehen wir uns die Syntax für das Azure CLI-Tool an.</span><span class="sxs-lookup"><span data-stu-id="45305-101">Before we start, let's review the syntax for the Azure CLI tool.</span></span> <span data-ttu-id="45305-102">Wenn Sie das Modul **Steuern von Azure-Diensten mit der Azure CLI** abgeschlossen haben, wissen Sie bereits, dass die Azure CLI-Befehle folgende Form aufweisen:</span><span class="sxs-lookup"><span data-stu-id="45305-102">If you've taken the **Control Azure services with the Azure CLI** module, then you know that Azure CLI commands take the form of:</span></span>

```azurecli
az [command] [subcommand] [--parameter --parameter]
```

<span data-ttu-id="45305-103">Der `[command]` identifiziert den Azure-Bereich, den Sie steuern möchten.</span><span class="sxs-lookup"><span data-stu-id="45305-103">The `[command]` identifies the specific area of Azure you want to control.</span></span> <span data-ttu-id="45305-104">Sie können z.B. Abonnementinformationen mit dem `account`-Befehl oder SQL-Datenbanken mit dem `sql`-Befehl verwalten.</span><span class="sxs-lookup"><span data-stu-id="45305-104">For example, you can manage subscription information with the `account` command, or SQL databases with the `sql` command.</span></span> <span data-ttu-id="45305-105">„`[subcommand]`“ und „`[--parameters]`“ richten sich dann nach dem Befehl, mit dem Sie arbeiten.</span><span class="sxs-lookup"><span data-stu-id="45305-105">The `[subcommand]` and `[--parameters]` are then dependent upon the command you're working with.</span></span> 

<span data-ttu-id="45305-106">Sie können eine Liste der Befehle, Unterbefehle und Parameter anzeigen, indem Sie einen Teilbefehl eingeben.</span><span class="sxs-lookup"><span data-stu-id="45305-106">You can view a list of commands, subcommands, and parameters by typing in a partial command.</span></span> <span data-ttu-id="45305-107">Wenn Sie beispielsweise „`az`“ in der Befehlszeile eingeben, erhalten Sie einen Hilfebildschirm auf der obersten Ebene. Mit der Eingabe von „`az vm`“ erhalten Sie alle Unterbefehle für virtuelle Computer.</span><span class="sxs-lookup"><span data-stu-id="45305-107">For example, typing `az` at the command line will give you the top-level help screen, and typing `az vm` will give you all the subcommands for virtual machines.</span></span> <span data-ttu-id="45305-108">Dieser Ansatz bietet eine hervorragende Möglichkeit, das Azure CLI-Tool zu erkunden.</span><span class="sxs-lookup"><span data-stu-id="45305-108">This approach can be a great way to explore the Azure CLI tool.</span></span>

> [!NOTE]
> <span data-ttu-id="45305-109">Wir verwenden den im Browser gehosteten Azure Cloud Shell-Dienst, um mit der Azure CLI zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="45305-109">We will be using browser-hosted Azure Cloud Shell to work with the Azure CLI.</span></span> <span data-ttu-id="45305-110">Wenn Sie lieber auf Ihrem lokalen Computer arbeiten, können Sie alle hier erläuterten Befehle auch über die Befehlszeile ausführen, indem Sie die [Azure CLI installieren](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="45305-110">If you prefer to work from your local machine, all of the commands we cover can also be executed from the command line by [installing the Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="45305-111">Anmelden an Azure</span><span class="sxs-lookup"><span data-stu-id="45305-111">Log in to Azure</span></span>

<span data-ttu-id="45305-112">Wenn Sie mit der Azure CLI arbeiten, müssen Sie sich zunächst bei Ihrem Azure-Konto anmelden.</span><span class="sxs-lookup"><span data-stu-id="45305-112">The first thing you'll do when working with the Azure CLI is to log in to your Azure account.</span></span> <span data-ttu-id="45305-113">Dies erfolgt über den `login`-Befehl.</span><span class="sxs-lookup"><span data-stu-id="45305-113">This is done with the `login` command.</span></span> <span data-ttu-id="45305-114">Wenn Sie Cloud Shell verwenden, können Sie sich mithilfe einer Schaltfläche bei Azure anmelden.</span><span class="sxs-lookup"><span data-stu-id="45305-114">If you're using Cloud Shell, there will be a button to sign in to Azure.</span></span>

```azurecli
az login
```

<span data-ttu-id="45305-115">Dieser Befehl startet ein Browserfenster und ermöglicht Ihnen die Auswahl des Microsoft-Kontos, das Sie verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="45305-115">This command will launch a browser window and allow you to select the Microsoft account you want to use.</span></span>

## <a name="working-with-subscriptions"></a><span data-ttu-id="45305-116">Arbeiten mit Abonnements</span><span class="sxs-lookup"><span data-stu-id="45305-116">Working with subscriptions</span></span>

<span data-ttu-id="45305-117">In diesem Modul arbeiten wir in einem temporären Abonnement, das für Übungszwecke erstellt wurde. Normalerweise verwenden Sie aber ein Abonnement aus Ihrem eigenen Konto.</span><span class="sxs-lookup"><span data-stu-id="45305-117">In this module, we will work in a temporary subscription created as a playground, but you will normally use a subscription from your own account.</span></span> <span data-ttu-id="45305-118">Wenn Sie über mehrere Abonnements verfügen, können Sie mit der `az account list --output table`-Anweisung eine formatierte Liste der Abonnements abrufen.</span><span class="sxs-lookup"><span data-stu-id="45305-118">If you have more than one subscription, you can get a clearly formatted list of subscriptions using the `az account list --output table` statement.</span></span>

```
Name                                  CloudName    SubscriptionId                        State    IsDefault
------------------------------------  -----------  ------------------------------------  -------  -----------
Contoso Legacy Resources              AzureCloud   abc13b0c-d2c4-64b2-9ac5-2f4cb819b752  Enabled  True
Visual Studio Enterprise              AzureCloud   233aebce-23c2-4572-c056-c029449e93ed  Enabled  False
```

<span data-ttu-id="45305-119">Beachten Sie, dass der Befehl auch das _standardmäßige_ Abonnement identifiziert, in dem all Ihre Befehle gelten.</span><span class="sxs-lookup"><span data-stu-id="45305-119">Notice that the command also identifies the _default_ subscription where all your commands will apply.</span></span> <span data-ttu-id="45305-120">Wenn Sie lieber mit einem anderen Abonnement arbeiten möchten, können Sie den `az account set --subscription "[name]"`-Befehl verwenden.</span><span class="sxs-lookup"><span data-stu-id="45305-120">If you would prefer to work in a different subscription, you can use the `az account set --subscription "[name]"` command.</span></span> <span data-ttu-id="45305-121">Sie können z.B. das aktuelle Abonnement mit dem folgenden Befehl auf „`Visual Studio Enterprise`“ aus der oben stehenden Liste festlegen:</span><span class="sxs-lookup"><span data-stu-id="45305-121">For example, we could set our current subscription to be `Visual Studio Enterprise` from the above list through the following command:</span></span>

```azurecli
az account set --subscription "Visual Studio Enterprise"
```