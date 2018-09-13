In dieser Einheit rufen Sie den Zugriffsschlüssel ab und fügen ihn Ihrer App-Konfiguration hinzu. Da wir eine .NET Core-Konsolenanwendung erstellt haben, müssen wir darüber hinaus der Anwendung Unterstützung für das Lesen von Konfigurationsdateien hinzufügen.

## <a name="create-a-json-configuration-file"></a>Erstellen einer JSON-Konfigurationsdatei

1. Klicken Sie im Visual Studio-Projekt, das wir in der vorherigen Einheit erstellt haben, mit der rechten Maustaste auf das Projekt, und wählen Sie **Hinzufügen** und dann **Neues Element** aus (oder drücken Sie STRG+UMSCHALT+A).

1. Ein modales Dialogfeld wird angezeigt. Wählen Sie **JavaScript-JSON-Konfigurationsdatei** aus, geben Sie **appsettings.json** in das Textfeld *Name* ein, und klicken Sie dann auf **Hinzufügen**.

  ![App-Einstellungen](..\media-draft\7-appsettings.png)

1. Eine Datei wird mit Inhalt, der etwa wie folgt aussieht, dem Projekt hinzugefügt:

    ```json
    {
      "exclude": [
        "**/bin",
        "**/bower_components",
        "**/jspm_packages",
        "**/node_modules",
        "**/obj",
        "**/platforms"
      ]
    }
    ```
1. Entfernen Sie den Eintrag **exclude** sowie die zugehörigen Inhalte, und ersetzen Sie ihn durch einen einzelnen Eintrag **StorageAccountConnectionString** mit einem leeren Zeichenfolgenwert. Es sollte in etwa wie folgt aussehen:

    ```json
    {
      "StorageAccountConnectionString": ""
    }
    ```
1. Wählen Sie die Datei **appsettings.json** aus, klicken Sie mit der rechten Maustaste darauf, und wählen Sie **Eigenschaften** aus (drücken Sie alternativ ALT+EINGABE oder F4).

1. Ändern Sie **In Ausgabeverzeichnis kopieren** in **Kopieren, wenn neuer**.

  ![Buildvorgang](..\media-draft\7-build-action.png)

  > Dadurch wird sichergestellt, dass die App-Konfigurationsdatei in das Ausgabeverzeichnis aufgenommen wird, wenn die App kompiliert/erstellt wird.

## <a name="add-support-to-read-a-json-configuration-file"></a>Hinzufügen von Unterstützung zum Lesen einer JSON-Konfigurationsdatei

Einer .NET Core-Konsolenanwendung müssen bestimmte Bibliotheken hinzugefügt werden, damit sie problemlos eine JSON-Konfigurationsdatei lesen kann.

1. Klicken Sie mit der rechten Maustaste auf das Projekt, und wählen Sie **NuGet-Pakete verwalten...** aus.

![NuGet-Pakete verwalten](..\media-draft\5-manage-nuget-packages.png)

1. Daraufhin wird eine Seite angezeigt, auf der die zu diesem Zeitpunkt installierten NuGet-Pakete aufgeführt sind. Klicken Sie auf die Option **Durchsuchen**, und geben Sie **Microsoft.Extensions.Configuration.Json** in das Suchfeld ein. Das Paket **Microsoft.Extensions.Configuration.Json** wird in den Suchergebnissen angezeigt.

1. Wählen Sie das Paket **Microsoft.Extensions.Configuration.Json** und im rechten Bereich **Installieren** aus.

1. Ein Dialogfeld **Vorschau der Änderungen** wird angezeigt. Klicken Sie auf **OK**.

1. Ein Dialogfeld zur Zustimmung zur Lizenz wird angezeigt. Klicken Sie auf **I Accept** (Annehmen).


## <a name="read-from-the-configuration-file"></a>Lesen der Konfigurationsdatei

Nachdem wir nun die erforderlichen Bibliotheken hinzugefügt haben, um das Lesen der Konfiguration zu ermöglichen, müssen wir diese Funktionalität in unserer Konsolenanwendung aktivieren.

1. Suchen Sie die Datei **Program.cs** in Ihrem Projekt, und öffnen Sie sie in Visual Studio.

1. Am Anfang der Datei befindet sich die Zeile **using System;**. Fügen Sie unter dieser Zeile die folgenden Codezeilen hinzu:

    ```csharp
    using Microsoft.Extensions.Configuration;
    using System.IO;
    ```

1. Ersetzen Sie den Inhalt der Methode **Main** durch folgenden Code:

    ```csharp
    var builder = new ConfigurationBuilder()
        .SetBasePath(Directory.GetCurrentDirectory())
        .AddJsonFile("appsettings.json");

    var configuration = builder.Build();
    ```

1. Ihre Datei **Program.cs** sollte jetzt wie folgt aussehen:

    ```csharp
    using System;
    using Microsoft.Extensions.Configuration;
    using System.IO;

    namespace DemoConsoleApp
    {
        class Program
        {
            static void Main(string[] args)
            {
                var builder = new ConfigurationBuilder()
                    .SetBasePath(Directory.GetCurrentDirectory())
                    .AddJsonFile("appsettings.json");

                var configuration = builder.Build();
            }
        }
    }
    ```

> Dieser Code initialisiert das Konfigurationssystem zum Lesen der Datei **appsettings.json**.

## <a name="add-your-connection-string-to-the-configuration-file"></a>Hinzufügen der Verbindungszeichenfolge zur Konfigurationsdatei

Nun müssen wir die Verbindungszeichenfolge für das Speicherkonto abrufen und in die Konfiguration für die App einfügen.

1. Navigieren Sie zum Azure-Portal für Ihr Abonnement, das Ihr Speicherkonto enthält.

1. Navigieren Sie zum Speicherkonto.

1. Navigieren Sie zum Blatt „Kontoschlüssel“ des Speicherkontos im Portal.

1. Kopieren Sie die Verbindungszeichenfolge **key1**.

1. Fügen Sie den Inhalt des Zugriffsschlüssels, den Sie aus dem Portal kopiert haben, als Wert für **StorageAccountConnectionString** ein. Die Konfiguration sollte nun etwa wie folgt aussehen:

    ```json
    {
      "StorageAccountConnectionString": "your-access-key-connection-string-goes-here"
    }
    ```
