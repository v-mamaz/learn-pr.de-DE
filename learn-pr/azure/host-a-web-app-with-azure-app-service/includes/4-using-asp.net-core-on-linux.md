<span data-ttu-id="0abbb-101">Sie möchten zum Erstellen einer Webanwendung eine Open-Source-Technologie verwenden.</span><span class="sxs-lookup"><span data-stu-id="0abbb-101">You've decided to use an open-source technology for building your web application.</span></span> <span data-ttu-id="0abbb-102">Sie wissen, dass ASP.NET Core ein plattformübergreifendes Open-Source-Framework ist.</span><span class="sxs-lookup"><span data-stu-id="0abbb-102">You know that ASP.NET Core is a cross-platform and open-source framework.</span></span> <span data-ttu-id="0abbb-103">Sie möchten Ihre Web-App in einer Linux-Entwicklungsumgebung mithilfe von ASP.NET Core entwickeln.</span><span class="sxs-lookup"><span data-stu-id="0abbb-103">You decide to develop your web app in a Linux development environment using ASP.NET Core!</span></span>

<span data-ttu-id="0abbb-104">Mit Azure App Service können Sie Ihre bevorzugte Webtechnologie verwenden, einschließlich Node.js, PHP oder .NET Core.</span><span class="sxs-lookup"><span data-stu-id="0abbb-104">Azure App Service allows you to use your favorite web technology, including Node.js, PHP, or .NET Core.</span></span>

<span data-ttu-id="0abbb-105">Hier erfahren Sie, wie Sie eine ASP.NET Core-Anwendung mit der Befehlszeilenschnittstelle (CLI) von .NET erstellen.</span><span class="sxs-lookup"><span data-stu-id="0abbb-105">Here, you will learn to create an ASP.NET Core application using the .NET command-line interface (CLI).</span></span>

## <a name="what-is-aspnet-core"></a><span data-ttu-id="0abbb-106">Was ist ASP.NET Core?</span><span class="sxs-lookup"><span data-stu-id="0abbb-106">What is ASP.NET Core?</span></span>

<span data-ttu-id="0abbb-107">ASP.NET Core ist die neueste Entwicklung des bekannten ASP.NET-Webframeworks von Microsoft, ein plattformübergreifendes Open-Source-Framework zum Erstellen von modernen, cloudbasierten und mit dem Internet verbundenen Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="0abbb-107">ASP.NET Core is the latest evolution of Microsoft's popular ASP.NET web framework, a cross-platform, open-source framework for building modern, cloud-based, and internet-connected applications.</span></span>

<span data-ttu-id="0abbb-108">ASP.NET Core-Anwendungen können für .NET Core Framework oder für das gesamte vorhandene .NET Framework geschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="0abbb-108">ASP.NET Core applications can be written to target the .NET Core Framework or the existing, full .NET Framework.</span></span>

<span data-ttu-id="0abbb-109">Da es sich um ein plattformübergreifendes Open Source-Framework handelt, können Sie ASP.NET Core-Apps auf unterschiedlichen Plattformen erstellen, so auch unter Windows, macOS und Linux.</span><span class="sxs-lookup"><span data-stu-id="0abbb-109">Being a cross-platform and open-source framework, you can build ASP.NET Core apps on a variety of platforms, including Windows, macOS, and Linux.</span></span> <span data-ttu-id="0abbb-110">Die Visual Studio-IDE für Windows- und macOS-Umgebungen wird von Microsoft bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="0abbb-110">Microsoft offers the Visual Studio IDE for both Windows and macOS environments.</span></span> <span data-ttu-id="0abbb-111">Zudem ist der Visual Studio Code-Editor plattformübergreifend und mit diesen Umgebungen sowie mit Linux kompatibel.</span><span class="sxs-lookup"><span data-stu-id="0abbb-111">In addition, the Visual Studio Code editor is cross-platform and compatible with those as well as Linux.</span></span>

