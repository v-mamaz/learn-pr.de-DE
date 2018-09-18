<span data-ttu-id="aa7e9-101">Sie haben erfolgreich Ihre Web-App erstellt und in Azure veröffentlicht. Doch was geschieht, wenn Sie Änderungen vornehmen möchten?</span><span class="sxs-lookup"><span data-stu-id="aa7e9-101">You've successfully created your web app and published it to Azure, but what happens when you want to make changes?</span></span> <span data-ttu-id="aa7e9-102">Visual Studio merkt sich den Speicherort, in dem die App veröffentlicht ist. So können Sie Ihre App in zwei Klicks aktualisieren und ändern.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-102">Visual Studio will remember where the app is published, which makes updating and changing your app a two-click process.</span></span>

## <a name="explore-the-project-structure"></a><span data-ttu-id="aa7e9-103">Erkunden der Projektstruktur</span><span class="sxs-lookup"><span data-stu-id="aa7e9-103">Explore the project structure</span></span>

<span data-ttu-id="aa7e9-104">Sie haben eine ASP.NET-Web-App in Visual Studio erstellt und müssen nun Ihre Website bearbeiten und anpassen.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-104">We've created an ASP.NET web app in Visual Studio, and now you will need to edit and customize your website.</span></span> <span data-ttu-id="aa7e9-105">Sehen Sie sich die Projektstruktur und die von Visual Studio erstellten Elemente an.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-105">Let's explore the project structure to see what Visual Studio has created for us.</span></span>

### <a name="dependencies"></a><span data-ttu-id="aa7e9-106">Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="aa7e9-106">Dependencies</span></span>

<span data-ttu-id="aa7e9-107">Zu Abhängigkeiten zählen die ASP.NET-Informationen, um Ihre App für die Verwendung einzurichten.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-107">Dependencies include the ASP.NET internals to get your app up and running.</span></span> <span data-ttu-id="aa7e9-108">Diesen Ordner werden Sie nicht so häufig verwenden, es sei denn, Sie fügen spezielle Pakete von Drittanbietern hinzu.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-108">Unless you are adding specific third-party packages, you won't need to spend much time in this folder.</span></span>

### <a name="properties"></a><span data-ttu-id="aa7e9-109">Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="aa7e9-109">Properties</span></span>

<span data-ttu-id="aa7e9-110">Der Ordner „Eigenschaften“ enthält die Konfigurationsdaten für den Speicherort, in dem Sie Ihre Web-App hosten.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-110">The properties folder contains configuration data for where you are hosting your web app.</span></span> <span data-ttu-id="aa7e9-111">Wenn Sie nun den Ordner **PublishProfiles** erweitern, sollten Sie die URL der Alpine Ski Hill-Website sehen.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-111">If you expand the **PublishProfiles** folder now, you should see the URL for the Alpine Ski Hill site.</span></span> <span data-ttu-id="aa7e9-112">Veröffentlichungsprofile bestehen aus einer XML-Datei, die Konfigurationsinformationen zur Veröffentlichung enthält (z.B. die Azure-Adresse), anhand derer Visual Studio Ihre Dateien hochlädt.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-112">Each publishing profile is an .xml file containing publishing configuration information such as the Azure address that Visual Studio uses to upload your files.</span></span>

### <a name="wwwroot"></a><span data-ttu-id="aa7e9-113">wwwroot</span><span class="sxs-lookup"><span data-stu-id="aa7e9-113">wwwroot</span></span>

<span data-ttu-id="aa7e9-114">Die Datei „wwwroot“ enthält alle statischen Ressourcen für Ihre Website, z.B. die CSS-, JS-, Bild- und LIB-Dateien.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-114">The wwwroot file contains all of your static assets for your site, such as the .css, .js, images, and .lib files.</span></span> <span data-ttu-id="aa7e9-115">Diese benötigen Sie, wenn Sie Formatierungsarbeiten vornehmen und weitere Funktionen zu Ihrer Website hinzufügen möchten.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-115">When you are ready to style and add more functionality to your site, you will work in here.</span></span>

### <a name="pages"></a><span data-ttu-id="aa7e9-116">Seiten</span><span class="sxs-lookup"><span data-stu-id="aa7e9-116">Pages</span></span>

<span data-ttu-id="aa7e9-117">Der Ordner **Seiten** enthält _**Razor**_-Vorlagen für die Seiten Ihrer Website.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-117">The **Pages** folder includes _**Razor**_ templates for the pages of your site.</span></span>
<span data-ttu-id="aa7e9-118">Razor ist eine auf HTML basierende Syntax, die spezielle Konventionen für die Anzeige von Daten und Ausführung von Logik auf Ihrer Website aufweist.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-118">Razor is a syntax that is built up around HTML, which has special conventions for displaying data and executing logic on your site.</span></span>

