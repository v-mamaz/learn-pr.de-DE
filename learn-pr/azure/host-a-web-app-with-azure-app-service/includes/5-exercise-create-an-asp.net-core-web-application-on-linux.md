<span data-ttu-id="a0e69-101">In dieser Einheit erstellen Sie eine ASP.NET Core-Web-App.</span><span class="sxs-lookup"><span data-stu-id="a0e69-101">In this unit, you will create an ASP.NET Core web app.</span></span>

## <a name="create-a-new-web-project"></a><span data-ttu-id="a0e69-102">Erstellen eines neuen Webprojekts</span><span class="sxs-lookup"><span data-stu-id="a0e69-102">Create a new web project</span></span>

<span data-ttu-id="a0e69-103">Das Herzstück der .NET-CLI-Tools ist das Befehlszeilentool `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="a0e69-103">The heart of the .NET CLI tools is the `dotnet` command line tool.</span></span> <span data-ttu-id="a0e69-104">Mit diesem Befehl erstellen Sie ein neues ASP.NET Core-Webprojekt.</span><span class="sxs-lookup"><span data-stu-id="a0e69-104">Using this command, you will create a new ASP.NET Core web project.</span></span>

<span data-ttu-id="a0e69-105">Erstellen Sie in Cloud Shell auf der rechten Seite eine neue ASP.NET Core-MVC-Anwendung.</span><span class="sxs-lookup"><span data-stu-id="a0e69-105">In the Cloud Shell on the right, create a new ASP.NET Core MVC application.</span></span> <span data-ttu-id="a0e69-106">Nennen Sie sie „BestBikeApp“.</span><span class="sxs-lookup"><span data-stu-id="a0e69-106">Name it "BestBikeApp".</span></span>

```bash
dotnet new mvc --name BestBikeApp
```

<span data-ttu-id="a0e69-107">Der Befehl erstellt einen neuen Ordner namens „BestBikeApp“ für Ihr Projekt.</span><span class="sxs-lookup"><span data-stu-id="a0e69-107">The command will create a new folder named "BestBikeApp" to hold your project.</span></span> <span data-ttu-id="a0e69-108">Führen Sie dort `cd` aus, und führen Sie anschließend die Anwendung aus, um sich zu vergewissern, dass sie vollständig ist.</span><span class="sxs-lookup"><span data-stu-id="a0e69-108">`cd` there, then build and run the application to verify it is complete.</span></span>

```bash
cd BestBikeApp
dotnet run
```

<span data-ttu-id="a0e69-109">Das Ergebnis sollte in etwa wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="a0e69-109">You should get something like:</span></span>

```console
Using launch settings from /home/your-user/Documents/BestBikeApp/Properties/launchSettings.json...
...
Hosting environment: Production
Content root path: /home/your-user/BestBikeApp
Now listening on: http://localhost:5000
Application started.
```

<span data-ttu-id="a0e69-110">Die Ausgabe beschreibt die Situation nach dem Start Ihrer App: Die Anwendung wird ausgeführt und lauscht am Port 5000.</span><span class="sxs-lookup"><span data-stu-id="a0e69-110">The output describes the situation after starting your app: the application is running and listening at port 5000.</span></span>

<span data-ttu-id="a0e69-111">Wenn Sie die App auf Ihrem eigenen Computer ausführen würden, könnten wir über einen Browser auf http://localhost:5000 zugreifen.</span><span class="sxs-lookup"><span data-stu-id="a0e69-111">If were running the app on our own machine we'd be able to open a browser to http://localhost:5000.</span></span> <span data-ttu-id="a0e69-112">Da wir uns in Azure Cloud Shell befinden, müssen wir die App an einem Ort mit einem öffentlichen Endpunkt bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="a0e69-112">Since we're on Azure Cloud Shell, we'll need to deploy the app to somewhere with a public endpoint.</span></span> <span data-ttu-id="a0e69-113">Hierzu können wir die App Service-Instanz verwenden, die wir zuvor erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="a0e69-113">The App Service instance we created earlier is perfect for that.</span></span>