><span data-ttu-id="0abbb-112">Um das Erstellen von ASP.NET Core-Anwendungen auf unterschiedlichen Plattformen zu unterstützten, hat Microsoft die .NET Core-CLI-Tools eingeführt. Mit diesen Tools können Sie Ihre Anwendungen mit umfangreichen, konsistenten und plattformübergreifenden APIs erstellen, testen und veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="0abbb-112">To support building ASP.NET Core applications on different platforms, Microsoft introduced the .NET Core CLI tools to help you build, test, and publish your applications using a rich, consistent, and cross-platform set of APIs.</span></span>

<span data-ttu-id="0abbb-113">Mit ASP.NET Core können Sie Web-Apps und -dienste, IoT-Apps sowie mobile Back-Ends.</span><span class="sxs-lookup"><span data-stu-id="0abbb-113">With ASP.NET Core, you can build web apps and services, IoT apps, and mobile back ends.</span></span> <span data-ttu-id="0abbb-114">ASP.NET Core-Anwendungen können entweder in der Cloud oder lokal gehostet werden.</span><span class="sxs-lookup"><span data-stu-id="0abbb-114">ASP.NET Core applications can be hosted either in the cloud or on-premises.</span></span>

<span data-ttu-id="0abbb-115">ASP.NET Core besteht standardmäßig aus einem eingebetteten Webserver und einer Laufzeitumgebung, in der der Anwendungscode ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="0abbb-115">By design, ASP.NET Core consists of an embedded web server and a runtime environment that runs the application code.</span></span> <span data-ttu-id="0abbb-116">Der Anwendungscode wird mithilfe eines überarbeiteten ASP.NET MVC-Frameworks geschrieben, das auf kleinere Module und Pakete zurückgreift.</span><span class="sxs-lookup"><span data-stu-id="0abbb-116">The application code is written using a reworked ASP.NET MVC framework that relies on smaller modules and packages.</span></span> <span data-ttu-id="0abbb-117">Daraus ergibt sich eine kleinere Webanwendungsblaupause, die mühelos über Cloudumgebungen verwaltet und gehostet werden kann.</span><span class="sxs-lookup"><span data-stu-id="0abbb-117">The result is a smaller web application blueprint that is easy to maintain and host over cloud environments.</span></span> <span data-ttu-id="0abbb-118">Die folgende Abbildung zeigt eine in .NET Core gehostete ASP.NET Core-Anwendung und den externen Webserver, der den HTTP-Internetdatenverkehr verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="0abbb-118">The following illustration shows an ASP.NET Core application hosted in .NET Core and the external web server that handles internet http traffic.</span></span>

![Eine Abbildung mit einer ASP.NET Core-Anwendung und der zugehörigen Ausführungsumgebung](../media/4-asp-net-core-architecture.png)

<span data-ttu-id="0abbb-120">ASP.NET Core-Anwendungen sind eigenständige **Konsolenanwendungen**, die über das Treibertool **dotnet** aufgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="0abbb-120">ASP.NET Core applications are standalone **console** applications invoked through the **dotnet** driver tool.</span></span> <span data-ttu-id="0abbb-121">ASP.NET Core-Anwendungen werden nicht in den IIS-Arbeitsprozess, sondern vielmehr über ein natives IIS-Modul mit dem Namen **AspNetCoreModule** geladen, das die externe Konsolenanwendung ausführt.</span><span class="sxs-lookup"><span data-stu-id="0abbb-121">ASP.NET Core applications are not loaded into the IIS worker process, but rather, are loaded through a native IIS module called **AspNetCoreModule** that executes the external console application.</span></span>

## <a name="how-to-create-an-aspnet-core-web-project"></a><span data-ttu-id="0abbb-122">Erstellen eines ASP.NET Core-Webprojekts</span><span class="sxs-lookup"><span data-stu-id="0abbb-122">How to create an ASP.NET Core web project</span></span>

<span data-ttu-id="0abbb-123">Es gibt zwei häufig verwendete Optionen zum Erstellen eines neuen ASP.NET Core-Projekts:</span><span class="sxs-lookup"><span data-stu-id="0abbb-123">There are a two common options for creating a new ASP.NET Core project:</span></span>

