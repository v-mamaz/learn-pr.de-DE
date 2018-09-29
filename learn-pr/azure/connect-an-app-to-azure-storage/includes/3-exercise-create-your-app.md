<span data-ttu-id="99c35-101">Zur Erinnerung: Wir arbeiten an einer Anwendung zum Teilen von Fotos, die Azure Storage verwendet, um Bilder und andere Daten zu verwalten, die wir im Auftrag unserer Benutzer speichern.</span><span class="sxs-lookup"><span data-stu-id="99c35-101">Recall that we are working on a photo-sharing application that will use Azure Storage to manage pictures and other bits of data we store on behalf of our users.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="99c35-102">::: zone pivot="csharp"</span><span class="sxs-lookup"><span data-stu-id="99c35-102">::: zone pivot="csharp"</span></span>

<span data-ttu-id="99c35-103">Um dieses Szenario zu vereinfachen und uns auf die Storage-APIs konzentrieren zu können, erstellen wir eine neue .NET Core-Konsolenanwendung.</span><span class="sxs-lookup"><span data-stu-id="99c35-103">To simplify our scenario so that we can focus on the Storage APIs, we will create a new .NET Core Console application.</span></span> <span data-ttu-id="99c35-104">Außerdem wird davon ausgegangen, dass diese immer über Netzwerkkonnektivität verfügt.</span><span class="sxs-lookup"><span data-stu-id="99c35-104">We will also assume it always has network connectivity.</span></span> <span data-ttu-id="99c35-105">Sie sollten Ihre App allerdings immer härten, um sicherzustellen, dass Netzwerkausfälle keine Auswirkungen auf die Benutzer haben oder zu Anwendungsfehlern führen.</span><span class="sxs-lookup"><span data-stu-id="99c35-105">However, you should always harden your app to ensure network failures will not impact the user experience or result in a failure of the application itself.</span></span>

## <a name="create-a-net-core-application"></a><span data-ttu-id="99c35-106">Erstellen einer .NET Core-Anwendung</span><span class="sxs-lookup"><span data-stu-id="99c35-106">Create a .NET Core application</span></span>

<span data-ttu-id="99c35-107">.NET Core ist eine plattformübergreifende Version von .NET, die unter macOS, Windows und Linux verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="99c35-107">.NET Core is a cross-platform version of .NET that runs on macOS, Windows, and Linux.</span></span> <span data-ttu-id="99c35-108">Sie können die Tools lokal installieren oder Cloud Shell auf der rechten Seite des Fensters verwenden, um die folgenden Schritte auszuführen.</span><span class="sxs-lookup"><span data-stu-id="99c35-108">You can install the tools locally or use the Cloud Shell on the right side of the window to execute the below steps below.</span></span>

1. <span data-ttu-id="99c35-109">Melden Sie sich bei Cloud Shell an, oder öffnen Sie eine Befehlszeilensitzung, und erstellen Sie eine neue .NET Core-Konsolenanwendung namens „PhotoSharingApp“.</span><span class="sxs-lookup"><span data-stu-id="99c35-109">Sign into the Cloud Shell or open a command-line session and create a new .NET Core Console application with the name "PhotoSharingApp".</span></span> <span data-ttu-id="99c35-110">Sie können das Flag `-o` oder `--output` hinzufügen, um die App in einem bestimmten Ordner zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="99c35-110">You can add the `-o` or `--output` flag to create the app in a specific folder.</span></span>

    ```bash
    dotnet new console --name PhotoSharingApp
    ```

1. <span data-ttu-id="99c35-111">Führen Sie die App aus, um sich zu vergewissern, dass sie ordnungsgemäß erstellt und ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="99c35-111">Run the app to make sure it builds and executes correctly.</span></span> <span data-ttu-id="99c35-112">Es sollte „Hello, World!“</span><span class="sxs-lookup"><span data-stu-id="99c35-112">It should display "Hello World!"</span></span> <span data-ttu-id="99c35-113">in der Konsole angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="99c35-113">to the console.</span></span>

    ```bash
    cd PhotoSharingApp
    
    dotnet run
    ```
<span data-ttu-id="99c35-114">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="99c35-114">::: zone-end</span></span>

<span data-ttu-id="99c35-115">::: zone pivot="javascript"</span><span class="sxs-lookup"><span data-stu-id="99c35-115">::: zone pivot="javascript"</span></span>

<span data-ttu-id="99c35-116">Um dieses Szenario zu vereinfachen und uns auf die Storage-APIs konzentrieren zu können, erstellen wir eine neue Node.js-Anwendung, die über die Konsole ausgeführt werden kann.</span><span class="sxs-lookup"><span data-stu-id="99c35-116">To simplify our scenario so that we can focus on the Storage APIs, we will create a new Node.js application that can run from the console.</span></span> <span data-ttu-id="99c35-117">Außerdem setzen wir voraus, dass sie immer über Netzwerkkonnektivität verfügt.</span><span class="sxs-lookup"><span data-stu-id="99c35-117">We will also assume it always has network connectivity.</span></span> <span data-ttu-id="99c35-118">Sie sollten Ihre App allerdings immer härten, um sicherzustellen, dass Netzwerkausfälle keine Auswirkungen auf die Benutzer haben oder zu Anwendungsfehlern führen.</span><span class="sxs-lookup"><span data-stu-id="99c35-118">However, you should always harden your app to ensure network failures will not impact the user experience, or result in a failure of the application itself.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="99c35-119">Erstellen einer Node.js-Anwendung</span><span class="sxs-lookup"><span data-stu-id="99c35-119">Create a Node.js application</span></span>

