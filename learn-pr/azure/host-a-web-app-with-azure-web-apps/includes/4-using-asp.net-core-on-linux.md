<span data-ttu-id="2e4b6-101">Sie möchten zum Erstellen einer Webanwendung eine Open-Source-Technologie verwenden.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-101">You've decided to use an open-source technology for building your web application.</span></span> <span data-ttu-id="2e4b6-102">Sie wissen, dass ASP.NET Core ein plattformübergreifendes Open-Source-Framework ist.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-102">You know that ASP.NET Core is a cross-platform and open-source framework.</span></span> <span data-ttu-id="2e4b6-103">Sie möchten Ihre Web-App in einer Linux-Umgebung mithilfe von ASP.NET Core entwickeln.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-103">You decide to develop your web app in a Linux environment using ASP.NET Core!</span></span>

<span data-ttu-id="2e4b6-104">Dank Web-Apps in Azure können Sie die von Ihnen bevorzugte Webtechnologie verwenden.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-104">Web Apps in Azure allows you to use your favorite web technology.</span></span> <span data-ttu-id="2e4b6-105">Web-Apps ist das Richtige für Sie, ganz gleich, ob Sie mit Node.js, PHP oder .NET Core besonders zufrieden sind.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-105">Whether you're most comfortable with Node.js, PHP, or .NET Core, Web Apps will work for you.</span></span>

<span data-ttu-id="2e4b6-106">Hier erstellen Sie eine ASP.NET Core-Anwendung mithilfe der .NET-Befehlszeilenschnittstelle.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-106">Here, you will create an ASP.NET Core application using the .NET command-line interface (CLI).</span></span>

## <a name="what-is-aspnet-core"></a><span data-ttu-id="2e4b6-107">Was ist ASP.NET Core?</span><span class="sxs-lookup"><span data-stu-id="2e4b6-107">What is ASP.NET Core?</span></span>

<span data-ttu-id="2e4b6-108">ASP.NET Core ist die neueste Entwicklung des bekannten ASP.NET-Webframeworks von Microsoft, ein plattformübergreifendes Open-Source-Framework zum Erstellen von modernen, cloudbasierten und mit dem Internet verbundenen Anwendungen.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-108">ASP.NET Core is the latest evolution of Microsoft's popular ASP.NET web framework, a cross-platform, open-source framework for building modern, cloud-based, and internet-connected applications.</span></span>

<span data-ttu-id="2e4b6-109">ASP.NET Core-Anwendungen können für .NET Core Framework oder für das gesamte vorhandene .NET Framework geschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-109">ASP.NET Core applications can be written to target the .NET Core Framework or the existing, full .NET Framework.</span></span>

<span data-ttu-id="2e4b6-110">Da es sich um ein plattformübergreifendes Open-Source-Framework handelt, können Sie ASP.NET Core-Apps auf unterschiedlichen Plattformen erstellen, so auch unter Windows, macOS und Linux.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-110">Being a cross-platform and open-source framework, you can build ASP.NET Core apps on a variety of platforms, including Windows, macOS, and Linux.</span></span> <span data-ttu-id="2e4b6-111">Bislang stellt Microsoft die Visual Studio-IDE für Windows- und für macOS-Umgebungen bereit.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-111">Thus far, Microsoft offers the Visual Studio IDE for both Windows and macOS environments.</span></span> <span data-ttu-id="2e4b6-112">Zudem ist der Visual Studio Code-Editor plattformübergreifend und mit diesen Umgebungen kompatibel.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-112">In addition, the Visual Studio Code editor is cross-platform and compatible with them.</span></span>

><span data-ttu-id="2e4b6-113">Um das Erstellen von ASP.NET Core-Anwendungen auf unterschiedlichen Plattformen zu unterstützten, hat Microsoft die .NET Core-CLI-Tools eingeführt. Mit diesen Tools können Sie Ihre Anwendungen mit umfangreichen, konsistenten und plattformübergreifenden APIs erstellen, testen und veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-113">To support building ASP.NET Core applications on different platforms, Microsoft introduced the .NET Core CLI tools to help you build, test, and publish your applications using a rich, consistent, and cross-platform set of APIs.</span></span>

