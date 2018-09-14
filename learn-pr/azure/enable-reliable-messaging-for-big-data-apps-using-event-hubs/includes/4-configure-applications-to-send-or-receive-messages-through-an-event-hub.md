Nachdem Sie Ihren Event Hub erstellt und konfiguriert haben, müssen Sie Anwendungen für das Senden und Empfangen von Ereignisdatenströmen konfigurieren.

Eine Zahlungsabwicklungslösung verwendet beispielsweise eine Form von Absenderanwendung, um die Kreditkartendaten des Kunden zu erfassen, und eine Empfängeranwendung, um die Gültigkeit der Kreditkarte zu verifizieren.

Obwohl es Unterschiede gibt, wie eine Java-Anwendung konfiguriert ist, gelten im Vergleich mit einer .NET-Anwendung allgemeine Grundsätze, gemäß denen Anwendungen die Verbindung mit einem Event Hub und das erfolgreiche Senden oder Empfangen von Nachrichten ermöglicht werden können. Obwohl sich die Bearbeitung von Java-Konfigurationstextdateien von der Vorbereitung einer.NET-Anwendung mit Visual Studio unterscheidet, sind die Grundsätze dieselben.

## <a name="what-are-the-minimum-event-hub-application-requirements"></a>Was sind die Mindestanforderungen einer Event Hub-Anwendung?

Um eine Anwendung für das Senden von Nachrichten an einen Event Hub zu konfigurieren, müssen Sie die folgenden Informationen angeben, damit die Anwendung Anmeldeinformationen für die Verbindung erstellen kann:

- Name des Event Hub-Namespace
- Event Hub-Name
- Name der freigegebenen Zugriffsrichtlinie
- Primärer freigegebener Zugriffsschlüssel

Um eine Anwendung für das Empfangen von Nachrichten von einen Event Hub zu konfigurieren, geben Sie die folgenden Informationen an, damit die Anwendung Anmeldeinformationen für die Verbindung erstellen kann:

- Name des Event Hub-Namespace
- Event Hub-Name
- Name der freigegebenen Zugriffsrichtlinie
- Primärer freigegebener Zugriffsschlüssel
- Speicherkontoname
- Verbindungszeichenfolge für das Speicherkonto
- Name des Containers mit dem Speicherkonto

Wenn Sie über eine Empfängeranwendung verfügen, die Nachrichten in Azure Blob Storage speichert, müssen Sie auch zunächst ein Speicherkonto einrichten.

## <a name="the-azure-cli-commands-for-creating-a-general-purpose-standard-storage-account"></a>Die Azure CLI-Befehle zum Erstellen eines allgemeinen Standardspeicherkontos

1. Erstellen Sie ein allgemeines V2-Storage-Konto in Ihrer Ressourcengruppe und denselben Azure-Datencenter-Speicherort, den Sie beim Erstellen der Ressourcengruppe verwendet.

    ```azurecli
    az storage account create --name <storage account name> --resource-group <resource group name> --location <location> --sku Standard_RAGRS --encryption blob
    ```

1. Um auf diesen Speicher zugreifen zu können, benötigen Sie einen Zugriffsschlüssel für das Speicherkonto. Zeigen Sie die Zugriffsschlüssel an, die dem Speicherkonto zugeordnet sind.

    ```azurecli
    az storage account keys list --account-name <storage account name> --resource-group <resource group name>
    ```

1. Speichern Sie den **key1** zugeordneten Wert.

1. Sie benötigen auch die Verbindungsdetails für das Speicherkonto. Zeigen Sie die Verbindungszeichenfolge für das Speicherkonto an.

    ```azurecli
    az storage account show-connection-string -n <storage account name> -g <resource group name>
    ```

1. Speichern Sie den **connectionString** zugeordneten Wert.

1. Nachrichten werden in einem Container in Ihrem Speicherkonto gespeichert. Erstellen Sie einen Container in Ihrem Speicherkonto, indem Sie `<connection string>` mit der Verbindungszeichenfolge aus dem vorherigen Schritt verwenden.

    ```azurecli
    az storage container create -n <container> --connection-string "<connection string>"
    ```

## <a name="shell-command-for-cloning-an-application-github-repository"></a>Shell-Befehl zum Klonen des GitHub-Repositorys einer Anwendung

Git ist ein Tool für die Zusammenarbeit, das ein verteiltes Versionsverwaltungsmodell verwendet und für die gemeinschaftliche Arbeit an Software- und Dokumentationsprojekten konzipiert ist. Git-Clients sind für mehrere Plattformen, darunter Windows, verfügbar, und die Git-Befehlszeile ist in der Bash Cloud Shell von Azure enthalten. GitHub ist ein webbasierter Hostingdienst für Git-Repositorys. 

Wenn Sie eine Anwendung haben, die als Projekt in GitHub gehostet wird, können Sie eine lokale Kopie des Projekts erstellen, indem Sie dessen Repository mit dem Befehl **git clone** klonen.

1. Klonen Sie ein Repository in Ihr Basisverzeichnis.

    ```azurecli
      git clone https://github.com/<project repository>
    ```

## <a name="shell-commands-for-preparing-an-application"></a>Shellbefehle für das Vorbereiten einer Anwendung

1. Sie können nun einen Editor wie **Nano** einsetzen, um die Anwendung zu bearbeiten und den Namespace und Namen Ihres Event Hubs, den Namen der freigegebenen Zugriffsrichtlinie und den Primärschlüssel hinzufügen. Nano ist ein einfacher Texteditor, der für Linux und andere Unix-ähnliche Betriebssysteme sowie auch in der Bash Cloud Shell von Azure zur Verfügung steht. Verwenden Sie diesen Befehl z.B. zum Öffnen einer Java-Anwendungsdatei im **Nano**-Editor.

    ```azurecli
    nano <application>.java
    ```

1. Je nachdem, wie Ihre Anwendungen entwickelt werden, müssen Sie die Anwendung möglicherweise kompilieren oder einen Build dafür erstellen, nachdem Sie die Konfigurationsinformationen für den Event Hub hinzugefügt haben. Die Java-Anwendungen, die in der nächsten Einheit verwendet werden, müssen beispielsweise mithilfe eines Tools wie Apache **Maven** erstellt werden. Maven kompiliert JAVA-Dateien in CLASS-Dateien oder packt sie zu JAR-Dateien. Maven ist in der Bash Cloud Shell verfügbar. Zum Erstellen der Java-Anwendung verwenden Sie **mvn**-Befehle. Verwenden Sie diesen mvn-Befehl, um eine Java-Anwendung zu erstellen.

    ```azurecli
    mvn clean package -DskipTests
    ```

## <a name="summary"></a>Zusammenfassung

Absender- und Empfängeranwendungen müssen mit spezifischen Informationen für die Event Hub-Umgebung konfiguriert werden. Sie legen ein Speicherkonto an, wenn Ihre Empfängeranwendung Nachrichten in Blob Storage speichert. Wenn Ihre Anwendung auf GitHub gehostet wird, müssen Sie sie in Ihr lokales Verzeichnis klonen. Texteditoren wie **Nano** werden verwendet, um Ihren Namespace der Anwendung hinzufügen.