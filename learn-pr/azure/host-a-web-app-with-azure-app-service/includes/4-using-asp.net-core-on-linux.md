Sie möchten zum Erstellen einer Webanwendung eine Open-Source-Technologie verwenden. Sie wissen, dass ASP.NET Core ein plattformübergreifendes Open-Source-Framework ist. Sie möchten Ihre Web-App in einer Linux-Entwicklungsumgebung mithilfe von ASP.NET Core entwickeln.

Mit Azure App Service können Sie Ihre bevorzugte Webtechnologie verwenden, einschließlich Node.js, PHP oder .NET Core.

Hier erfahren Sie, wie Sie eine ASP.NET Core-Anwendung mit der Befehlszeilenschnittstelle (CLI) von .NET erstellen.

## <a name="what-is-aspnet-core"></a>Was ist ASP.NET Core?

ASP.NET Core ist die neueste Entwicklung des bekannten ASP.NET-Webframeworks von Microsoft, ein plattformübergreifendes Open-Source-Framework zum Erstellen von modernen, cloudbasierten und mit dem Internet verbundenen Anwendungen.

ASP.NET Core-Anwendungen können für .NET Core Framework oder für das gesamte vorhandene .NET Framework geschrieben werden.

Da es sich um ein plattformübergreifendes Open Source-Framework handelt, können Sie ASP.NET Core-Apps auf unterschiedlichen Plattformen erstellen, so auch unter Windows, macOS und Linux. Die Visual Studio-IDE für Windows- und macOS-Umgebungen wird von Microsoft bereitgestellt. Zudem ist der Visual Studio Code-Editor plattformübergreifend und mit diesen Umgebungen sowie mit Linux kompatibel.

>Um das Erstellen von ASP.NET Core-Anwendungen auf unterschiedlichen Plattformen zu unterstützten, hat Microsoft die .NET Core-CLI-Tools eingeführt. Mit diesen Tools können Sie Ihre Anwendungen mit umfangreichen, konsistenten und plattformübergreifenden APIs erstellen, testen und veröffentlichen.

Mit ASP.NET Core können Sie Web-Apps und -dienste, IoT-Apps sowie mobile Back-Ends. ASP.NET Core-Anwendungen können entweder in der Cloud oder lokal gehostet werden.

ASP.NET Core besteht standardmäßig aus einem eingebetteten Webserver und einer Laufzeitumgebung, in der der Anwendungscode ausgeführt wird. Der Anwendungscode wird mithilfe eines überarbeiteten ASP.NET MVC-Frameworks geschrieben, das auf kleinere Module und Pakete zurückgreift. Daraus ergibt sich eine kleinere Webanwendungsblaupause, die mühelos über Cloudumgebungen verwaltet und gehostet werden kann. Die folgende Abbildung zeigt eine in .NET Core gehostete ASP.NET Core-Anwendung und den externen Webserver, der den HTTP-Internetdatenverkehr verarbeitet.

![Eine Abbildung mit einer ASP.NET Core-Anwendung und der zugehörigen Ausführungsumgebung](../media/4-asp-net-core-architecture.png)

ASP.NET Core-Anwendungen sind eigenständige **Konsolenanwendungen**, die über das Treibertool **dotnet** aufgerufen werden. ASP.NET Core-Anwendungen werden nicht in den IIS-Arbeitsprozess, sondern vielmehr über ein natives IIS-Modul mit dem Namen **AspNetCoreModule** geladen, das die externe Konsolenanwendung ausführt.

## <a name="how-to-create-an-aspnet-core-web-project"></a>Erstellen eines ASP.NET Core-Webprojekts

Es gibt zwei häufig verwendete Optionen zum Erstellen eines neuen ASP.NET Core-Projekts:

- Sie können Visual Studio-Vorlagen (Windows- und macOS-Versionen) verwenden, um ein neues Projekt zu erstellen. Visual Studio bietet eine Vielzahl von Vorlagen, die Sie zum Erstellen von Webprojekten verwenden können. Sie können beispielsweise die Vorlage **Leer** verwenden, um ein reines ASP.NET Core-Projekt mit dem grundlegenden Setup zu erstellen. Darüber hinaus können Sie die Vorlage **Webanwendung (Modal-View-Controller)** verwenden, um eine vollwertige ASP.NET Core MVC-Anwendung mit **Beispielcontrollern** und -**ansichten** zu erstellen, die Sie beim Programmieren der Anwendung unterstützen. Der jüngste Neuzugang ist die Projektvorlage **Webanwendung**, die zum Erstellen eines ASP.NET Core-Projekts basierend auf Razor-Seiten und statt auf der herkömmlichen MVC-Projektstruktur verwendet wird.