- <span data-ttu-id="0abbb-124">Sie können Visual Studio-Vorlagen (Windows- und macOS-Versionen) verwenden, um ein neues Projekt zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="0abbb-124">You can use Visual Studio (Windows and macOS versions) templates to generate a new project.</span></span> <span data-ttu-id="0abbb-125">Visual Studio bietet eine Vielzahl von Vorlagen, die Sie zum Erstellen von Webprojekten verwenden können.</span><span class="sxs-lookup"><span data-stu-id="0abbb-125">Visual Studio offers a variety of templates that you can use to create web projects.</span></span> <span data-ttu-id="0abbb-126">Sie können beispielsweise die Vorlage **Leer** verwenden, um ein reines ASP.NET Core-Projekt mit dem grundlegenden Setup zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="0abbb-126">For instance, you can use the **Empty** template to create a bare-bones ASP.NET Core project with the basic setup.</span></span> <span data-ttu-id="0abbb-127">Darüber hinaus können Sie die Vorlage **Webanwendung (Modal-View-Controller)** verwenden, um eine vollwertige ASP.NET Core MVC-Anwendung mit **Beispielcontrollern** und -**ansichten** zu erstellen, die Sie beim Programmieren der Anwendung unterstützen.</span><span class="sxs-lookup"><span data-stu-id="0abbb-127">In addition, you can use the **Web Application (Modal-View-Controller)** template to generate a full-fledged ASP.NET Core MVC application, with sample **controllers** and **views** that can help you start coding your application.</span></span> <span data-ttu-id="0abbb-128">Der jüngste Neuzugang ist die Projektvorlage **Webanwendung**, die zum Erstellen eines ASP.NET Core-Projekts basierend auf Razor-Seiten und statt auf der herkömmlichen MVC-Projektstruktur verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="0abbb-128">The latest arrival is the **Web Application** project template that is used to create an ASP.NET Core project based on Razor pages and not on the traditional MVC project structure.</span></span>

