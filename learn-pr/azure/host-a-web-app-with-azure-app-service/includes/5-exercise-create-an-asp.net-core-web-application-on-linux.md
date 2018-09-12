<span data-ttu-id="885dd-101">In dieser Einheit erstellen Sie auf einem Ubuntu-Computer mithilfe der .NET CLI eine ASP.NET Core-Web-App.</span><span class="sxs-lookup"><span data-stu-id="885dd-101">In this unit, you will create an ASP.NET Core web app using the .NET CLI on an Ubuntu machine.</span></span>

## <a name="aspnet-core-installation-on-linux-environment"></a><span data-ttu-id="885dd-102">ASP.NET Core-Installation in einer Linux-Umgebung</span><span class="sxs-lookup"><span data-stu-id="885dd-102">ASP.NET Core installation on Linux environment</span></span>

<span data-ttu-id="885dd-103">Besuchen Sie die [Downloadseite von Microsoft .NET](https://www.microsoft.com/net/download), und führen Sie die Schritte aus, die auf der Seite „.NET Core SDK“ angegeben sind.</span><span class="sxs-lookup"><span data-stu-id="885dd-103">Visit the Microsoft [.NET Downloads page](https://www.microsoft.com/net/download) and follow the same steps mentioned on the .NET Core SDK page.</span></span> <span data-ttu-id="885dd-104">Sie sind nachstehend aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="885dd-104">They are below.</span></span> <span data-ttu-id="885dd-105">Öffnen Sie zum Ausführen der Befehle eine neue Befehlszeileninstanz vom Typ **Terminal**.</span><span class="sxs-lookup"><span data-stu-id="885dd-105">In order to execute the commands, you need to open a new **Terminal** command-line instance.</span></span>

### <a name="register-microsoft-key-and-feed"></a><span data-ttu-id="885dd-106">Registrieren von Microsoft-Schlüssel und Feed</span><span class="sxs-lookup"><span data-stu-id="885dd-106">Register Microsoft key and feed</span></span>

<span data-ttu-id="885dd-107">Vor der Installation von .NET müssen Sie den Microsoft-Schlüssel und das Produktrepository registrieren sowie die erforderlichen Abhängigkeiten installieren.</span><span class="sxs-lookup"><span data-stu-id="885dd-107">Before installing .NET, you'll need to register the Microsoft key, register the product repository, and install the required dependencies.</span></span> <span data-ttu-id="885dd-108">Dieser Schritt muss nur einmal pro Computer ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="885dd-108">This only needs to be done once per machine.</span></span>

```console
~$ wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb
~$ sudo dpkg -i packages-microsoft-prod.deb
```

## <a name="install-the-net-sdk"></a><span data-ttu-id="885dd-109">Installieren des .NET SDK</span><span class="sxs-lookup"><span data-stu-id="885dd-109">Install the .NET SDK</span></span>

<span data-ttu-id="885dd-110">Aktualisieren Sie die Produkte, die zur Installation verfügbar sind, und installieren Sie das .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="885dd-110">Update the products available for installation, then install the .NET SDK.</span></span>

<span data-ttu-id="885dd-111">Führen Sie an der Eingabeaufforderung die folgenden Befehle aus:</span><span class="sxs-lookup"><span data-stu-id="885dd-111">At your command prompt, run the following commands:</span></span>

```console
sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get install dotnet-sdk-2.1
```

<span data-ttu-id="885dd-112">Während der Installation werden Sie ggf. zur Eingabe des Kennworts Ihres Kontos aufgefordert.</span><span class="sxs-lookup"><span data-stu-id="885dd-112">During the installation process, you might be asked to enter your account password.</span></span> <span data-ttu-id="885dd-113">Geben Sie Ihr Kennwort ein, und drücken Sie die EINGABETASTE, um fortzufahren.</span><span class="sxs-lookup"><span data-stu-id="885dd-113">Provide your password and hit Enter to continue.</span></span>

<span data-ttu-id="885dd-114">Geben Sie Folgendes ein, um die Installation zu überprüfen:</span><span class="sxs-lookup"><span data-stu-id="885dd-114">To verify the installation, type the following:</span></span>

```console
dotnet --version
```

<span data-ttu-id="885dd-115">Daraufhin wird folgende Ausgabe angezeigt:</span><span class="sxs-lookup"><span data-stu-id="885dd-115">And the output displayed is:</span></span>

```console
2.1.302
```

<span data-ttu-id="885dd-116">Bei der Installation des .NET Core SDK wurde auch ASP.NET Core installiert.</span><span class="sxs-lookup"><span data-stu-id="885dd-116">Now that you have the .NET Core SDK installed, you also have the ASP.NET Core installed.</span></span> <span data-ttu-id="885dd-117">Sehen wir uns gemeinsam an, wie Sie über die .NET CLI mithilfe der soeben vermittelten Befehle ein neues ASP.NET-Core-Projekt erstellen.</span><span class="sxs-lookup"><span data-stu-id="885dd-117">Let's see together how you can make use of the .NET CLI to create a new ASP.NET Core project using the commands we just learned.</span></span>

## <a name="open-a-terminal-window"></a><span data-ttu-id="885dd-118">Öffnen eines Terminalfensters</span><span class="sxs-lookup"><span data-stu-id="885dd-118">Open a Terminal window</span></span>

<span data-ttu-id="885dd-119">Als Erstes müssen Sie das Terminalfenster öffnen.</span><span class="sxs-lookup"><span data-stu-id="885dd-119">First, you need to open the Terminal window.</span></span> <span data-ttu-id="885dd-120">Das Terminalfenster ermöglicht die Ausführung von Befehlen und hat eine ähnliche Funktion wie das Windows-Fenster „Eingabeaufforderung“.</span><span class="sxs-lookup"><span data-stu-id="885dd-120">The Terminal window allows you to execute commands, and has a similar role to the Windows Command Prompt window.</span></span>

## <a name="create-a-new-web-project"></a><span data-ttu-id="885dd-121">Erstellen eines neuen Webprojekts</span><span class="sxs-lookup"><span data-stu-id="885dd-121">Create a new web project</span></span>

<span data-ttu-id="885dd-122">Das Herzstück der .NET CLI-Tools ist das Treibertool *dotnet*.</span><span class="sxs-lookup"><span data-stu-id="885dd-122">The heart of the .NET CLI tools is the *dotnet* driver tool.</span></span> <span data-ttu-id="885dd-123">Mit diesem Befehl erstellen Sie ein neues ASP.NET Core-Webprojekt.</span><span class="sxs-lookup"><span data-stu-id="885dd-123">Using this command, you will create a new ASP.NET Core web project.</span></span>

<span data-ttu-id="885dd-124">Um eine neue ASP.NET Core MVC-Anwendung zu erstellen, müssen Sie lediglich die folgenden Befehle eingeben:</span><span class="sxs-lookup"><span data-stu-id="885dd-124">To create a new ASP.NET Core MVC application, you only need to type the following commands:</span></span>

```console
cd ~/Documents
mkdir BestBikeApp   # Hit Enter
cd BestBikeApp      # Hit Enter
dotnet new mvc      # Hit Enter
```

<span data-ttu-id="885dd-125">Mit den obigen Befehlen navigieren Sie zum Stammordner *Documents* und erstellen dann einen neuen Ordner.</span><span class="sxs-lookup"><span data-stu-id="885dd-125">The above commands navigate to the *Documents* root folder, and then create a new folder.</span></span> <span data-ttu-id="885dd-126">Danach wird der Ordner geöffnet.</span><span class="sxs-lookup"><span data-stu-id="885dd-126">Then, you go inside that folder.</span></span> <span data-ttu-id="885dd-127">Und schließlich wird der .NET CLI-Befehl ausgeführt, um eine neue ASP.NET MVC-Anwendung mit allen wiederhergestellten Paketen zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="885dd-127">Finally, you issue the .NET CLI command to generate a new ASP.NET MVC application with all the packages restored:</span></span>

```console
The template "ASP.NET Core Web App (Model-View-Controller)" was created successfully.
This template contains technologies from parties other than Microsoft, see https://aka.ms/aspnetcore-template-3pn-210 for details.

Processing post-creation actions...
Running 'dotnet restore' on /home/your-user/Documents/BestBikeApp/BestBikeApp.csproj...
...
```

<span data-ttu-id="885dd-128">Sie müssen jetzt nur noch den folgenden Befehl ausführen, um die Anwendung zu starten:</span><span class="sxs-lookup"><span data-stu-id="885dd-128">All you have to do now is run the application by issuing this command:</span></span>

```console
dotnet run
```

<span data-ttu-id="885dd-129">Im *Terminal* zeigt der Befehl *dotnet* einige nützliche Informationen zur aktiven Anwendung an:</span><span class="sxs-lookup"><span data-stu-id="885dd-129">In the *terminal*, the *dotnet* command displays some useful information for the running app:</span></span>

```console
Using launch settings from /home/your-user/Documents/BestBikeApp/Properties/launchSettings.json...
...
Hosting environment: Development
Content root path: /home/your-user/Documents/BestBikeApp
Now listening on: https://localhost:5001
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

<span data-ttu-id="885dd-130">Die Ausgabe beschreibt die Situation nach dem Start Ihrer Anwendung: Die Anwendung wird ausgeführt und lauscht an den Ports 5001 und 5002 (über HTTPS).</span><span class="sxs-lookup"><span data-stu-id="885dd-130">The output describes the situation after starting your app: the application is running and listening at port 5001 and 5002 (via HTTPS).</span></span>

<span data-ttu-id="885dd-131">Wenn Sie HTTPS lokal auf dem Computer im Entwicklungsmodus ausführen möchten, müssen Sie ein **selbstsigniertes Zertifikat** erstellen und als vertrauenswürdig einstufen.</span><span class="sxs-lookup"><span data-stu-id="885dd-131">In order to run HTTPS locally on the machine in development mode, you need to create and trust a **self-signed certificate**.</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="885dd-132">Erstellen eines selbstsignierten Zertifikats</span><span class="sxs-lookup"><span data-stu-id="885dd-132">Create a self-signed certificate</span></span>

<span data-ttu-id="885dd-133">Führen Sie den folgenden Befehl aus, um ein selbstsigniertes Entwicklungszertifikat zu generieren:</span><span class="sxs-lookup"><span data-stu-id="885dd-133">Run the command below to generate a development self-signed certificate:</span></span>

```console
dotnet dev-certs https -v
```

<span data-ttu-id="885dd-134">Nach der Befehlsausführung wird Folgendes zurückgegeben:</span><span class="sxs-lookup"><span data-stu-id="885dd-134">Running the command returns the following:</span></span>

```console
The HTTPS developer certificate was generated successfully.
```

## <a name="run-the-application"></a><span data-ttu-id="885dd-135">Ausführen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="885dd-135">Run the application</span></span>

<span data-ttu-id="885dd-136">Für diese Demonstration verwenden wir den Browser Firefox.</span><span class="sxs-lookup"><span data-stu-id="885dd-136">For this demonstration, we are using the Firefox browser.</span></span>

<span data-ttu-id="885dd-137">Öffnen Sie den Browser, und geben Sie die Adresse `http://localhost:5001` ein, um sich zu vergewissern, dass die Anwendung erfolgreich ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="885dd-137">Open the browser and type in the address `http://localhost:5001` to verify the application is running successfully.</span></span>

![Screenshot einer Webbrowseransicht der Standardwebseite der ASP.NET Core-MVC-Vorlage](../media/5-asp-core-mvc-default-template.PNG)

> [!NOTE]
> <span data-ttu-id="885dd-139">Da das selbstsignierte Zertifikat für die Entwicklung von Firefox nicht verifiziert werden konnte, müssen Sie für die URL der Anwendung **eine Ausnahme hinzufügen**.</span><span class="sxs-lookup"><span data-stu-id="885dd-139">You need to **add an exception** for the application's URL because the development self-signed certificate couldn't be verified by Firefox.</span></span>