- Sie können die .NET Core-CLI-Tools zum Erstellen eines neuen ASP.NET Core-Projekts verwenden. Microsoft verwaltet eine Reihe von ASP.NET Core-Projektvorlagen für die CLI-Tools, die nahezu identisch mit den Visual Studio-Vorlagen sind. Der einzige Unterschied zu den CLI-Tools besteht darin, dass Sie die Befehle zum Erstellen eines neuen ASP.NET Core-Projekts eingeben müssen.
> Die .NET-CLI-Tools nutzen die **Vorlagen-Engine** zur Unterstützung unterschiedlicher Projektvorlagen.  Weitere Informationen zu der von den .NET-CLI-Tools intern verwendeten [Vorlagen-Engine](https://github.com/dotnet/templating) finden Sie im zugehörigen GitHub-Repository.

Hierbei handelt es sich um die am häufigsten verwendeten Tools zum Erstellen von ASP.NET Core-Projekten. Es gibt jedoch noch weitere Tools, die Sie suchen und ausprobieren können.

Die Projekte, die mit anderen Tools erstellt werden, können ein wenig anders sein. Sie alle generieren jedoch gültige und optimierte ASP.NET Core-Projekte.

## <a name="net-cli-tools"></a>.NET-CLI-Tools

Bei den .NET-CLI-Tools (auch als „NET Core-CLI“ bekannt) handelt es sich um plattformübergreifende Tools, die Befehle zum Erstellen und Wiederherstellen von Paketen und zum Erstellen, Ausführen und Veröffentlichen von .NET-Anwendungen über die Befehlszeile bereitstellen, ohne dass eine IDE mit vollem Funktionsumfang erforderlich ist.

Die .NET-CLI wird als Teil des .NET Core SDK installiert. Auf einem Computer können mehrere Versionen der CLI vorhanden sein und parallel ausgeführt werden.

Bei der lokalen Entwicklung müssen Sie das relevante .NET Core SDK installieren, um die .NET-CLI verwenden zu können. In Azure Cloud Shell ist die .NET-CLI bereits installiert.

Öffnen Sie die Befehlszeile, und geben Sie Folgendes ein:

```console
dotnet --version
```

Mit diesem Befehl wird die Version der installierten .NET-CLI angezeigt.

Zum Zeitpunkt der Erstellung dieses Dokuments wird Folgendes beim Ausführen des Befehls in Azure Cloud Shell zurückgegeben: `2.0.0`. Neuere Versionen stehen zur Verfügung, und möglicherweise ist eine neuere Version bereits auf Ihrem lokalen Computer installiert.

Sehen Sie sich zunächst einige der häufig verwendeten Befehle der .NET-CLI an.

Der *dotnet*-Befehl weist im Allgemeinen folgende Syntax auf:

```console
dotnet [verb] [arguments]
```

Das Verb stellt die auszuführende Aktion dar. Die Argumente stellen die Liste der Eingabeargumente dar, die das Verb für die Ausführung benötigt.

Hilfe zur Verwendung von *dotnet* und zur Liste aller verfügbarer *Verben* sowie verwandte Informationen erhalten Sie, indem Sie den folgenden Befehl eingeben:

```console
dotnet --help
```

Mit diesem Befehl wird Folgendes angezeigt:

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

Unter den **SDK-Befehlen** wird die gesamte Liste der Befehle angezeigt, die Sie für das .NET Core SDK ausführen können.

Folgende Befehle sind die nützlichsten:

- **dotnet new**: Dieser Befehl wird verwendet, um für eine neue .NET-Anwendung ein Gerüst zu erstellen bzw. eine neue .NET-Anwendung zu erstellen.

- **dotnet restore**: Dieser Befehl wird verwendet, um alle von der Anwendung referenzierten Pakete wiederherzustellen/herunterzuladen.

- **dotnet run**: Dieser Befehl wird zum Ausführen der .NET-Anwendung verwendet.

Um Unterstützung zur Verwendung eines bestimmten Befehls zu erhalten, können Sie Folgendes eingeben:

```console
dotnet new --help
```

Dieser Befehl ergibt Folgendes:

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

Mit diesem Befehl werden alle verfügbaren Optionen auflistet, die Sie mit dem `dotnet new`-Befehl verwenden können. Ferner werden alle verfügbaren Projektvorlagen aufgelistet, die Sie zum Erzeugen der nächsten .NET-Anwendung verwenden können. Und schließlich werden in einem Abschnitt Beispiele zur Verwendung des Befehls zum Erzeugen einer neuen .NET-Anwendung angezeigt.

Informationen zu den restlichen Befehlen erhalten Sie, indem Sie das `--help`-Argument für die in der .NET-CLI verfügbaren Befehle verwenden.

## <a name="summary"></a>Zusammenfassung

Wenn Sie eine Webanwendung erstellen möchten, haben Sie die Wahl zwischen verschiedenen Sprachen und Frameworks. App Service versucht, Ihnen diese Wahl zu erleichtern, denn Sie können unterschiedliche Arten von Anwendungen wie Node.js, PHP oder .NET Core hosten. Dadurch können Sie die Sprachen und Frameworks verwenden, mit denen Sie besonders zufrieden sind, und müssen sich nicht an die Anforderungen Ihres Webhosts anpassen.
