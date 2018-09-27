<span data-ttu-id="5ad59-101">::: zone pivot="csharp" Lassen Sie uns die Azure Storage-Clientbibliothek in Ihre .NET Core-Konsolenanwendung integrieren.</span><span class="sxs-lookup"><span data-stu-id="5ad59-101">::: zone pivot="csharp" Let's integrate the Azure Storage client library into your .NET Core console application.</span></span>

<span data-ttu-id="5ad59-102">Die Azure Storage-Clientbibliothek für .NET wird mit NuGet verteilt.</span><span class="sxs-lookup"><span data-stu-id="5ad59-102">The Azure storage client library for .NET is distributed with NuGet.</span></span> <span data-ttu-id="5ad59-103">Nach Wunsch können Sie das Paket **WindowsAzure.Storage** Ihren .NET- oder .NET Core-Anwendungen hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="5ad59-103">You will want to add the **WindowsAzure.Storage** package to your .NET or .NET Core applications.</span></span>

## <a name="add-the-azure-storage-nuget-package"></a><span data-ttu-id="5ad59-104">Hinzufügen des NuGet-Pakets für Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5ad59-104">Add the Azure Storage NuGet package</span></span>

1. <span data-ttu-id="5ad59-105">Wechseln Sie im Terminal mit `cd` in das Verzeichnis PhotoSharingApp, wenn Sie sich nicht bereits dort befinden.</span><span class="sxs-lookup"><span data-stu-id="5ad59-105">In the terminal, `cd` to the PhotoSharingApp directory if you aren't already there.</span></span>

1. <span data-ttu-id="5ad59-106">Fügen Sie das Paket **WindowsAzure.Storage** der Anwendung hinzu.</span><span class="sxs-lookup"><span data-stu-id="5ad59-106">Add the **WindowsAzure.Storage** package to the application.</span></span>

    ```bash
    dotnet add package WindowsAzure.Storage
    ```

1. <span data-ttu-id="5ad59-107">Dies sollte zu Konsolenaktivität führen, während die Clientbibliothek und alle erforderlichen Abhängigkeiten heruntergeladen werden.</span><span class="sxs-lookup"><span data-stu-id="5ad59-107">This should result in some console activity while the client library and all the required dependencies are downloaded.</span></span> <span data-ttu-id="5ad59-108">Sobald dies erledigt ist, können Sie einen Build für die App erstellen und sie erneut ausführen, um sicherzustellen, dass alles betriebsbereit ist.</span><span class="sxs-lookup"><span data-stu-id="5ad59-108">Once it's done, go ahead and build and run the app again to make sure everything is ready to go.</span></span>

    ```bash
    dotnet run
    ```

1. <span data-ttu-id="5ad59-109">Wie zuvor sollte „Hello World!“ ausgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="5ad59-109">As before, it should output "Hello World!".</span></span>

<span data-ttu-id="5ad59-110">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="5ad59-110">::: zone-end</span></span>

<span data-ttu-id="5ad59-111">::: zone pivot="javascript"</span><span class="sxs-lookup"><span data-stu-id="5ad59-111">::: zone pivot="javascript"</span></span>

<span data-ttu-id="5ad59-112">Nun wollen wir die **Microsoft Azure Storage-Clientbibliothek für Node.js und JavaScript** in Ihre Anwendung integrieren.</span><span class="sxs-lookup"><span data-stu-id="5ad59-112">Let's integrate the **Microsoft Azure Storage Client Library for Node.js and JavaScript** into your application.</span></span>

<span data-ttu-id="5ad59-113">Die Clientbibliothek für Node.js steht über den Node Package Manager (npm) zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="5ad59-113">The client library for Node.js is available through the Node Package manager (NPM).</span></span> <span data-ttu-id="5ad59-114">Fügen Sie das Paket **azure-storage** Ihrer Datei **packages.json** hinzu.</span><span class="sxs-lookup"><span data-stu-id="5ad59-114">You will want to add the **azure-storage** package to your **packages.json** file.</span></span>

> [!NOTE]
> <span data-ttu-id="5ad59-115">Die **Microsoft Azure Storage-Clientbibliothek für Node.js und JavaScript** ist für Serveranwendungen vorgesehen.</span><span class="sxs-lookup"><span data-stu-id="5ad59-115">The **Microsoft Azure Storage Client Library for Node.js and JavaScript** is intended for server applications.</span></span> <span data-ttu-id="5ad59-116">Wenn Sie clientseitigen JavaScript-Code ausführen, sollten Sie die **Azure Storage-Clientbibliothek für JavaScript** verwenden, die die gleiche Funktionalität bietet, aber auf die Ausführung in einem Browser ausgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="5ad59-116">If you are doing client-side JavaScript, you will want to use the **Azure Storage Client Library for JavaScript**, which provides the same functionality but is tailored to running in a browser.</span></span>

## <a name="add-the-azure-storage-package"></a><span data-ttu-id="5ad59-117">Hinzufügen des Azure Storage-Pakets</span><span class="sxs-lookup"><span data-stu-id="5ad59-117">Add the Azure Storage package</span></span>

1. <span data-ttu-id="5ad59-118">Wechseln Sie in Cloud Shell mit `cd` in das Verzeichnis PhotoSharingApp, wenn Sie nicht bereits dort sind.</span><span class="sxs-lookup"><span data-stu-id="5ad59-118">In Cloud Shell, `cd` to the PhotoSharingApp directory if you aren't already there.</span></span>

1. <span data-ttu-id="5ad59-119">Fügen Sie das Paket **azure-storage** der Anwendung hinzu.</span><span class="sxs-lookup"><span data-stu-id="5ad59-119">Add the **azure-storage** package to the application.</span></span> <span data-ttu-id="5ad59-120">Geben Sie unbedingt die Option `--save` an, damit ein Speichern in **packages.json** erfolgt.</span><span class="sxs-lookup"><span data-stu-id="5ad59-120">Make sure to supply the `--save` option so it persists to **packages.json**.</span></span>

    ```bash
    npm install azure-storage --save
    ```

1. <span data-ttu-id="5ad59-121">Dies sollte zu Konsolenaktivität führen, während die Clientbibliothek und alle erforderlichen Abhängigkeiten heruntergeladen werden.</span><span class="sxs-lookup"><span data-stu-id="5ad59-121">This should result in some console activity while the client library and all the required dependencies are downloaded.</span></span> <span data-ttu-id="5ad59-122">Sobald dies erledigt ist, können Sie einen Build für die App erstellen und sie erneut ausführen, um sicherzustellen, dass alles betriebsbereit ist.</span><span class="sxs-lookup"><span data-stu-id="5ad59-122">Once it's done, go ahead and build and run the app again to make sure everything is ready to go.</span></span>

    ```bash
    node index.js
    ```

1. <span data-ttu-id="5ad59-123">Wie zuvor sollte „Hello, World!“ ausgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="5ad59-123">As before, it should output "Hello, World!"</span></span>

<span data-ttu-id="5ad59-124">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="5ad59-124">::: zone-end</span></span>

<span data-ttu-id="5ad59-125">Nun, da wir über die notwendigen Bibliotheken verfügen, lassen Sie uns einen Blick auf die allgemeinen Aufgaben werfen, die Sie in Ihrem Code erledigen müssen, um mit Azure Storage zu arbeiten.</span><span class="sxs-lookup"><span data-stu-id="5ad59-125">Now that we have the necessary libraries in place, let's look at the common tasks you'll do in your code to work with Azure storage.</span></span>
