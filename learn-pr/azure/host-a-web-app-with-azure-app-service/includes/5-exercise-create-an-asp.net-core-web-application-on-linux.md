In dieser Einheit erstellen Sie auf einem Ubuntu-Computer mithilfe der .NET CLI eine ASP.NET Core-Web-App.

## <a name="aspnet-core-installation-on-linux-environment"></a>ASP.NET Core-Installation in einer Linux-Umgebung

Besuchen Sie die [Downloadseite von Microsoft .NET](https://www.microsoft.com/net/download), und führen Sie die Schritte aus, die auf der Seite „.NET Core SDK“ angegeben sind. Sie sind nachstehend aufgeführt. Öffnen Sie zum Ausführen der Befehle eine neue Befehlszeileninstanz vom Typ **Terminal**.

### <a name="register-microsoft-key-and-feed"></a>Registrieren von Microsoft-Schlüssel und Feed

Vor der Installation von .NET müssen Sie den Microsoft-Schlüssel und das Produktrepository registrieren sowie die erforderlichen Abhängigkeiten installieren. Dieser Schritt muss nur einmal pro Computer ausgeführt werden.

```console
~$ wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb
~$ sudo dpkg -i packages-microsoft-prod.deb
```

## <a name="install-the-net-sdk"></a>Installieren des .NET SDK

Aktualisieren Sie die Produkte, die zur Installation verfügbar sind, und installieren Sie das .NET SDK.

Führen Sie an der Eingabeaufforderung die folgenden Befehle aus:

```console
sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get install dotnet-sdk-2.1
```

Während der Installation werden Sie ggf. zur Eingabe des Kennworts Ihres Kontos aufgefordert. Geben Sie Ihr Kennwort ein, und drücken Sie die EINGABETASTE, um fortzufahren.

Geben Sie Folgendes ein, um die Installation zu überprüfen:

```console
dotnet --version
```

Daraufhin wird folgende Ausgabe angezeigt:

```console
2.1.302
```

Bei der Installation des .NET Core SDK wurde auch ASP.NET Core installiert. Sehen wir uns gemeinsam an, wie Sie über die .NET CLI mithilfe der soeben vermittelten Befehle ein neues ASP.NET-Core-Projekt erstellen.

## <a name="open-a-terminal-window"></a>Öffnen eines Terminalfensters

Als Erstes müssen Sie das Terminalfenster öffnen. Das Terminalfenster ermöglicht die Ausführung von Befehlen und hat eine ähnliche Funktion wie das Windows-Fenster „Eingabeaufforderung“.

## <a name="create-a-new-web-project"></a>Erstellen eines neuen Webprojekts

Das Herzstück der .NET CLI-Tools ist das Treibertool *dotnet*. Mit diesem Befehl erstellen Sie ein neues ASP.NET Core-Webprojekt.

Um eine neue ASP.NET Core MVC-Anwendung zu erstellen, müssen Sie lediglich die folgenden Befehle eingeben:

```console
cd ~/Documents
mkdir BestBikeApp   # Hit Enter
cd BestBikeApp      # Hit Enter
dotnet new mvc      # Hit Enter
```

Mit den obigen Befehlen navigieren Sie zum Stammordner *Documents* und erstellen dann einen neuen Ordner. Danach wird der Ordner geöffnet. Und schließlich wird der .NET CLI-Befehl ausgeführt, um eine neue ASP.NET MVC-Anwendung mit allen wiederhergestellten Paketen zu erstellen:

```console
The template "ASP.NET Core Web App (Model-View-Controller)" was created successfully.
This template contains technologies from parties other than Microsoft, see https://aka.ms/aspnetcore-template-3pn-210 for details.

Processing post-creation actions...
Running 'dotnet restore' on /home/your-user/Documents/BestBikeApp/BestBikeApp.csproj...
...
```

Sie müssen jetzt nur noch den folgenden Befehl ausführen, um die Anwendung zu starten:

```console
dotnet run
```

Im *Terminal* zeigt der Befehl *dotnet* einige nützliche Informationen zur aktiven Anwendung an:

```console
Using launch settings from /home/your-user/Documents/BestBikeApp/Properties/launchSettings.json...
...
Hosting environment: Development
Content root path: /home/your-user/Documents/BestBikeApp
Now listening on: https://localhost:5001
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

Die Ausgabe beschreibt die Situation nach dem Start Ihrer Anwendung: Die Anwendung wird ausgeführt und lauscht an den Ports 5001 und 5002 (über HTTPS).

Wenn Sie HTTPS lokal auf dem Computer im Entwicklungsmodus ausführen möchten, müssen Sie ein **selbstsigniertes Zertifikat** erstellen und als vertrauenswürdig einstufen.

## <a name="create-a-self-signed-certificate"></a>Erstellen eines selbstsignierten Zertifikats

Führen Sie den folgenden Befehl aus, um ein selbstsigniertes Entwicklungszertifikat zu generieren:

```console
dotnet dev-certs https -v
```

Nach der Befehlsausführung wird Folgendes zurückgegeben:

```console
The HTTPS developer certificate was generated successfully.
```

## <a name="run-the-application"></a>Ausführen der Anwendung

Für diese Demonstration verwenden wir den Browser Firefox.

Öffnen Sie den Browser, und geben Sie die Adresse `http://localhost:5001` ein, um sich zu vergewissern, dass die Anwendung erfolgreich ausgeführt wird.

![Screenshot einer Webbrowseransicht der Standardwebseite der ASP.NET Core-MVC-Vorlage](../media/5-asp-core-mvc-default-template.PNG)

> [!NOTE]
> Da das selbstsignierte Zertifikat für die Entwicklung von Firefox nicht verifiziert werden konnte, müssen Sie für die URL der Anwendung **eine Ausnahme hinzufügen**.
