<span data-ttu-id="54004-101">Erstellen Sie eine Client-App für die Arbeit mit einer Warteschlange.</span><span class="sxs-lookup"><span data-stu-id="54004-101">Let's create a client application to work with a queue.</span></span> <span data-ttu-id="54004-102">Anschließend fügen Sie die Verbindungszeichenfolge in den Code ein.</span><span class="sxs-lookup"><span data-stu-id="54004-102">Then we'll add our connection string to the code.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="54004-103">Erstellen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="54004-103">Create the application</span></span>

<span data-ttu-id="54004-104">Erstellen Sie eine .NET Core-Anwendung, die Sie unter Linux, macOS oder Windows ausführen können.</span><span class="sxs-lookup"><span data-stu-id="54004-104">We'll create a .NET Core application that you can run on Linux, macOS, or Windows.</span></span> <span data-ttu-id="54004-105">Geben Sie ihr den Namen **QueueApp**.</span><span class="sxs-lookup"><span data-stu-id="54004-105">Let's name it **QueueApp**.</span></span> <span data-ttu-id="54004-106">Der Einfachheit halber verwenden Sie hierzu eine einzelne App, die Nachrichten über die Warteschlange sendet und empfängt.</span><span class="sxs-lookup"><span data-stu-id="54004-106">For simplicity, we'll use a single app that will both send and receive messages through our queue.</span></span>

1. <span data-ttu-id="54004-107">Verwenden Sie den Befehl `dotnet new`, um eine neue Konsolenanwendung mit dem Namen **QueueApp** zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="54004-107">Use the `dotnet new` command to create a new console app with the name **QueueApp**.</span></span> <span data-ttu-id="54004-108">Sie können Befehle rechts in Cloud Shell eingeben. Wenn Sie lokal arbeiten, verwenden Sie alternativ ein Terminal bzw. ein Konsolenfenster.</span><span class="sxs-lookup"><span data-stu-id="54004-108">You can type commands into the Cloud Shell on the right, or if you are working locally, in a terminal/console window.</span></span> <span data-ttu-id="54004-109">Hiermit wird eine einfache App mit einer einzelnen Quelldatei (`Program.cs`) erstellt.</span><span class="sxs-lookup"><span data-stu-id="54004-109">This creates a simple app with a single source file: `Program.cs`.</span></span>

    ```azurecli
    dotnet new console -n QueueApp
    ```

1. <span data-ttu-id="54004-110">Wechseln Sie zum neu erstellten `QueueApp`-Ordner, und erstellen Sie die App, um sicherzustellen, dass alles funktioniert hat.</span><span class="sxs-lookup"><span data-stu-id="54004-110">Switch to the newly created `QueueApp` folder and build the app to verify that all is well.</span></span>

    ```azurecli
    cd QueueApp
    ```

    ```azurecli
    dotnet build
    ```

## <a name="get-your-connection-string"></a><span data-ttu-id="54004-111">Abrufen der Verbindungszeichenfolge</span><span class="sxs-lookup"><span data-stu-id="54004-111">Get your connection string</span></span>

<span data-ttu-id="54004-112">Vergessen Sie nicht, dass Sie die Verbindungszeichenfolge im Azure-Portal im Abschnitt **Einstellungen > Zugriffsschlüssel** Ihres Speicherkontos finden.</span><span class="sxs-lookup"><span data-stu-id="54004-112">Recall that your connection string is available in the Azure portal **Settings > Access keys** section of your storage account.</span></span>

<span data-ttu-id="54004-113">Sie können sie auch über die Azure CLI oder PowerShell-Tools abrufen.</span><span class="sxs-lookup"><span data-stu-id="54004-113">You can also retrieve it through the Azure CLI or PowerShell tools.</span></span> <span data-ttu-id="54004-114">Verwenden Sie den Azure CLI-Befehl.</span><span class="sxs-lookup"><span data-stu-id="54004-114">Let's use the Azure CLI command.</span></span> <span data-ttu-id="54004-115">Denken Sie daran, `<name>` durch den spezifischen Namen des Speicherkontos zu ersetzen, das Sie erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="54004-115">Remember to replace the `<name>` with the specific name of the storage account you created.</span></span> <span data-ttu-id="54004-116">Sie können `az storage account list` verwenden, wenn Sie eine Erinnerung benötigen.</span><span class="sxs-lookup"><span data-stu-id="54004-116">You can use `az storage account list` if you need a reminder.</span></span>

```azurecli
az storage account show-connection-string --name <name> --resource-group ExerciseResources
```

<span data-ttu-id="54004-117">Dieser Befehl gibt einen JSON-Block mit Ihrer Verbindungszeichenfolge zurück.</span><span class="sxs-lookup"><span data-stu-id="54004-117">This command will return a JSON block with your connection string.</span></span> <span data-ttu-id="54004-118">Er enthält den Namen und den Kontoschlüssel des Speicherkontos:</span><span class="sxs-lookup"><span data-stu-id="54004-118">It will include the storage account name and the account key:</span></span>