<span data-ttu-id="aa7e9-119">Jede Seite auf Ihrer Website wird durch zwei Codedateien dargestellt:</span><span class="sxs-lookup"><span data-stu-id="aa7e9-119">Each page in your site is represented with two code files:</span></span>

- <span data-ttu-id="aa7e9-120">Bei der ersten Datei handelt es sich um eine `.cshtml`-Datei, die Razor-Markupdatei.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-120">The first is a `.cshtml` file, which is the Razor markup file.</span></span> <span data-ttu-id="aa7e9-121">Diese Datei enthält Ihren HTML-Code für die Anzeige und einen gewissen Umfang an C#-Logik.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-121">This file includes your display HTML and some C# logic.</span></span>

- <span data-ttu-id="aa7e9-122">Bei der zweiten Datei handelt es sich um eine `.cs`-Datei, die das C#-CodeBehind mit der `PageModel`-Klasse enthält.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-122">The second file is a `.cs` file, which is the C# code-behind that includes `PageModel` class.</span></span> <span data-ttu-id="aa7e9-123">Mit dieser Datei können Sie HTTP-Anforderungen abfangen und einige Verarbeitungsaufgaben für diese Anforderungen durchführen, bevor Sie Daten an die Razor-Datei übergeben.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-123">This file allows you to intercept HTTP requests and do some processing on that request before passing off any data to the Razor file.</span></span>

### <a name="appsettingjson"></a><span data-ttu-id="aa7e9-124">appsetting.json</span><span class="sxs-lookup"><span data-stu-id="aa7e9-124">appsetting.json</span></span>

<span data-ttu-id="aa7e9-125">Dies ist eine Konfigurationsdatei für ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-125">This is a configuration file for ASP.NET.</span></span>

### <a name="bundleconfigjson"></a><span data-ttu-id="aa7e9-126">bundleconfig.json</span><span class="sxs-lookup"><span data-stu-id="aa7e9-126">bundleconfig.json</span></span>

<span data-ttu-id="aa7e9-127">„bundleconfig.json“ ist eine Konfigurationsdatei für die Vorverarbeitung.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-127">The bundleconfig.json is preprocessing configuration.</span></span> <span data-ttu-id="aa7e9-128">Diese Datei sorgt dafür, dass Ihre CSS- und JS-Dateien bei der Veröffentlichung komprimiert werden.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-128">This file is making your .css and .js files smaller when they are published.</span></span>

### <a name="programcs-and-startupcs"></a><span data-ttu-id="aa7e9-129">„Program.cs“ und „Startup.cs“</span><span class="sxs-lookup"><span data-stu-id="aa7e9-129">Program.cs and Startup.cs</span></span>

<span data-ttu-id="aa7e9-130">„Program.cs“ und „Startup.cs“ konfigurieren und starten Ihren Webhost für Ihre Website.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-130">Program.cs and Startup.cs configure and launch your web host for your site.</span></span>

## <a name="updating-your-website-using-razor"></a><span data-ttu-id="aa7e9-131">Aktualisieren einer Website mithilfe von Razor</span><span class="sxs-lookup"><span data-stu-id="aa7e9-131">Updating your website using Razor</span></span>

<span data-ttu-id="aa7e9-132">Im Folgenden werden einige grundlegende Änderungen an unserer Website vorgenommen.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-132">We will want to make some basic changes to our website.</span></span> <span data-ttu-id="aa7e9-133">Hierfür benötigen Sie ein grundlegendes Verständnis bezüglich der Nutzung der Razor-Vorlagen zum Anpassen Ihrer Web-App.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-133">In order to do this, you will need to have a basic understanding of how to leverage the Razor templates to customize your web app.</span></span>

## <a name="what-is-razor"></a><span data-ttu-id="aa7e9-134">Was ist Razor?</span><span class="sxs-lookup"><span data-stu-id="aa7e9-134">What is Razor?</span></span>

<span data-ttu-id="aa7e9-135">Razor ist eine ASP.NET-Syntax zum Erstellen dynamischer Webseiten mit C#.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-135">Razor is an ASP.NET syntax used to create dynamic web pages with C#.</span></span> <span data-ttu-id="aa7e9-136">Wenn ein Server eine Razor-Seite liest, wird der C#-Code ausgeführt, bevor er die HTML-Seite rendert.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-136">When a server reads a Razor page, the C# code is run before it renders the HTML.</span></span> <span data-ttu-id="aa7e9-137">So können Sie schnell dynamische Inhalte generieren.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-137">This allows you to generate dynamic content quickly.</span></span>

<span data-ttu-id="aa7e9-138">Razor verwendet `@`-Anweisungen für die Verarbeitung einer Seite mit ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-138">Razor uses `@` directives to tell ASP.NET how to process a page.</span></span>