<span data-ttu-id="2e4b6-114">Mit ASP.NET Core können Sie Web-Apps und -dienste, IoT-Apps sowie mobile Back-Ends.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-114">With ASP.NET Core, you can build web apps and services, IoT apps, and mobile back ends.</span></span> <span data-ttu-id="2e4b6-115">ASP.NET Core-Anwendungen können entweder in der Cloud oder lokal gehostet werden.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-115">ASP.NET Core applications can be hosted either in the cloud or on-premises.</span></span>

<span data-ttu-id="2e4b6-116">ASP.NET Core besteht standardmäßig aus einem eingebetteten Webserver und einer Laufzeitumgebung, in der der Anwendungscode ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-116">By design, ASP.NET Core consists of an embedded web server and a runtime environment that runs the application code.</span></span> <span data-ttu-id="2e4b6-117">Der Anwendungscode wird mithilfe eines überarbeiteten ASP.NET MVC-Frameworks geschrieben, das auf kleinere Module und Pakete zurückgreift.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-117">The application code is written using a reworked ASP.NET MVC framework that relies on smaller modules and packages.</span></span> <span data-ttu-id="2e4b6-118">Daraus ergibt sich eine kleinere Webanwendungsblaupause, die mühelos über Cloudumgebungen verwaltet und gehostet werden kann.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-118">The result is a smaller web application blueprint that is easy to maintain and host over cloud environments.</span></span> <span data-ttu-id="2e4b6-119">Die folgende Abbildung zeigt eine in .NET Core gehostete ASP.NET Core-Anwendung und den externen Webserver, der den HTTP-Internetdatenverkehr verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-119">The following illustration shows an ASP.NET Core application hosted in .NET Core and the external web server that handles internet http traffic.</span></span>

![Eine Abbildung mit einer ASP.NET Core-Anwendung und der zugehörigen Ausführungsumgebung](../media/4-asp-net-core-architecture.png)

<span data-ttu-id="2e4b6-121">ASP.NET Core-Anwendungen sind eigenständige **Konsolenanwendungen**, die über das Treibertool **dotnet** aufgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-121">ASP.NET Core applications are standalone **console** applications invoked through the **dotnet** driver tool.</span></span> <span data-ttu-id="2e4b6-122">ASP.NET Core-Anwendungen werden nicht in den IIS-Arbeitsprozess, sondern vielmehr über ein natives IIS-Modul mit dem Namen **AspNetCoreModule** geladen, das die externe Konsolenanwendung ausführt.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-122">ASP.NET Core applications are not loaded into the IIS worker process, but rather, are loaded through a native IIS module called **AspNetCoreModule** that executes the external console application.</span></span>

## <a name="how-to-create-an-aspnet-core-web-project"></a><span data-ttu-id="2e4b6-123">Erstellen eines ASP.NET Core-Webprojekts</span><span class="sxs-lookup"><span data-stu-id="2e4b6-123">How to create an ASP.NET Core web project</span></span>

<span data-ttu-id="2e4b6-124">Zum Erstellen eines neuen ASP.NET Core-Projekts gibt es verschiedene Möglichkeiten:</span><span class="sxs-lookup"><span data-stu-id="2e4b6-124">There are a few options for creating a new ASP.NET Core project:</span></span>

- <span data-ttu-id="2e4b6-125">Sie können Visual Studio-Vorlagen (Windows- und macOS-Versionen) verwenden, um ein neues Projekt zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-125">You can use Visual Studio (Windows and macOS versions) templates to generate a new project.</span></span> <span data-ttu-id="2e4b6-126">Visual Studio bietet eine Vielzahl von Vorlagen, die Sie zum Erstellen von Webprojekten verwenden können.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-126">Visual Studio offers a variety of templates that you can use to create web projects.</span></span> <span data-ttu-id="2e4b6-127">Sie können beispielsweise die Vorlage **Leer** verwenden, um ein reines ASP.NET Core-Projekt mit dem grundlegenden Setup zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-127">For instance, you can use the **Empty** template to create a bare-bones ASP.NET Core project with the basic setup.</span></span> <span data-ttu-id="2e4b6-128">Darüber hinaus können Sie die Vorlage **Webanwendung (Modal-View-Controller)** verwenden, um eine vollwertige ASP.NET Core MVC-Anwendung mit **Beispielcontrollern** und -**ansichten** zu erstellen, die Sie beim Programmieren der Anwendung unterstützen.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-128">In addition, you can use the **Web Application (Modal-View-Controller)** template to generate a full-fledged ASP.NET Core MVC application, with sample **controllers** and **views** that can help you start coding your application.</span></span> <span data-ttu-id="2e4b6-129">Der jüngste Neuzugang ist die Projektvorlage **Webanwendung**, die zum Erstellen eines ASP.NET Core-Projekts basierend auf Razor-Seiten und statt auf der herkömmlichen MVC-Projektstruktur verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-129">The latest arrival is the **Web Application** project template that is used to create an ASP.NET Core project based on Razor pages and not on the traditional MVC project structure.</span></span>

