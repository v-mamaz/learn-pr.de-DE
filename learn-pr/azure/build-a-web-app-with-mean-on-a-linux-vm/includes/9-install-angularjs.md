Bei AngularJS handelt es sich um ein Framework zum Erstellen von übersichtlichen und dynamischen Webanwendungen. Verwenden Sie HTML als Sprache für Inhaltsvorlagen, und verwenden Sie eine Syntax für Datenbindungen als Erweiterung. Wenn Sie AngularJS zur Datenbindung und Dependency Injection verwenden, benötigen Sie einen Großteil des Codes nicht, den Sie andernfalls zum Verwalten von Inhaltsaktualisierungen schreiben müssten. Die Inhalte Ihres Benutzers werden innerhalb des Browser aktualisiert, sodass AngularJS mit jeder beliebigen serverseitigen Hostingtechnologie eine Verbindung herstellen kann.

## <a name="angularjs-information"></a>Informationen zu Angular.js

Bei AngularJS handelt es sich um ein Front-End-Framework von JavaScript, das nur den Clients zur Verfügung stehen muss, die auf die Anwendung zugreifen. Es gibt mehrere Möglichkeiten, wie dies erreicht werden kann:

- Verweisen Sie über ein Content Delivery Network (CDN) auf AngularJS.
- Stellen Sie AngularJS über gehosteten Inhalt als Node.js-Paket bereit. Verwenden Sie dabei den Paket-Manager npm.
- Stellen Sie AngularJS über gehosteten Inhalt als Bower-Paket bereit.

In diesem Modul wird AngularJS der Einfachheit halber direkt über ein CDN verwendet. Dadurch wird die Abhängigkeit der Skriptdatei an das CDN übergeben und nicht direkt auf dem Serverinhalt verwaltet. Dies kann abhängig von der Geschwindigkeit und der geografischen Verteilung des für eine entsprechende Ressource verwendeten CDN auch die Geschwindigkeit von Downloads erhöhen.

> [!NOTE]
> AngularJS ist der Vorgänger von Angular, einer vollständigen Neuauflage dieser Webanwendungsplattform. Viele Konzepte der beiden Versionen sind zwar ähnlich, aber es handelt sich jetzt um verschiedene Projekte. Für Angular soll es Versionen mit der Nummer 2.x.y und höher geben, während AngularJS mit Versionen mit der Nummer 1.x.y eingestellt wird. AngularJS wird weiterhin häufig in Webanwendungsszenarios verwendet.

## <a name="how-to-install-angularjs-via-cdn"></a>Installieren von AngularJS über ein CDN

Sie _installieren_ AngularJS nicht wirklich. Sie fügen über ein Skripttag auf Ihrer HTML-Seite einen Verweis auf die JavaScript-Datei hinzu. Da AngularJS für alle Funktionen der Webanwendung sehr wichtig ist, wird es in das Tag `<head>` eingeschlossen (im Vergleich zu späterem Laden von JavaScript-Dateien gegen Ende des Tags `<body>`).

```html
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.7.2/angular.min.js"></script>
```