<span data-ttu-id="aa7e9-139">Sehen Sie sich beispielsweise den Code auf der Seite `Contact.cshtml` an:</span><span class="sxs-lookup"><span data-stu-id="aa7e9-139">For example, take a look at the code in the `Contact.cshtml` page:</span></span>

```aspx-csharp
@page
@model ContactModel
@{
    ViewData["Title"] = "Contact";
}
<h2>@ViewData["Title"]</h2>
<h3>@Model.Message</h3>
...
```

- <span data-ttu-id="aa7e9-140">Die `@page`-Anweisung weist ASP.NET an, diese Datei als Razor-Seite zu verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-140">The `@page` directive is telling ASP.NET to process this file as a Razor page.</span></span>
- <span data-ttu-id="aa7e9-141">Die `@model`-Anweisung weist ASP.NET an, diese Razor-Seite mit einer C#-Klasse namens `ContactModel` zu verknüpfen.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-141">The `@model` directive is telling ASP.NET to tie this Razor page with a C# class called `ContactModel`.</span></span>

<span data-ttu-id="aa7e9-142">Darüber hinaus verwendet Razor das `@`-Symbol für den Übergang zwischen Code und HTML.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-142">Razor also uses the `@` symbol to transition between code and HTML.</span></span> <span data-ttu-id="aa7e9-143">Wenn Sie sich den obigen Codeausschnitt ansehen, wird Ihnen `@{ ... }` auffallen.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-143">If you look at the snippet above, you'll notice `@{ ... }`.</span></span> <span data-ttu-id="aa7e9-144">Hierbei handelt es sich um einen **Razor-Codeblock**.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-144">This is a **Razor code block**.</span></span> <span data-ttu-id="aa7e9-145">Dieser Code wird _ausgeführt, aber nicht gerendert_.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-145">It's code which is _executed but not rendered_.</span></span>

<span data-ttu-id="aa7e9-146">Um die Ausgabe einer Codeanweisung zu rendern, wird `@` vor einem C#-Ausdruck verwendet.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-146">To render the output of a code statement, we use the `@` in front of a C# expression.</span></span> <span data-ttu-id="aa7e9-147">Hierzu sehen Sie weiter oben in den Tags `<h2>` und `<h3>` zwei Beispiele im Codeblock.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-147">We have two examples of that in the code block above in the `<h2>` and `<h3>` tags.</span></span>

## <a name="publish-your-updates"></a><span data-ttu-id="aa7e9-148">Veröffentlichen Ihrer Aktualisierungen</span><span class="sxs-lookup"><span data-stu-id="aa7e9-148">Publish your updates</span></span>

<span data-ttu-id="aa7e9-149">Nachdem Sie die Änderungen an Ihrer Website vorgenommen haben, sollten Sie sie in Azure veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-149">Once you've made the changes to your website, you will want to publish them to Azure.</span></span> <span data-ttu-id="aa7e9-150">Dieser Prozess ist mit dem der ursprünglichen Veröffentlichung vergleichbar.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-150">This process is similar to how we initially published.</span></span>

1. <span data-ttu-id="aa7e9-151">Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Projekt.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-151">Right-click the project in Solution Explorer.</span></span>

1. <span data-ttu-id="aa7e9-152">Der Name Ihrer Website gefolgt von „Web Deploy“ sollte nun angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-152">Now you should see the name of your website followed by Web Deploy.</span></span> <span data-ttu-id="aa7e9-153">Wenn Sie Ihre Website „AlpineSkiHouse42“ genannt haben, würde unter den verfügbaren Optionen **AlpineSkiHouse42 – Web Deploy** angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-153">If you had named your website AlpineSkiHouse42, you would see **AlpineSkiHouse42 - Web Deploy** in the available options.</span></span> <span data-ttu-id="aa7e9-154">Wählen Sie diese Option aus. Ihre Website wird dann in Azure aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-154">Select that and your site will update in Azure.</span></span>

## <a name="summary"></a><span data-ttu-id="aa7e9-155">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="aa7e9-155">Summary</span></span>

<span data-ttu-id="aa7e9-156">Die Erstellung und Veröffentlichung einer Website stellen lediglich die ersten Schritte bei der Erstellung einer guten Website dar.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-156">Creating and publishing a website are just the first steps in creating a good website.</span></span> <span data-ttu-id="aa7e9-157">Fügen Sie Inhalte hinzu, müssen Sie Ihre Website aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-157">Once you start to add content, you'll need to update your site.</span></span> <span data-ttu-id="aa7e9-158">Nachdem Sie Ihre Website zunächst in Azure veröffentlicht haben, können Sie sie jederzeit über den Projektmappen-Explorer aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="aa7e9-158">Once you've initially published your site to Azure, you can update at any time from the Solution Explorer.</span></span>