```json
{
  "connectionString": "DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=<name>;AccountKey=vyw6aKz2PtSAgQ4ljJQgJFgxbCETdXt39ZyYQ5fLqoBJj/gT+43TbrhoVco7Rqj/AAJVlvFORRfnYqGHiX9QcQ=="
}
```

## <a name="add-the-connection-string-to-the-application"></a><span data-ttu-id="54004-119">Hinzufügen der Verbindungszeichenfolge in die Anwendung</span><span class="sxs-lookup"><span data-stu-id="54004-119">Add the connection string to the application</span></span>

<span data-ttu-id="54004-120">Abschließend fügen Sie die Verbindungszeichenfolge in die App ein, damit sie auf das Speicherkonto zugreifen kann.</span><span class="sxs-lookup"><span data-stu-id="54004-120">Finally, let's add the connection string into our app so it can access the storage account.</span></span>

> [!WARNING]
> <span data-ttu-id="54004-121">Der Einfachheit halber platzieren Sie die Verbindungszeichenfolge in die Datei **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="54004-121">For simplicity, you will place the connection string in the **Program.cs** file.</span></span> <span data-ttu-id="54004-122">Für eine Produktionsanwendung sollten Sie sie an einem sicheren Ort speichern.</span><span class="sxs-lookup"><span data-stu-id="54004-122">In a production application, you should store it in a secure location.</span></span> <span data-ttu-id="54004-123">Für die serverseitige Verwendung wird Azure Key Vault empfohlen.</span><span class="sxs-lookup"><span data-stu-id="54004-123">For server side use, we recommend using Azure Key Vault.</span></span>

1. <span data-ttu-id="54004-124">Geben Sie `code .` im Terminal ein, um den Onlinecode-Editor zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="54004-124">Type `code .` in the terminal to open the online code editor.</span></span> <span data-ttu-id="54004-125">Wenn Sie alleine arbeiten, können Sie alternativ die IDE Ihrer Wahl verwenden.</span><span class="sxs-lookup"><span data-stu-id="54004-125">Alternatively, if you are working on your own you can use the IDE of your choice.</span></span> <span data-ttu-id="54004-126">Hierfür empfiehlt sich Visual Studio Code, da es sich dabei um eine hervorragende plattformübergreifende IDE handelt.</span><span class="sxs-lookup"><span data-stu-id="54004-126">We recommend Visual Studio Code, which is an excellent cross-platform IDE.</span></span>

1. <span data-ttu-id="54004-127">Öffnen Sie die Quelldatei `Program.cs` im Projekt.</span><span class="sxs-lookup"><span data-stu-id="54004-127">Open the `Program.cs` source file in the project.</span></span>

1. <span data-ttu-id="54004-128">Fügen Sie einen `const string`-Wert in die `Program`-Klasse hinzu, der die Verbindungszeichenfolge enthält.</span><span class="sxs-lookup"><span data-stu-id="54004-128">In the `Program` class, add a `const string` value to hold the connection string.</span></span> <span data-ttu-id="54004-129">Nur der Wert ist erforderlich (er beginnt mit dem Text **DefaultEndpointsProtocol**).</span><span class="sxs-lookup"><span data-stu-id="54004-129">You only need the value (it starts with the text **DefaultEndpointsProtocol**).</span></span>

1. <span data-ttu-id="54004-130">Speichern Sie die Datei.</span><span class="sxs-lookup"><span data-stu-id="54004-130">Save the file.</span></span> <span data-ttu-id="54004-131">Sie können in der rechten Ecke des Cloud-Editors auf die Schaltfläche mit den Auslassungspunkten (...) klicken, dabei wird Ihnen auch die Tastenkombination angezeigt.</span><span class="sxs-lookup"><span data-stu-id="54004-131">You can click the ellipse "..." in the right corner of the cloud editor, it will also show you the keyboard shortcut.</span></span>

<span data-ttu-id="54004-132">Der Code sollte etwa wie folgt aussehen (Ihr Zeichenfolgenwert ist für Ihr Konto eindeutig).</span><span class="sxs-lookup"><span data-stu-id="54004-132">Your code should look something like this (the string value will be unique to your account).</span></span>

```csharp
...
namespace QueueApp
{
    class Program
    {
        private const string ConnectionString = "DefaultEndpointsProtocol=https; ...";
        
        ...
    }
}
```

<span data-ttu-id="54004-133">Da Sie das Starterprojekt nun eingerichtet haben, sehen Sie sich als Nächstes an, wie Sie im Code mit einer Warteschlange arbeiten können.</span><span class="sxs-lookup"><span data-stu-id="54004-133">Now that we have this starter project setup, let's look at how to work with a queue in code.</span></span> <span data-ttu-id="54004-134">_Meldungen_ stellen den Anfang dar.</span><span class="sxs-lookup"><span data-stu-id="54004-134">It all starts with _messages_.</span></span>