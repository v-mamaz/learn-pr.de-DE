Bei AngularJS handelt es sich um ein Framework zum Erstellen von übersichtlichen und dynamischen Webanwendungen. Verwenden Sie HTML als Sprache für Inhaltsvorlagen, und verwenden Sie eine Syntax für Datenbindungen als Erweiterung. Wenn Sie AngularJS zur Datenbindung und Dependency Injection verwenden, benötigen Sie einen Großteil des Codes nicht, den Sie andernfalls zum Verwalten von Updates für Inhalte schreiben müssten. Die Inhalte Ihres Benutzers werden innerhalb des Browser aktualisiert, sodass AngularJS mit jeder beliebigen serverseitigen Hostingtechnologie eine Verbindung herstellen kann.

## <a name="what-must-be-installed"></a>Was muss installiert werden?

Bei AngularJS handelt es sich um ein Front-End-Framework von JavaScript, das nur den Clients zur Verfügung stehen muss, die auf die Anwendung zugreifen. Es gibt mehrere Möglichkeiten, wie dies erreicht werden kann.

1. Verweisen Sie über das Content Delivery Network (CDN) auf AngularJS.
1. Stellen Sie AngularJS über gehosteten Inhalt als Node.js-Paket bereit. Verwenden Sie dabei den Paket-Manager npm.
1. Stellen Sie AngularJS über gehosteten Inhalt als Bower-Paket bereit.

In diesem Modul wird AngularJS der Einfachheit halber direkt über ein CDN verwendet. Dabei wird die Abhängigkeit der Skriptdatei direkt an das CDN übergeben und nicht direkt auf dem Serverinhalt verwaltet. Dadurch kann abhängig von der Geschwindigkeit und der geografischen Verteilung des für eine betreffende Ressource verwendeten CDN auch die Geschwindigkeit von Downloads erhöht werden.

> [!Note]
> AngularJS ist der Vorgänger von Angular, einer vollständigen Neuauflage dieser Webanwendungsplattform. Viele Konzepte der beiden Versionen sind zwar ähnlich, aber es handelt sich um verschiedene Projekte. Für Angular soll es Versionen mit der Nummer 2.x.y und höher geben, während AngularJS mit Versionen mit der Nummer 1.x.y eingestellt wird. AngularJS wird weiterhin häufig in Webanwendungsszenarios verwendet.

## <a name="how-to-install-angularjs-via-cdn"></a>Installieren von AngularJS über ein CDN

    You don't really _install_ AngularJS; you just add a reference to the JavaScript file via a script tag in you HTML page. Since AngularJS is critical to any functionality of our web application, we include it within the `<head>` tag like this (as compared to later loading of JavaScript files toward the end of the `<body>` tag).

    ```html
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.7.2/angular.min.js"></script>
    ```
