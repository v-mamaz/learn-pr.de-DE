In dieser Übung erstellen Sie auf einem Ubuntu-Computer mithilfe der .NET CLI eine ASP.NET Core-Web-App.

## <a name="aspnet-core-installation-on-linux-environment"></a>ASP.NET Core-Installation in einer Linux-Umgebung

Besuchen Sie die [Downloadseite von .NET ](https://www.microsoft.com/net/download) von Microsoft und führen Sie die Schritte aus, die auf der Seite „.NET Core SDK“ angegeben sind. Sie sind nachstehend geführt. Um die Befehle ausführen zu können, müssen Sie eine neue **Terminal**instanz öffnen, ähnlich wie in diesem Beispiel:

![Terminalistanz](../media-draft/5-terminal-instance.PNG)

### <a name="register-microsoft-key-and-feed"></a>Registrieren von Microsoft-Schlüssel und Feed

Vor der Installation von .NET müssen Sie den Microsoft-Schlüssel und das Produktrepository registrieren sowie die erforderlichen Abhängigkeiten installieren. Dies muss nur pro Computer nur einmal erfolgen.

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

Führen Sie den folgenden Befehl aus, um die Installation zu überprüfen:

```console
dotnet --version
```

Die angezeigte Ausgabe sieht so aus:

```console
2.1.302
```

Bei der Installation des .NET Core SDK wurde auch ASP.NET Core installiert. Lassen Sie uns gemeinsam anschauen, wie Sie mithilfe der .NET CLI ein neues ASP.NET-Core-Projekt mit den zuvor erlernten Befehlen erstellen können.

## <a name="open-a-terminal-window"></a>Öffnen eines Terminalfensters

Zuerst müssen Sie das Terminalfenster ausfindig machen und öffnen. Das Terminalfenster ermöglicht die Ausführung von Befehlen und spielt eine ähnliche Rolle wie das Windows-Fenster „Eingabeaufforderung“.

## <a name="create-a-new-web-project"></a>Erstellen eines neuen Webprojekts

Das Herzstück der .NET CLI-Tools ist das Treibertool *dotnet*. Mit diesem Befehl erstellen Sie ein neues ASP.NET Core-Webprojekt.

Um eine neue ASP.NET Core MVC-Anwendung zu erstellen, müssen Sie lediglich die folgenden Befehle eingeben:

```console
cd ~/Documents
mkdir BestBikeApp   # Hit Enter
cd BestBikeApp      # Hit Enter
dotnet new mvc      # Hit Enter
```

Mit den obigen Befehlen navigieren Sie zum Stammordner *Documents* und erstellen dann ein neues Verzeichnis bzw. einen neuen Ordner. Anschließend wechseln Sie in dieses Verzeichnis bzw. diesen Ordner und geben den .NET CLI-Befehl ein, um eine neue ASP.NET MVC-Anwendung mit allen wiederhergestellten Paketen zu erstellen:

```console
The template "ASP.NET Core Web App (Model-View-Controller)" was created successfully.
This template contains technologies from parties other than Microsoft, see https://aka.ms/aspnetcore-template-3pn-210 for details.

Processing post-creation actions...
Running 'dotnet restore' on /home/your-user/Documents/BestBikeApp/BestBikeApp.csproj...
...
```

Sie müssen jetzt nur noch die Anwendung durch Ausführen dieses Befehls starten:

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

Um HTTPS lokal auf dem Computer im Entwicklungsmodus ausführen zu können, müssen Sie ein selbstsigniertes vertrauenswürdiges **Zertifikat** erstellen.

## <a name="create-a-self-signed-certificate"></a>Erstellen eines selbstsignierten Zertifikats

Führen Sie den folgenden Befehl aus, um ein selbstsigniertes Zertifikat für die Entwicklung zu generieren:

```console
dotnet dev-certs https -v
```

Bei Ausführen des Befehls wird Folgendes zurückgegeben:

```console
The HTTPS developer certificate was generated successfully.
```

## <a name="run-the-application"></a>Ausführen der Anwendung

Für diese Demonstration verwende ich den Browser Firefox.

Öffnen Sie den Browser, und geben die Adresse `http://localhost:5001` ein, um die Anwendung aufzurufen.

![ASP.NET Core MVC-Standardvorlage](../media-draft/5-asp-core-mvc-default-template.PNG)

> Sie müssen für die URL der Anwendung **eine Ausnahme hinzufügen**, da das selbstsignierte Zertifikat für die Entwicklung von Firefox nicht verifiziert werden konnte.

Die Web-App ist betriebsbereit und wird erfolgreich ausgeführt!
