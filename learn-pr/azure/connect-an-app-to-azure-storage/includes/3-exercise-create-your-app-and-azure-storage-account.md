<span data-ttu-id="e480b-101">In dieser Einheit erfahren Sie, wie Sie eine .NET Core-Konsolenanwendung und ein Azure-Speicherkonto erstellen können.</span><span class="sxs-lookup"><span data-stu-id="e480b-101">In this unit, you will create a .NET Core console application and an Azure storage account.</span></span>

## <a name="create-a-net-core-console-application"></a><span data-ttu-id="e480b-102">Erstellen einer .NET Core-Konsolenanwendung</span><span class="sxs-lookup"><span data-stu-id="e480b-102">Create a .NET Core console application</span></span>

<span data-ttu-id="e480b-103">In diesem Beispiel wird Visual Studio 2017 verwendet, um Ihre App zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="e480b-103">We will be using Visual Studio 2017 to create our app.</span></span>

1. <span data-ttu-id="e480b-104">Klicken Sie in Visual Studio 2017 auf die Menüoption **Datei** > **Neu** > **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="e480b-104">In Visual Studio 2017, select the **File** > **New** > **Project** menu option.</span></span>

1. <span data-ttu-id="e480b-105">Klicken Sie in der Kategorie **Visual C# - .NET Core** auf **Console App (.NET Core)** (Konsolen-App (.NET Core)), geben Sie einen Namen für Ihre App ein, und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="e480b-105">Within the **Visual C# - .NET Core** category, select **Console App (.NET Core)**, enter a name for your app and select **OK**.</span></span>
  <span data-ttu-id="e480b-106">![Neue App](..\media-draft\3-new-console-app.png)</span><span class="sxs-lookup"><span data-stu-id="e480b-106">![New App](..\media-draft\3-new-console-app.png)</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="e480b-107">Erstellen eines Azure-Speicherkontos</span><span class="sxs-lookup"><span data-stu-id="e480b-107">Create an Azure storage account</span></span>

<span data-ttu-id="e480b-108">Sie müssen zunächst ein Speicherkonto erstellen, damit Sie eine Verbindung mit diesem herstellen können.</span><span class="sxs-lookup"><span data-stu-id="e480b-108">In order to connect to an Azure storage account, we must first create a storage account to connect to.</span></span>

1. <span data-ttu-id="e480b-109">Klicken Sie oben links im Azure-Portal auf „Create a resource“ (Ressource erstellen).</span><span class="sxs-lookup"><span data-stu-id="e480b-109">In the top left of the Azure Portal, select 'Create a resource'.</span></span>

1. <span data-ttu-id="e480b-110">Klicken Sie im angezeigten Auswahlbereich auf „Storage“.</span><span class="sxs-lookup"><span data-stu-id="e480b-110">In the selection pane that appears, select 'Storage'.</span></span>

1. <span data-ttu-id="e480b-111">Klicken Sie rechts in diesem Bereich auf „Speicherkonto – Blob, Datei, Tabelle, Warteschlange“.</span><span class="sxs-lookup"><span data-stu-id="e480b-111">On the right side of that pane, select 'Storage account - blob, file, table, queue'.</span></span>
  <span data-ttu-id="e480b-112">![Portalauswahl](..\media-draft\3-portal-storage-select.png)</span><span class="sxs-lookup"><span data-stu-id="e480b-112">![portal select](..\media-draft\3-portal-storage-select.png)</span></span>

1. <span data-ttu-id="e480b-113">Sie müssen die Informationen zu diesem Speicherkonto eingeben.</span><span class="sxs-lookup"><span data-stu-id="e480b-113">The details of the storage account need to be entered.</span></span> <span data-ttu-id="e480b-114">Geben Sie einen Namen für das Speicherkonto an.</span><span class="sxs-lookup"><span data-stu-id="e480b-114">Enter a name for the storage account.</span></span>

1. <span data-ttu-id="e480b-115">Eine Ressourcengruppe ist ein logischer Container für Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="e480b-115">A resource group is a logical container for resources.</span></span> <span data-ttu-id="e480b-116">Klicken Sie unter „Ressourcengruppe“ auf die Option **Neu erstellen**, und geben Sie einen Namen für die Ressourcengruppe ein.</span><span class="sxs-lookup"><span data-stu-id="e480b-116">For the resource group selection, select **Create New** and enter a name for your resource group.</span></span>

1. <span data-ttu-id="e480b-117">Behalten Sie für alle anderen Optionen die Standardwerte bei, und klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="e480b-117">Leave all other options at their default values and click **Create**.</span></span>
  <span data-ttu-id="e480b-118">![Portaldetails](..\media-draft\3-portal-storage-details.png)</span><span class="sxs-lookup"><span data-stu-id="e480b-118">![Portal details](..\media-draft\3-portal-storage-details.png).</span></span>

<span data-ttu-id="e480b-119">Dann wird Ihre Ressourcengruppe bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="e480b-119">Your resource group is now being provisioned.</span></span> <span data-ttu-id="e480b-120">Anschließend wird Ihr Speicherkonto innerhalb der Ressourcengruppe erstellt.</span><span class="sxs-lookup"><span data-stu-id="e480b-120">After that, your storage account is created within the resource group.</span></span>
<span data-ttu-id="e480b-121">Dann haben Sie Ihre Anwendung erstellt und können sie jetzt konfigurieren und mit Ihrem Speicherkonto verbinden.</span><span class="sxs-lookup"><span data-stu-id="e480b-121">Additionally, you have created your application and are ready to configure and connect it to your storage account.</span></span>
