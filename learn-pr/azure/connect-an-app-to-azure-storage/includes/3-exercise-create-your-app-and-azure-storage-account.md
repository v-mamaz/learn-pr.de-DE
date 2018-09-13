In dieser Einheit erfahren Sie, wie Sie eine .NET Core-Konsolenanwendung und ein Azure-Speicherkonto erstellen können.

## <a name="create-a-net-core-console-application"></a>Erstellen einer .NET Core-Konsolenanwendung

In diesem Beispiel wird Visual Studio 2017 verwendet, um Ihre App zu erstellen.

1. Klicken Sie in Visual Studio 2017 auf die Menüoption **Datei** > **Neu** > **Projekt**.

1. Klicken Sie in der Kategorie **Visual C# - .NET Core** auf **Console App (.NET Core)** (Konsolen-App (.NET Core)), geben Sie einen Namen für Ihre App ein, und klicken Sie auf **OK**.
  ![Neue App](..\media-draft\3-new-console-app.png)

## <a name="create-an-azure-storage-account"></a>Erstellen eines Azure-Speicherkontos

Sie müssen zunächst ein Speicherkonto erstellen, damit Sie eine Verbindung mit diesem herstellen können.

1. Klicken Sie oben links im Azure-Portal auf „Create a resource“ (Ressource erstellen).

1. Klicken Sie im angezeigten Auswahlbereich auf „Storage“.

1. Klicken Sie rechts in diesem Bereich auf „Speicherkonto – Blob, Datei, Tabelle, Warteschlange“.
  ![Portalauswahl](..\media-draft\3-portal-storage-select.png)

1. Sie müssen die Informationen zu diesem Speicherkonto eingeben. Geben Sie einen Namen für das Speicherkonto an.

1. Eine Ressourcengruppe ist ein logischer Container für Ressourcen. Klicken Sie unter „Ressourcengruppe“ auf die Option **Neu erstellen**, und geben Sie einen Namen für die Ressourcengruppe ein.

1. Behalten Sie für alle anderen Optionen die Standardwerte bei, und klicken Sie auf **Erstellen**.
  ![Portaldetails](..\media-draft\3-portal-storage-details.png)

Dann wird Ihre Ressourcengruppe bereitgestellt. Anschließend wird Ihr Speicherkonto innerhalb der Ressourcengruppe erstellt.
Dann haben Sie Ihre Anwendung erstellt und können sie jetzt konfigurieren und mit Ihrem Speicherkonto verbinden.