- <span data-ttu-id="0abbb-129">Sie können die .NET Core-CLI-Tools zum Erstellen eines neuen ASP.NET Core-Projekts verwenden.</span><span class="sxs-lookup"><span data-stu-id="0abbb-129">You can use the .NET Core CLI tools to generate a new ASP.NET Core project.</span></span> <span data-ttu-id="0abbb-130">Microsoft verwaltet eine Reihe von ASP.NET Core-Projektvorlagen für die CLI-Tools, die nahezu identisch mit den Visual Studio-Vorlagen sind.</span><span class="sxs-lookup"><span data-stu-id="0abbb-130">Microsoft maintains a set of ASP.NET Core project templates for the CLI tools that is almost identical to the Visual Studio templates.</span></span> <span data-ttu-id="0abbb-131">Der einzige Unterschied zu den CLI-Tools besteht darin, dass Sie die Befehle zum Erstellen eines neuen ASP.NET Core-Projekts eingeben müssen.</span><span class="sxs-lookup"><span data-stu-id="0abbb-131">The only difference with the CLI tools is that you need to type commands to create a new ASP.NET Core project.</span></span>
> <span data-ttu-id="0abbb-132">Die .NET-CLI-Tools nutzen die **Vorlagen-Engine** zur Unterstützung unterschiedlicher Projektvorlagen.</span><span class="sxs-lookup"><span data-stu-id="0abbb-132">The .NET CLI tools make use of the **templating engine** to support different project templates.</span></span>  <span data-ttu-id="0abbb-133">Weitere Informationen zu der von den .NET-CLI-Tools intern verwendeten [Vorlagen-Engine](https://github.com/dotnet/templating) finden Sie im zugehörigen GitHub-Repository.</span><span class="sxs-lookup"><span data-stu-id="0abbb-133">To learn more, visit the GitHub repository for the [templating engine](https://github.com/dotnet/templating) used internally by the .NET CLI tools.</span></span>

<span data-ttu-id="0abbb-134">Hierbei handelt es sich um die am häufigsten verwendeten Tools zum Erstellen von ASP.NET Core-Projekten.</span><span class="sxs-lookup"><span data-stu-id="0abbb-134">These are the most common tools for creating ASP.NET Core projects.</span></span> <span data-ttu-id="0abbb-135">Es gibt jedoch noch weitere Tools, die Sie suchen und ausprobieren können.</span><span class="sxs-lookup"><span data-stu-id="0abbb-135">However, there are more tools out there that you can search for and explore.</span></span>

<span data-ttu-id="0abbb-136">Die Projekte, die mit anderen Tools erstellt werden, können ein wenig anders sein. Sie alle generieren jedoch gültige und optimierte ASP.NET Core-Projekte.</span><span class="sxs-lookup"><span data-stu-id="0abbb-136">It's worth mentioning that the projects generated by the different tools can be slightly different, however, they all generate valid and optimized ASP.NET Core projects.</span></span>

## <a name="net-cli-tools"></a><span data-ttu-id="0abbb-137">.NET-CLI-Tools</span><span class="sxs-lookup"><span data-stu-id="0abbb-137">.NET CLI tools</span></span>

<span data-ttu-id="0abbb-138">Bei den .NET-CLI-Tools (auch als „NET Core-CLI“ bekannt) handelt es sich um plattformübergreifende Tools, die Befehle zum Erstellen und Wiederherstellen von Paketen und zum Erstellen, Ausführen und Veröffentlichen von .NET-Anwendungen über die Befehlszeile bereitstellen, ohne dass eine IDE mit vollem Funktionsumfang erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="0abbb-138">The .NET CLI tools, also known as .NET Core CLI, is a cross-platform tool that provides commands for creating and restoring packages, and for building, running, and publishing .NET applications from the command line without the need for a full-featured IDE.</span></span>

<span data-ttu-id="0abbb-139">Die .NET-CLI wird als Teil des .NET Core SDK installiert.</span><span class="sxs-lookup"><span data-stu-id="0abbb-139">The .NET CLI is installed as part of the .NET Core SDK.</span></span> <span data-ttu-id="0abbb-140">Auf einem Computer können mehrere Versionen der CLI vorhanden sein und parallel ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="0abbb-140">Multiple versions of the CLI can coexist on the same machine and run side by side.</span></span>

<span data-ttu-id="0abbb-141">Bei der lokalen Entwicklung müssen Sie das relevante .NET Core SDK installieren, um die .NET-CLI verwenden zu können.</span><span class="sxs-lookup"><span data-stu-id="0abbb-141">If you are developing locally, to start using the .NET CLI, you need to install the relevant .NET Core SDK.</span></span> <span data-ttu-id="0abbb-142">In Azure Cloud Shell ist die .NET-CLI bereits installiert.</span><span class="sxs-lookup"><span data-stu-id="0abbb-142">The Azure Cloud Shell already has the .NET CLI installed.</span></span>

<span data-ttu-id="0abbb-143">Öffnen Sie die Befehlszeile, und geben Sie Folgendes ein:</span><span class="sxs-lookup"><span data-stu-id="0abbb-143">Open the command line and type the following:</span></span>

```console
dotnet --version
```

<span data-ttu-id="0abbb-144">Mit diesem Befehl wird die Version der installierten .NET-CLI angezeigt.</span><span class="sxs-lookup"><span data-stu-id="0abbb-144">This command displays the version of the .NET CLI installed.</span></span>

<span data-ttu-id="0abbb-145">Zum Zeitpunkt der Erstellung dieses Dokuments wird Folgendes beim Ausführen des Befehls in Azure Cloud Shell zurückgegeben: `2.0.0`.</span><span class="sxs-lookup"><span data-stu-id="0abbb-145">As of this writing, running the command on Azure Cloud Shell returns: `2.0.0`.</span></span> <span data-ttu-id="0abbb-146">Neuere Versionen stehen zur Verfügung, und möglicherweise ist eine neuere Version bereits auf Ihrem lokalen Computer installiert.</span><span class="sxs-lookup"><span data-stu-id="0abbb-146">There are newer versions available and you may have a newer version on your local machine.</span></span>

<span data-ttu-id="0abbb-147">Sehen Sie sich zunächst einige der häufig verwendeten Befehle der .NET-CLI an.</span><span class="sxs-lookup"><span data-stu-id="0abbb-147">Let us start exploring some of the popular commands of the .NET CLI.</span></span>

<span data-ttu-id="0abbb-148">Der *dotnet*-Befehl weist im Allgemeinen folgende Syntax auf:</span><span class="sxs-lookup"><span data-stu-id="0abbb-148">The *dotnet* command has the following general syntax:</span></span>

```console
dotnet [verb] [arguments]
```

<span data-ttu-id="0abbb-149">Das Verb stellt die auszuführende Aktion dar.</span><span class="sxs-lookup"><span data-stu-id="0abbb-149">The verb represents the action to execute.</span></span> <span data-ttu-id="0abbb-150">Die Argumente stellen die Liste der Eingabeargumente dar, die das Verb für die Ausführung benötigt.</span><span class="sxs-lookup"><span data-stu-id="0abbb-150">The arguments represent the list of input arguments that the verb requires in order to execute.</span></span>

<span data-ttu-id="0abbb-151">Hilfe zur Verwendung von *dotnet* und zur Liste aller verfügbarer *Verben* sowie verwandte Informationen erhalten Sie, indem Sie den folgenden Befehl eingeben:</span><span class="sxs-lookup"><span data-stu-id="0abbb-151">To get help on the *dotnet* usage and list all of the *verbs* available, and other related information, type the following command:</span></span>

```console
dotnet --help
```

<span data-ttu-id="0abbb-152">Mit diesem Befehl wird Folgendes angezeigt:</span><span class="sxs-lookup"><span data-stu-id="0abbb-152">This command displays the following:</span></span>

```console
.NET Command Line Tools (2.1.302)
Usage: dotnet [runtime-options] [path-to-application]
Usage: dotnet [sdk-options] [command] [arguments] [command-options]

path-to-application:
  The path to an application .dll file to execute.

SDK commands:
  new              Initialize .NET projects.
  restore          Restore dependencies specified in the .NET project.
  run              Compiles and immediately executes a .NET project.
  build            Builds a .NET project.
  publish          Publishes a .NET project for deployment (including the runtime).
  test             Runs unit tests using the test runner specified in the project.

...
```

<span data-ttu-id="0abbb-153">Unter den **SDK-Befehlen** wird die gesamte Liste der Befehle angezeigt, die Sie für das .NET Core SDK ausführen können.</span><span class="sxs-lookup"><span data-stu-id="0abbb-153">Under the **SDK commands**, you can see the entire list of commands that you can execute against the .NET Core SDK.</span></span>

<span data-ttu-id="0abbb-154">Folgende Befehle sind die nützlichsten:</span><span class="sxs-lookup"><span data-stu-id="0abbb-154">The most useful commands at all times are the following:</span></span>

- <span data-ttu-id="0abbb-155">**dotnet new**: Dieser Befehl wird verwendet, um für eine neue .NET-Anwendung ein Gerüst zu erstellen bzw. eine neue .NET-Anwendung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="0abbb-155">**dotnet new**: This command is used to scaffold/generate a new .NET application.</span></span>

- <span data-ttu-id="0abbb-156">**dotnet restore**: Dieser Befehl wird verwendet, um alle von der Anwendung referenzierten Pakete wiederherzustellen/herunterzuladen.</span><span class="sxs-lookup"><span data-stu-id="0abbb-156">**dotnet restore**: This command is used to restore/download all packages that are referenced by the application.</span></span>

- <span data-ttu-id="0abbb-157">**dotnet run**: Dieser Befehl wird zum Ausführen der .NET-Anwendung verwendet.</span><span class="sxs-lookup"><span data-stu-id="0abbb-157">**dotnet run**: This command is used to run your .NET application.</span></span>

<span data-ttu-id="0abbb-158">Um Unterstützung zur Verwendung eines bestimmten Befehls zu erhalten, können Sie Folgendes eingeben:</span><span class="sxs-lookup"><span data-stu-id="0abbb-158">Now, to get assistance on how to use a specific command, you can type the following:</span></span>

```console
dotnet new --help
```

<span data-ttu-id="0abbb-159">Dieser Befehl ergibt Folgendes:</span><span class="sxs-lookup"><span data-stu-id="0abbb-159">This command results in:</span></span>

```console
Usage: new [options]

Options:
  -h, --help          Displays help for this command.
  -l, --list          Lists templates containing the specified name. If no name is specified, lists all templates.
  -n, --name          The name for the output being created. If no name is specified, the name of the current directory is used.
  -o, --output        Location to place the generated output.
  -i, --install       Installs a source or a template pack.
  -u, --uninstall     Uninstalls a source or a template pack.
  --nuget-source      Specifies a NuGet source to use during install.
  --type              Filters templates based on available types. Predefined values are "project", "item" or "other".
  --force             Forces content to be generated even if it would change existing files.
  -lang, --language   Filters templates based on language and specifies the language of the template to create.


Templates                                         Short Name         Language          Tags
----------------------------------------------------------------------------------------------------------------------------
Console Application                               console            [C#], F#, VB      Common/Console
Class library                                     classlib           [C#], F#, VB      Common/Library
...

Razor Page                                        page               [C#]              Web/ASP.NET
MVC ViewImports                                   viewimports        [C#]              Web/ASP.NET
MVC ViewStart                                     viewstart          [C#]              Web/ASP.NET
ASP.NET Core Empty                                web                [C#], F#          Web/Empty
ASP.NET Core Web App (Model-View-Controller)      mvc                [C#], F#          Web/MVC
ASP.NET Core Web App                              razor              [C#]              Web/MVC/Razor Pages
ASP.NET Core with Angular                         angular            [C#]              Web/MVC/SPA
...

Solution File                                     sln                                  Solution

Examples:
    dotnet new mvc --auth Individual
    dotnet new webapi
    dotnet new --help
```

<span data-ttu-id="0abbb-160">Mit diesem Befehl werden alle verfügbaren Optionen auflistet, die Sie mit dem `dotnet new`-Befehl verwenden können.</span><span class="sxs-lookup"><span data-stu-id="0abbb-160">This command lists all the available options that you can use with the `dotnet new` command.</span></span> <span data-ttu-id="0abbb-161">Ferner werden alle verfügbaren Projektvorlagen aufgelistet, die Sie zum Erzeugen der nächsten .NET-Anwendung verwenden können.</span><span class="sxs-lookup"><span data-stu-id="0abbb-161">Also, it lists all the available project templates that you can use to generate your next .NET application.</span></span> <span data-ttu-id="0abbb-162">Und schließlich werden in einem Abschnitt Beispiele zur Verwendung des Befehls zum Erzeugen einer neuen .NET-Anwendung angezeigt.</span><span class="sxs-lookup"><span data-stu-id="0abbb-162">Finally, a section shows examples on how to use the command to generate a new .NET application.</span></span>

<span data-ttu-id="0abbb-163">Informationen zu den restlichen Befehlen erhalten Sie, indem Sie das `--help`-Argument für die in der .NET-CLI verfügbaren Befehle verwenden.</span><span class="sxs-lookup"><span data-stu-id="0abbb-163">You can learn the rest of the commands by using the `--help` argument for any command available in the .NET CLI.</span></span>

## <a name="summary"></a><span data-ttu-id="0abbb-164">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="0abbb-164">Summary</span></span>

<span data-ttu-id="0abbb-165">Wenn Sie eine Webanwendung erstellen möchten, haben Sie die Wahl zwischen verschiedenen Sprachen und Frameworks.</span><span class="sxs-lookup"><span data-stu-id="0abbb-165">When deciding to build a web application, you have a choice of many languages and frameworks.</span></span> <span data-ttu-id="0abbb-166">App Service versucht, Ihnen diese Wahl zu erleichtern, denn Sie können unterschiedliche Arten von Anwendungen wie Node.js, PHP oder .NET Core hosten.</span><span class="sxs-lookup"><span data-stu-id="0abbb-166">App Service helps make this choice easier by allowing you to host different types of applications, like Node.js, PHP, or .NET Core.</span></span> <span data-ttu-id="0abbb-167">Dadurch können Sie die Sprachen und Frameworks verwenden, mit denen Sie besonders zufrieden sind, und müssen sich nicht an die Anforderungen Ihres Webhosts anpassen.</span><span class="sxs-lookup"><span data-stu-id="0abbb-167">This allows you to use the languages and frameworks that you're most comfortable with instead of changing to meet the requirements of your web host.</span></span>