- <span data-ttu-id="2e4b6-130">Sie können die .NET Core-CLI-Tools zum Erstellen eines neuen ASP.NET Core-Projekts verwenden.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-130">You can use the .NET Core CLI tools to generate a new ASP.NET Core project.</span></span> <span data-ttu-id="2e4b6-131">Microsoft stellt allgemeine ASP.NET Core-Projektvorlagen für Visual Studio und die CLI-Tools bereit.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-131">Microsoft maintains an almost common set of ASP.NET Core project templates for both Visual Studio and the CLI tools.</span></span> <span data-ttu-id="2e4b6-132">Dabei unterscheiden sich die Vorlagen für CLI-Tools nur insofern, als dass zum Erstellen eines neuen ASP.NET Core-Projekts Befehle eingegeben werden müssen.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-132">The only difference with the CLI tools is that you need to type commands to create a new ASP.NET Core project.</span></span>
> <span data-ttu-id="2e4b6-133">Die .NET-CLI-Tools nutzen das **Vorlagenmodul** zur Unterstützung unterschiedlicher Projektvorlagen.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-133">The .NET CLI tools make use of the **templating engine** to support different project templates.</span></span>  <span data-ttu-id="2e4b6-134">Weitere Informationen zu dem von den .NET-CLI-Tools intern verwendeten [Vorlagenmodul](https://github.com/dotnet/templating) finden Sie im GitHub-Repository.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-134">To learn more, visit the GitHub repository for the [templating engine](https://github.com/dotnet/templating) used internally by the .NET CLI tools.</span></span>

<span data-ttu-id="2e4b6-135">Die oben beschriebenen Vorlagen gelten als wichtige Tools zum Erstellen von ASP.NET Core-Projekten.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-135">The above are considered the top tools for generating ASP.NET Core projects.</span></span> <span data-ttu-id="2e4b6-136">Es gibt jedoch noch weitere Tools, die Sie suchen und ausprobieren können.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-136">However, there are more tools out there that you can search for and explore.</span></span>

<span data-ttu-id="2e4b6-137">Die Projekte, die mit anderen Tools erstellt werden, können ein wenig anders sein. Sie alle generieren jedoch gültige und optimierte ASP.NET Core-Projekte.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-137">It's worth mentioning that the projects generated by the different tools can be slightly different, however, they all generate valid and optimized ASP.NET Core projects.</span></span>

## <a name="net-cli-tools"></a><span data-ttu-id="2e4b6-138">.NET-CLI-Tools</span><span class="sxs-lookup"><span data-stu-id="2e4b6-138">.NET CLI tools</span></span>

<span data-ttu-id="2e4b6-139">Bei den .NET-CLI-Tools, auch bekannt als .NET Core-CLI, handelt es sich um ein plattformübergreifendes Tool, das Befehle zum Erstellen und Wiederherstellen von Paketen sowie zum Erstellen, Ausführen</span><span class="sxs-lookup"><span data-stu-id="2e4b6-139">The .NET CLI tools, also known as .NET Core CLI, is a cross-platform tool that provides commands for creating and restoring packages, and for building, running.</span></span> <span data-ttu-id="2e4b6-140">und Veröffentlichen von .NET-Anwendungen über die Befehlszeile ohne IDE mit vollem Funktionsumfang bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-140">and publishing .NET applications from the command line without the need for a full-featured IDE.</span></span>

<span data-ttu-id="2e4b6-141">Die .NET-CLI wird als Teil des .NET Core SDK installiert.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-141">The .NET CLI is installed as part of the .NET Core SDK.</span></span> <span data-ttu-id="2e4b6-142">Auf einem Computer können mehrere Versionen der Befehlszeilenschnittstelle vorhanden sein und parallel ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-142">Multiple versions of the CLI can coexist on the same machine and run side by side.</span></span>

<span data-ttu-id="2e4b6-143">Damit Sie die .NET-CLI nutzen können, müssen Sie das entsprechende .NET Core SDK für die Umgebung installieren, die Sie zum Entwickeln der App verwenden: Windows, macOS oder Linux.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-143">To start using the .NET CLI, you need to install the relevant .NET Core SDK with respect to the environment that you are using to develop your app: Windows, macOS, or Linux.</span></span> <span data-ttu-id="2e4b6-144">Wechseln Sie zu [.NET Downloads](https://www.microsoft.com/net/download?initial-os=linux), und wählen Sie das .NET Core SDK für Linux aus.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-144">Go to [.NET Downloads](https://www.microsoft.com/net/download?initial-os=linux) and grab the .NET Core SDK for Linux.</span></span> <span data-ttu-id="2e4b6-145">Ich verwende ein Ubuntu 18.04-Betriebssystem, das unter Windows 10 ausgeführt wird und VMware Workspace Player 14 verwendet, um die von der .NET-CLI bereitgestellten Befehle vorzustellen.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-145">I am using an Ubuntu 18.04 OS running on top Windows 10 using VMware Workspace Player 14 to demonstrate the different commands offered by .NET CLI.</span></span>

<span data-ttu-id="2e4b6-146">Öffnen Sie die Befehlszeile, und geben Sie Folgendes ein:</span><span class="sxs-lookup"><span data-stu-id="2e4b6-146">Open the command line and type the following:</span></span>

```console
dotnet --version
```

<span data-ttu-id="2e4b6-147">Mit diesem Befehl wird die Version der installierten .NET-CLI angezeigt.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-147">This command displays the version of the .NET CLI installed.</span></span>

<span data-ttu-id="2e4b6-148">Wenn ich den obigen Befehl auf meinem Computer ausführe, wird Folgendes angezeigt: `2.1.302`.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-148">Running the above command on my machine displays this: `2.1.302`.</span></span>

<span data-ttu-id="2e4b6-149">Erkunden wir zunächst einige der häufig verwendeten Befehle der .NET-CLI.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-149">Let us start exploring some of the popular commands of the .NET CLI.</span></span>

<span data-ttu-id="2e4b6-150">Der *dotnet*-Befehl weist im Allgemeinen folgende Syntax auf:</span><span class="sxs-lookup"><span data-stu-id="2e4b6-150">The *dotnet* command has the following general syntax:</span></span>

```console
dotnet [verb] [arguments]
```

<span data-ttu-id="2e4b6-151">Das Verb stellt die auszuführende Aktion dar.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-151">The verb represents the action to execute.</span></span> <span data-ttu-id="2e4b6-152">Die Argumente stellen die Liste der Eingabeargumente dar, die das Verb für die Ausführung benötigt.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-152">The arguments represent the list of input arguments that the verb requires in order to execute.</span></span>

<span data-ttu-id="2e4b6-153">Hilfe zur Verwendung von *dotnet* und zur Liste aller verfügbarer *Verben* sowie verwandte Informationen erhalten Sie, indem Sie den folgenden Befehl eingeben:</span><span class="sxs-lookup"><span data-stu-id="2e4b6-153">To get help on the *dotnet* usage and list all of the *verbs* available, and other related information, type the following command:</span></span>

```console
dotnet --help
```

<span data-ttu-id="2e4b6-154">Mit diesem Befehl wird Folgendes angezeigt:</span><span class="sxs-lookup"><span data-stu-id="2e4b6-154">This command displays the following:</span></span>

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

<span data-ttu-id="2e4b6-155">Unter den **SDK-Befehlen** wird die gesamte Liste der Befehle angezeigt, die Sie für das .NET Core SDK ausführen können.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-155">Under the **SDK commands**, you can see the entire list of commands that you can execute against the .NET Core SDK.</span></span>

<span data-ttu-id="2e4b6-156">Folgende Befehle sind die nützlichsten:</span><span class="sxs-lookup"><span data-stu-id="2e4b6-156">The most useful commands at all times are the following:</span></span>

- <span data-ttu-id="2e4b6-157">**dotnet new**: Dieser Befehl wird verwendet, um für eine neue .NET-Anwendung ein Gerüst zu erstellen bzw. eine neue .NET-Anwendung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-157">**dotnet new**: This command is used to scaffold/generate a new .NET application.</span></span>

- <span data-ttu-id="2e4b6-158">**dotnet restore**: Dieser Befehl wird verwendet, um alle von der Anwendung referenzierten Pakete wiederherzustellen/herunterzuladen.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-158">**dotnet restore**: This command is used to restore/download all packages that are referenced by the application.</span></span>

- <span data-ttu-id="2e4b6-159">**dotnet run**: Dieser Befehl wird zum Ausführen der .NET-Anwendung verwendet.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-159">**dotnet run**: This command is used to run your .NET application.</span></span>

<span data-ttu-id="2e4b6-160">Um Unterstützung zur Verwendung eines bestimmten Befehls zu erhalten, können Sie Folgendes eingeben:</span><span class="sxs-lookup"><span data-stu-id="2e4b6-160">Now, to get assistance on how to use a specific command, you can type the following:</span></span>

```console
dotnet run --help
```

<span data-ttu-id="2e4b6-161">Dieser Befehl ergibt Folgendes:</span><span class="sxs-lookup"><span data-stu-id="2e4b6-161">This command results in:</span></span>

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

<span data-ttu-id="2e4b6-162">Mit diesem Befehl werden alle verfügbaren Optionen auflistet, die Sie mit dem `dotnet new`-Befehl verwenden können.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-162">This command lists all the available options that you can use with the `dotnet new` command.</span></span> <span data-ttu-id="2e4b6-163">Ferner werden alle verfügbaren Projektvorlagen aufgelistet, die Sie zum Erzeugen der nächsten .NET-Anwendung verwenden können.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-163">Also, it lists all the available project templates that you can use to generate your next .NET application.</span></span> <span data-ttu-id="2e4b6-164">Und schließlich werden in einem Abschnitt Beispiele zur Verwendung des Befehls zum Erzeugen einer neuen .NET-Anwendung angezeigt.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-164">Finally, a section shows examples on how to use the command to generate a new .NET application.</span></span>

<span data-ttu-id="2e4b6-165">Informationen zu den restlichen Befehlen erhalten Sie, indem Sie das `--help`-Argument für die in der .NET-CLI verfügbaren Befehle verwenden.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-165">You can learn the rest of the commands by using the `--help` argument for any command available in the .NET CLI.</span></span>

## <a name="aspnet-core-installation-on-linux-environment"></a><span data-ttu-id="2e4b6-166">ASP.NET Core-Installation in einer Linux-Umgebung</span><span class="sxs-lookup"><span data-stu-id="2e4b6-166">ASP.NET Core installation on Linux environment</span></span>

<span data-ttu-id="2e4b6-167">Die aktuelle und höchste Version von ASP.NET Core ist Version 2.1.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-167">The latest and greatest version of ASP.NET Core is v2.1.</span></span> <span data-ttu-id="2e4b6-168">Im Allgemeinen wird ASP.NET Core als Teil von .NET Core SDK ausgeliefert.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-168">In general, ASP.NET Core ships as part of the .NET Core SDK.</span></span> <span data-ttu-id="2e4b6-169">Daher können Sie nach der Installation des .NET Core SDK auf Ihrem Computer mit der Entwicklung von .NET Core-Anwendungen, auch von ASP.NET Core-Web-Apps, beginnen.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-169">Therefore, by installing the .NET Core SDK on your machine, you can start developing with any .NET Core application, including ASP.NET Core web apps.</span></span>

<span data-ttu-id="2e4b6-170">Für diese Demonstration verwende ich ein Ubuntu 18.04-Betriebssystem unter Windows 10 zusammen mit VMware Workstation Player.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-170">For this demonstration, I am using an Ubuntu 18.04 OS running on Windows 10, with the help of VMware Workstation Player.</span></span>

<span data-ttu-id="2e4b6-171">Um .NET Core SDK herunterzuladen, besuchen Sie die Startseite [.NET Downloads](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="2e4b6-171">To download the .NET Core SDK, you need to visit the [.NET Downloads](https://www.microsoft.com/net/download) home page.</span></span> <span data-ttu-id="2e4b6-172">Die Seite enthält Links zum Herunterladen des .NET Core SDK auf verschiedene Plattformen: Windows, Linux und MacOS.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-172">The page contains links to download the .NET Core SDK on different platforms: Windows, Linux, and macOS.</span></span>

<span data-ttu-id="2e4b6-173">Klicken Sie auf die Registerkarte **Linux**. Sie haben zwei Möglichkeiten:</span><span class="sxs-lookup"><span data-stu-id="2e4b6-173">Click on the **Linux** tab. You have two options:</span></span>

- <span data-ttu-id="2e4b6-174">.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="2e4b6-174">.NET Core SDK</span></span>
- <span data-ttu-id="2e4b6-175">.NET Core-Runtime</span><span class="sxs-lookup"><span data-stu-id="2e4b6-175">.NET Core Runtime</span></span>

<span data-ttu-id="2e4b6-176">Die .NET Core-Runtime ist bereits im .NET Core SDK enthalten.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-176">The .NET Core Runtime is already contained inside the .NET Core SDK.</span></span> <span data-ttu-id="2e4b6-177">Die Runtime wird zum Ausführen einer Anwendung verwendet.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-177">The runtime is used to run an application.</span></span> <span data-ttu-id="2e4b6-178">Alle Tools zum Entwickeln, Testen, Ausführen und Veröffentlichen sind im .NET Core SDK zu finden.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-178">All the tools to develop, test, run, and publish are inside the .NET Core SDK.</span></span> <span data-ttu-id="2e4b6-179">Klicken Sie daher auf **.NET Core SDK**.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-179">Therefore, you will click on **.NET Core SDK**.</span></span>

<span data-ttu-id="2e4b6-180">Sie werden von der Microsoft-Website zur Downloadseite weitergeleitet.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-180">The Microsoft website redirects you to the download page.</span></span> <span data-ttu-id="2e4b6-181">Dort müssen Sie die **Linux-Distribution** auswählen.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-181">There, you need to select the **Linux Distribution**.</span></span> <span data-ttu-id="2e4b6-182">In meinem Fall wähle ich **Ubuntu 18.04** aus.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-182">In my case, I will select **Ubuntu 18.04**.</span></span> <span data-ttu-id="2e4b6-183">Beim Auswählen werden automatisch Anweisungen zum Installieren des .NET Core SDK unter Ubuntu 18.04 angezeigt.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-183">Automatically, upon selection, the instructions on how to install .NET Core SDK on Ubuntu 18.04 is displayed.</span></span>

## <a name="summary"></a><span data-ttu-id="2e4b6-184">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="2e4b6-184">Summary</span></span>

<span data-ttu-id="2e4b6-185">Wenn Sie eine Webanwendung erstellen möchten, haben Sie die Auswahl zwischen verschiedenen Sprachen und Frameworks.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-185">When deciding to build a web application, you have a choice of many languages and frameworks.</span></span> <span data-ttu-id="2e4b6-186">Azure versucht, Ihnen diese Auswahl zu erleichtern, denn Sie können unterschiedliche Arten von Anwendungen wie Node.js, PHP oder .NET Core hosten.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-186">Azure tries to make this choice easier by allowing you to host different types of applications, like Node.js, PHP, or .NET Core.</span></span> <span data-ttu-id="2e4b6-187">Dadurch können Sie die Sprachen und Frameworks verwenden, mit denen Sie besonders zufrieden sind, und müssen sich nicht an die Anforderungen Ihres Webhosts anpassen.</span><span class="sxs-lookup"><span data-stu-id="2e4b6-187">This allows you to use the languages and frameworks that you're most comfortable with instead of changing to meet the needs of your web host.</span></span>
