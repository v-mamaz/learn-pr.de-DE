Sie haben erfolgreich Ihre Web-App erstellt und in Azure veröffentlicht. Doch was geschieht, wenn Sie Änderungen vornehmen möchten? Visual Studio merkt sich den Speicherort, in dem die App veröffentlicht ist. So können Sie Ihre App in zwei Klicks aktualisieren und ändern.

## <a name="explore-the-project-structure"></a>Erkunden der Projektstruktur

Sie haben eine ASP.NET-Web-App in Visual Studio erstellt und müssen nun Ihre Website bearbeiten und anpassen. Sehen Sie sich die Projektstruktur und die von Visual Studio erstellten Elemente an.

### <a name="dependencies"></a>Abhängigkeiten

Zu Abhängigkeiten zählen die ASP.NET-Informationen, um Ihre App für die Verwendung einzurichten. Diesen Ordner werden Sie nicht so häufig verwenden, es sei denn, Sie fügen spezielle Pakete von Drittanbietern hinzu.

### <a name="properties"></a>Eigenschaften

Der Ordner „Eigenschaften“ enthält die Konfigurationsdaten für den Speicherort, in dem Sie Ihre Web-App hosten. Wenn Sie nun den Ordner **PublishProfiles** erweitern, sollten Sie die URL der Alpine Ski Hill-Website sehen. Veröffentlichungsprofile bestehen aus einer XML-Datei, die Konfigurationsinformationen zur Veröffentlichung enthält (z.B. die Azure-Adresse), anhand derer Visual Studio Ihre Dateien hochlädt.

### <a name="wwwroot"></a>wwwroot

Die Datei „wwwroot“ enthält alle statischen Ressourcen für Ihre Website, z.B. die CSS-, JS-, Bild- und LIB-Dateien. Diese benötigen Sie, wenn Sie Formatierungsarbeiten vornehmen und weitere Funktionen zu Ihrer Website hinzufügen möchten.

### <a name="pages"></a>Seiten

Der Ordner **Seiten** enthält _**Razor**_-Vorlagen für die Seiten Ihrer Website.
Razor ist eine auf HTML basierende Syntax, die spezielle Konventionen für die Anzeige von Daten und Ausführung von Logik auf Ihrer Website aufweist.

Jede Seite auf Ihrer Website wird durch zwei Codedateien dargestellt:

- Bei der ersten Datei handelt es sich um eine `.cshtml`-Datei, die Razor-Markupdatei. Diese Datei enthält Ihren HTML-Code für die Anzeige und einen gewissen Umfang an C#-Logik.

- Bei der zweiten Datei handelt es sich um eine `.cs`-Datei, die das C#-CodeBehind mit der `PageModel`-Klasse enthält. Mit dieser Datei können Sie HTTP-Anforderungen abfangen und einige Verarbeitungsaufgaben für diese Anforderungen durchführen, bevor Sie Daten an die Razor-Datei übergeben.

### <a name="appsettingjson"></a>appsetting.json

Dies ist eine Konfigurationsdatei für ASP.NET.

### <a name="bundleconfigjson"></a>bundleconfig.json

„bundleconfig.json“ ist eine Konfigurationsdatei für die Vorverarbeitung. Diese Datei sorgt dafür, dass Ihre CSS- und JS-Dateien bei der Veröffentlichung komprimiert werden.

### <a name="programcs-and-startupcs"></a>„Program.cs“ und „Startup.cs“

„Program.cs“ und „Startup.cs“ konfigurieren und starten Ihren Webhost für Ihre Website.

## <a name="updating-your-website-using-razor"></a>Aktualisieren einer Website mithilfe von Razor

Im Folgenden werden einige grundlegende Änderungen an unserer Website vorgenommen. Hierfür benötigen Sie ein grundlegendes Verständnis bezüglich der Nutzung der Razor-Vorlagen zum Anpassen Ihrer Web-App.

## <a name="what-is-razor"></a>Was ist Razor?

Razor ist eine ASP.NET-Syntax zum Erstellen dynamischer Webseiten mit C#. Wenn ein Server eine Razor-Seite liest, wird der C#-Code ausgeführt, bevor er die HTML-Seite rendert. So können Sie schnell dynamische Inhalte generieren.

Razor verwendet `@`-Anweisungen für die Verarbeitung einer Seite mit ASP.NET.

Sehen Sie sich beispielsweise den Code auf der Seite `Contact.cshtml` an:

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

- Die `@page`-Anweisung weist ASP.NET an, diese Datei als Razor-Seite zu verarbeiten.
- Die `@model`-Anweisung weist ASP.NET an, diese Razor-Seite mit einer C#-Klasse namens `ContactModel` zu verknüpfen.

Darüber hinaus verwendet Razor das `@`-Symbol für den Übergang zwischen Code und HTML. Wenn Sie sich den obigen Codeausschnitt ansehen, wird Ihnen `@{ ... }` auffallen. Hierbei handelt es sich um einen **Razor-Codeblock**. Dieser Code wird _ausgeführt, aber nicht gerendert_.

Um die Ausgabe einer Codeanweisung zu rendern, wird `@` vor einem C#-Ausdruck verwendet. Hierzu sehen Sie weiter oben in den Tags `<h2>` und `<h3>` zwei Beispiele im Codeblock.

## <a name="publish-your-updates"></a>Veröffentlichen Ihrer Aktualisierungen

Nachdem Sie die Änderungen an Ihrer Website vorgenommen haben, sollten Sie sie in Azure veröffentlichen. Dieser Prozess ist mit dem der ursprünglichen Veröffentlichung vergleichbar.

1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Projekt.

1. Der Name Ihrer Website gefolgt von „Web Deploy“ sollte nun angezeigt werden. Wenn Sie Ihre Website „AlpineSkiHouse42“ genannt haben, würde unter den verfügbaren Optionen **AlpineSkiHouse42 – Web Deploy** angezeigt werden. Wählen Sie diese Option aus. Ihre Website wird dann in Azure aktualisiert.

## <a name="summary"></a>Zusammenfassung

Die Erstellung und Veröffentlichung einer Website stellen lediglich die ersten Schritte bei der Erstellung einer guten Website dar. Fügen Sie Inhalte hinzu, müssen Sie Ihre Website aktualisieren. Nachdem Sie Ihre Website zunächst in Azure veröffentlicht haben, können Sie sie jederzeit über den Projektmappen-Explorer aktualisieren.
