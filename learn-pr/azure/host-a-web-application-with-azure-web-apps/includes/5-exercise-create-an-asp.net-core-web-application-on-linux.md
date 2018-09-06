<span data-ttu-id="54909-101">In dieser Übung erstellen Sie auf einem Ubuntu-Computer mithilfe der .NET CLI eine ASP.NET Core-Web-App.</span><span class="sxs-lookup"><span data-stu-id="54909-101">In this exercise, you will create an ASP.NET Core web app using the .NET CLI on an Ubuntu machine.</span></span>

## <a name="aspnet-core-installation-on-linux-environment"></a><span data-ttu-id="54909-102">ASP.NET Core-Installation in einer Linux-Umgebung</span><span class="sxs-lookup"><span data-stu-id="54909-102">ASP.NET Core installation on Linux environment</span></span>

<span data-ttu-id="54909-103">Besuchen Sie die [Downloadseite von .NET ](https://www.microsoft.com/net/download) von Microsoft und führen Sie die Schritte aus, die auf der Seite „.NET Core SDK“ angegeben sind.</span><span class="sxs-lookup"><span data-stu-id="54909-103">Visit the Microsoft [.NET Downloads page](https://www.microsoft.com/net/download) and follow the same steps mentioned on the .NET Core SDK page.</span></span> <span data-ttu-id="54909-104">Sie sind nachstehend geführt.</span><span class="sxs-lookup"><span data-stu-id="54909-104">They are below.</span></span> <span data-ttu-id="54909-105">Um die Befehle ausführen zu können, müssen Sie eine neue **Terminal**instanz öffnen, ähnlich wie in diesem Beispiel:</span><span class="sxs-lookup"><span data-stu-id="54909-105">In order to execute the commands, you need to open a new **Terminal** instance, something similar to this:</span></span>

![Terminalistanz](../media-draft/5-terminal-instance.PNG)

### <a name="register-microsoft-key-and-feed"></a><span data-ttu-id="54909-107">Registrieren von Microsoft-Schlüssel und Feed</span><span class="sxs-lookup"><span data-stu-id="54909-107">Register Microsoft key and feed</span></span>

<span data-ttu-id="54909-108">Vor der Installation von .NET müssen Sie den Microsoft-Schlüssel und das Produktrepository registrieren sowie die erforderlichen Abhängigkeiten installieren.</span><span class="sxs-lookup"><span data-stu-id="54909-108">Before installing .NET, you'll need to register the Microsoft key, register the product repository, and install the required dependencies.</span></span> <span data-ttu-id="54909-109">Dies muss nur pro Computer nur einmal erfolgen.</span><span class="sxs-lookup"><span data-stu-id="54909-109">This only needs to be done once per machine.</span></span>

```console
~$ wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb
~$ sudo dpkg -i packages-microsoft-prod.deb
```

## <a name="install-the-net-sdk"></a><span data-ttu-id="54909-110">Installieren des .NET SDK</span><span class="sxs-lookup"><span data-stu-id="54909-110">Install the .NET SDK</span></span>

<span data-ttu-id="54909-111">Aktualisieren Sie die Produkte, die zur Installation verfügbar sind, und installieren Sie das .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="54909-111">Update the products available for installation, then install the .NET SDK.</span></span>

<span data-ttu-id="54909-112">Führen Sie an der Eingabeaufforderung die folgenden Befehle aus:</span><span class="sxs-lookup"><span data-stu-id="54909-112">At your command prompt, run the following commands:</span></span>

```console
sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get install dotnet-sdk-2.1
```

<span data-ttu-id="54909-113">Während der Installation werden Sie ggf. zur Eingabe des Kennworts Ihres Kontos aufgefordert.</span><span class="sxs-lookup"><span data-stu-id="54909-113">During the installation process, you might be asked to enter your account password.</span></span> <span data-ttu-id="54909-114">Geben Sie Ihr Kennwort ein, und drücken Sie die EINGABETASTE, um fortzufahren.</span><span class="sxs-lookup"><span data-stu-id="54909-114">Simply provide your password and hit Enter to continue.</span></span>

<span data-ttu-id="54909-115">Führen Sie den folgenden Befehl aus, um die Installation zu überprüfen:</span><span class="sxs-lookup"><span data-stu-id="54909-115">To verify the installation, type the following:</span></span>

```console
dotnet --version
```

<span data-ttu-id="54909-116">Die angezeigte Ausgabe sieht so aus:</span><span class="sxs-lookup"><span data-stu-id="54909-116">And the output displayed is:</span></span>

```console
2.1.302
```

<span data-ttu-id="54909-117">Bei der Installation des .NET Core SDK wurde auch ASP.NET Core installiert.</span><span class="sxs-lookup"><span data-stu-id="54909-117">Now that you have the .NET Core SDK installed, you also have the ASP.NET Core installed.</span></span> <span data-ttu-id="54909-118">Lassen Sie uns gemeinsam anschauen, wie Sie mithilfe der .NET CLI ein neues ASP.NET-Core-Projekt mit den zuvor erlernten Befehlen erstellen können.</span><span class="sxs-lookup"><span data-stu-id="54909-118">Let's see together how you can make use of the .NET CLI to create a new ASP.NET Core project using the commands we just learned.</span></span>

## <a name="open-a-terminal-window"></a><span data-ttu-id="54909-119">Öffnen eines Terminalfensters</span><span class="sxs-lookup"><span data-stu-id="54909-119">Open a Terminal window</span></span>

<span data-ttu-id="54909-120">Zuerst müssen Sie das Terminalfenster ausfindig machen und öffnen.</span><span class="sxs-lookup"><span data-stu-id="54909-120">First, you need to locate and open the Terminal window.</span></span> <span data-ttu-id="54909-121">Das Terminalfenster ermöglicht die Ausführung von Befehlen und spielt eine ähnliche Rolle wie das Windows-Fenster „Eingabeaufforderung“.</span><span class="sxs-lookup"><span data-stu-id="54909-121">The Terminal window allows you to execute commands, and has a similar role to the Windows Command Prompt window.</span></span>

## <a name="create-a-new-web-project"></a><span data-ttu-id="54909-122">Erstellen eines neuen Webprojekts</span><span class="sxs-lookup"><span data-stu-id="54909-122">Create a new web project</span></span>

<span data-ttu-id="54909-123">Das Herzstück der .NET CLI-Tools ist das Treibertool *dotnet*.</span><span class="sxs-lookup"><span data-stu-id="54909-123">The heart of the .NET CLI tools is the *dotnet* driver tool.</span></span> <span data-ttu-id="54909-124">Mit diesem Befehl erstellen Sie ein neues ASP.NET Core-Webprojekt.</span><span class="sxs-lookup"><span data-stu-id="54909-124">Using this command, you will create a new ASP.NET Core web project.</span></span>

<span data-ttu-id="54909-125">Um eine neue ASP.NET Core MVC-Anwendung zu erstellen, müssen Sie lediglich die folgenden Befehle eingeben:</span><span class="sxs-lookup"><span data-stu-id="54909-125">To create a new ASP.NET Core MVC application, you only need to type the following commands:</span></span>

```console
cd ~/Documents
mkdir BestBikeApp   # Hit Enter
cd BestBikeApp      # Hit Enter
dotnet new mvc      # Hit Enter
```

<span data-ttu-id="54909-126">Mit den obigen Befehlen navigieren Sie zum Stammordner *Documents* und erstellen dann ein neues Verzeichnis bzw. einen neuen Ordner.</span><span class="sxs-lookup"><span data-stu-id="54909-126">The above commands navigate to the *Documents* root folder, and then create a new directory / folder.</span></span> <span data-ttu-id="54909-127">Anschließend wechseln Sie in dieses Verzeichnis bzw. diesen Ordner und geben den .NET CLI-Befehl ein, um eine neue ASP.NET MVC-Anwendung mit allen wiederhergestellten Paketen zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="54909-127">Then, you go inside that directory/folder, and finally, you issue the .NET CLI command to generate a new ASP.NET MVC application with all the packages restored:</span></span>

```console
The template "ASP.NET Core Web App (Model-View-Controller)" was created successfully.
This template contains technologies from parties other than Microsoft, see https://aka.ms/aspnetcore-template-3pn-210 for details.

Processing post-creation actions...
Running 'dotnet restore' on /home/your-user/Documents/BestBikeApp/BestBikeApp.csproj...
...
```

<span data-ttu-id="54909-128">Sie müssen jetzt nur noch die Anwendung durch Ausführen dieses Befehls starten:</span><span class="sxs-lookup"><span data-stu-id="54909-128">All you have to do now is run the application by issuing this command:</span></span>

```console
dotnet run
```

<span data-ttu-id="54909-129">Im *Terminal* zeigt der Befehl *dotnet* einige nützliche Informationen zur aktiven Anwendung an:</span><span class="sxs-lookup"><span data-stu-id="54909-129">In the *terminal*, the *dotnet* command displays some useful information for the running app:</span></span>

```console
Using launch settings from /home/your-user/Documents/BestBikeApp/Properties/launchSettings.json...
...
Hosting environment: Development
Content root path: /home/your-user/Documents/BestBikeApp
Now listening on: https://localhost:5001
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

<span data-ttu-id="54909-130">Die Ausgabe beschreibt die Situation nach dem Start Ihrer Anwendung: Die Anwendung wird ausgeführt und lauscht an den Ports 5001 und 5002 (über HTTPS).</span><span class="sxs-lookup"><span data-stu-id="54909-130">The output describes the situation after starting your app: the application is running and listening at port 5001 and 5002 (via HTTPS).</span></span>

<span data-ttu-id="54909-131">Um HTTPS lokal auf dem Computer im Entwicklungsmodus ausführen zu können, müssen Sie ein selbstsigniertes vertrauenswürdiges **Zertifikat** erstellen.</span><span class="sxs-lookup"><span data-stu-id="54909-131">In order to run HTTPS locally on the machine in development mode, you need to create and trust a **self-signed certificate**.</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="54909-132">Erstellen eines selbstsignierten Zertifikats</span><span class="sxs-lookup"><span data-stu-id="54909-132">Create a self-signed certificate</span></span>

<span data-ttu-id="54909-133">Führen Sie den folgenden Befehl aus, um ein selbstsigniertes Zertifikat für die Entwicklung zu generieren:</span><span class="sxs-lookup"><span data-stu-id="54909-133">Run the command below to generate a development self-signed certificate:</span></span>

```console
dotnet dev-certs https -v
```

<span data-ttu-id="54909-134">Bei Ausführen des Befehls wird Folgendes zurückgegeben:</span><span class="sxs-lookup"><span data-stu-id="54909-134">Running the command returns the following:</span></span>

```console
The HTTPS developer certificate was generated successfully.
```

## <a name="run-the-application"></a><span data-ttu-id="54909-135">Ausführen der Anwendung</span><span class="sxs-lookup"><span data-stu-id="54909-135">Run the application</span></span>

<span data-ttu-id="54909-136">Für diese Demonstration verwende ich den Browser Firefox.</span><span class="sxs-lookup"><span data-stu-id="54909-136">For this demonstration, I am using the Firefox browser.</span></span>

<span data-ttu-id="54909-137">Öffnen Sie den Browser, und geben die Adresse `http://localhost:5001` ein, um die Anwendung aufzurufen.</span><span class="sxs-lookup"><span data-stu-id="54909-137">Open the browser and type in the address `http://localhost:5001` to go to the application.</span></span>

![ASP.NET Core MVC-Standardvorlage](../media-draft/5-asp-core-mvc-default-template.PNG)

> <span data-ttu-id="54909-139">Sie müssen für die URL der Anwendung **eine Ausnahme hinzufügen**, da das selbstsignierte Zertifikat für die Entwicklung von Firefox nicht verifiziert werden konnte.</span><span class="sxs-lookup"><span data-stu-id="54909-139">You need to **add an exception** for the application's URL because the development self-signed certificate couldn't be verified by Firefox.</span></span>

<span data-ttu-id="54909-140">Die Web-App ist betriebsbereit und wird erfolgreich ausgeführt!</span><span class="sxs-lookup"><span data-stu-id="54909-140">The web app is up and running successfully!</span></span>
