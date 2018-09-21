In dieser Einheit erstellen Sie eine ASP.NET Core-Web-App.

## <a name="create-a-new-web-project"></a>Erstellen eines neuen Webprojekts

Das Herzstück der .NET-CLI-Tools ist das Befehlszeilentool `dotnet`. Mit diesem Befehl erstellen Sie ein neues ASP.NET Core-Webprojekt.

Erstellen Sie in Cloud Shell auf der rechten Seite eine neue ASP.NET Core-MVC-Anwendung. Nennen Sie sie „BestBikeApp“.

```bash
dotnet new mvc --name BestBikeApp
```

Der Befehl erstellt einen neuen Ordner namens „BestBikeApp“ für Ihr Projekt. Führen Sie dort `cd` aus, und führen Sie anschließend die Anwendung aus, um sich zu vergewissern, dass sie vollständig ist.

```bash
cd BestBikeApp
dotnet run
```

Das Ergebnis sollte in etwa wie folgt aussehen:

```console
Using launch settings from /home/your-user/Documents/BestBikeApp/Properties/launchSettings.json...
...
Hosting environment: Production
Content root path: /home/your-user/BestBikeApp
Now listening on: http://localhost:5000
Application started.
```

Die Ausgabe beschreibt die Situation nach dem Start Ihrer App: Die Anwendung wird ausgeführt und lauscht am Port 5000.

Wenn Sie die App auf Ihrem eigenen Computer ausführen würden, könnten wir über einen Browser auf http://localhost:5000 zugreifen. Da wir uns in Azure Cloud Shell befinden, müssen wir die App an einem Ort mit einem öffentlichen Endpunkt bereitstellen. Hierzu können wir die App Service-Instanz verwenden, die wir zuvor erstellt haben.