<span data-ttu-id="99c35-120">Node.js ist ein beliebtes Framework zum Ausführen von JavaScript-Apps.</span><span class="sxs-lookup"><span data-stu-id="99c35-120">Node.js is a popular framework for running JavaScript apps.</span></span> <span data-ttu-id="99c35-121">Es wird üblicherweise für Web-Apps verwendet, ist aber auch geeignet, um Logik über die Befehlszeile auszuführen.</span><span class="sxs-lookup"><span data-stu-id="99c35-121">It is most commonly used for web apps, but you can use it to run logic from the command line as well.</span></span> <span data-ttu-id="99c35-122">Wenn Sie die Tools lokal installiert haben, können Sie die folgenden Schritte über eine Befehlszeile ausführen.</span><span class="sxs-lookup"><span data-stu-id="99c35-122">If you have the tools installed locally, you can run the following steps from a command line.</span></span> <span data-ttu-id="99c35-123">Alternativ können Sie Cloud Shell auf der rechten Seite des Fensters verwenden, um die folgenden Schritte auszuführen.</span><span class="sxs-lookup"><span data-stu-id="99c35-123">Alternatively, you can use the Cloud Shell on the right side of the window to execute the below steps.</span></span>

1. <span data-ttu-id="99c35-124">Melden Sie sich bei Cloud Shell an, oder öffnen Sie eine Befehlszeilensitzung, und erstellen Sie einen neuen Ordner namens „PhotoSharingApp“.</span><span class="sxs-lookup"><span data-stu-id="99c35-124">Sign into the Cloud Shell or open a command-line session and create a new folder named "PhotoSharingApp".</span></span>

    ```bash
    mkdir PhotoSharingApp
    ```

1. <span data-ttu-id="99c35-125">Wechseln Sie in den neuen Ordner, und verwenden Sie `npm` zum Initialisieren einer neuen Node.js-App.</span><span class="sxs-lookup"><span data-stu-id="99c35-125">Change into the new folder and use `npm` to initialize a new Node.js app.</span></span> <span data-ttu-id="99c35-126">Dadurch wird eine **package.json**-Datei mit Metadaten erstellt, die die App beschreiben.</span><span class="sxs-lookup"><span data-stu-id="99c35-126">This will create a **package.json** file containing metadata that describes the app.</span></span>

    ```bash
    cd PhotoSharingApp
    npm init -y
    ```

1. <span data-ttu-id="99c35-127">Erstellen Sie eine neue Quelldatei namens **index.js** für unseren Code.</span><span class="sxs-lookup"><span data-stu-id="99c35-127">Create a new source file **index.js**, which is where our code will go.</span></span>

    ```bash
    touch index.js
    ```

1. <span data-ttu-id="99c35-128">Öffnen Sie die Datei **index.js** mit einem Editor.</span><span class="sxs-lookup"><span data-stu-id="99c35-128">Open the **index.js** file with an editor.</span></span> <span data-ttu-id="99c35-129">Bei Verwendung von Cloud Shell können Sie `code .` eingeben, um einen Editor zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="99c35-129">If you are using the Cloud Shell, you can type `code .` to open an editor.</span></span>

1. <span data-ttu-id="99c35-130">Fügen Sie das folgende Programm in die Datei **index.js** ein.</span><span class="sxs-lookup"><span data-stu-id="99c35-130">Paste the following program into the **index.js** file.</span></span> <span data-ttu-id="99c35-131">Hierzu können Sie die Tastenkombination **STRG+V** verwenden oder mit der rechten Maustaste klicken und „Einfügen“ auswählen.</span><span class="sxs-lookup"><span data-stu-id="99c35-131">You can use the **Ctrl+V** keyboard shortcut or right-click to paste.</span></span>

    ```javascript
    #!/usr/bin/env node
    
    function main() {
        console.log('Hello, World!');
    }
    
    main();
    ```
1. <span data-ttu-id="99c35-132">Speichern Sie die Datei. (Hierfür können Sie das Menü „...“ rechts oben im Cloud Shell-Editor verwenden.)</span><span class="sxs-lookup"><span data-stu-id="99c35-132">Save the file&mdash;you can use the "..." menu on the top right corner of the Cloud Shell editor.</span></span>

1. <span data-ttu-id="99c35-133">Führen Sie die App aus, um sich zu vergewissern, dass sie ordnungsgemäß ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="99c35-133">Run the app to make sure it executes correctly.</span></span> <span data-ttu-id="99c35-134">Sie sollte „Hello, World!“</span><span class="sxs-lookup"><span data-stu-id="99c35-134">It should display "Hello, World!"</span></span> <span data-ttu-id="99c35-135">in der Konsole anzeigen.</span><span class="sxs-lookup"><span data-stu-id="99c35-135">to the console.</span></span>

    ```bash
    node index.js
    ```

<span data-ttu-id="99c35-136">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="99c35-136">::: zone-end</span></span>