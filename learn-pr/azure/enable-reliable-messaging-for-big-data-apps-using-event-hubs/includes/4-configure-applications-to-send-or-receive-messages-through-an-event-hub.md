Nachdem Sie Ihren Event Hub erstellt und konfiguriert haben, müssen Sie Anwendungen für das Senden und Empfangen von Ereignisdatenströmen konfigurieren.

Eine Zahlungsabwicklungslösung verwendet beispielsweise eine Form von Absenderanwendung, um die Kreditkartendaten des Kunden zu erfassen, und eine Empfängeranwendung, um die Gültigkeit der Kreditkarte zu verifizieren.

Es gibt zwar Unterschiede, wie eine Java-Anwendung konfiguriert ist, aber im Vergleich mit einer .NET-Anwendung gelten allgemeine Grundsätze, gemäß denen für Anwendungen die Verbindungsherstellung mit einem Event Hub und das erfolgreiche Senden bzw. Empfangen von Nachrichten ermöglicht werden kann. Obwohl sich die Bearbeitung von Java-Konfigurationstextdateien von der Vorbereitung einer .NET-Anwendung mit Visual Studio unterscheidet, sind die Grundsätze dieselben.

## <a name="what-are-the-minimum-event-hub-application-requirements"></a>Was sind die Mindestanforderungen einer Event Hub-Anwendung?

Um eine Anwendung für das Senden von Nachrichten an einen Event Hub zu konfigurieren, müssen Sie die folgenden Informationen angeben, damit die Anwendung Anmeldeinformationen für die Verbindung erstellen kann:

- Name des Event Hub-Namespace
- Event Hub-Name
- Name der SAS-Richtlinie
- Primärer freigegebener Zugriffsschlüssel

Um eine Anwendung für das Empfangen von Nachrichten von einem Event Hub zu konfigurieren, geben Sie die folgenden Informationen an, damit die Anwendung Anmeldeinformationen für die Verbindung erstellen kann:

- Name des Event Hub-Namespace
- Event Hub-Name
- Name der SAS-Richtlinie
- Primärer freigegebener Zugriffsschlüssel
- Speicherkontoname
- Verbindungszeichenfolge für das Speicherkonto
- Name des Containers mit dem Speicherkonto

Wenn Sie über eine Empfängeranwendung verfügen, die Nachrichten in Azure Blob Storage speichert, müssen Sie auch zunächst ein Speicherkonto einrichten.

## <a name="azure-cli-commands-for-creating-a-general-purpose-standard-storage-account"></a>Azure CLI-Befehle zum Erstellen eines allgemeinen Standardspeicherkontos

Die Azure CLI verfügt über eine Reihe von Befehlen, die Sie zum Erstellen und Verwalten eines Speicherkontos verwenden können. Wir verwenden sie in der nächsten Einheit, aber hier ist eine grundlegende Zusammenfassung der Befehle angegeben. 

> [!TIP]
> Es gibt mehrere MS Learn-Module zu Speicherkonten. Dieses Thema wird ab dem Modul **Einführung in Azure Storage** behandelt.

| Befehl | Beschreibung |
|---------|-------------|
| `storage account create` | Erstellen eines Speicherkontos vom Typ „Allgemein V2“ |
| `storage account key list` | Abrufen des Speicherkontoschlüssels |
| `storage account show-connection-string` | Abrufen der Verbindungszeichenfolge für ein Azure-Speicherkonto |
| `storage container create` | Erstellen eines neuen Containers in einem Speicherkonto |

## <a name="shell-command-for-cloning-an-application-github-repository"></a>Shell-Befehl zum Klonen des GitHub-Repositorys einer Anwendung

Git ist ein Tool für die Zusammenarbeit, das ein verteiltes Versionsverwaltungsmodell verwendet und für die gemeinschaftliche Arbeit an Software- und Dokumentationsprojekten konzipiert ist. Git-Clients sind für mehrere Plattformen, darunter Windows, verfügbar, und die Git-Befehlszeile ist in der Bash Cloud Shell von Azure enthalten. GitHub ist ein webbasierter Hostingdienst für Git-Repositorys. 

Wenn Sie eine Anwendung haben, die als Projekt in GitHub gehostet wird, können Sie eine lokale Kopie des Projekts erstellen, indem Sie dessen Repository mit dem Befehl **git clone** klonen. Wir führen dies in der nächsten Einheit durch.

## <a name="editing-files-in-the-cloud-shell"></a>Bearbeiten von Dateien in Cloud Shell

Sie können einen der integrierten Editoren in Cloud Shell verwenden, um alle Dateien zu ändern, aus denen die Anwendung besteht. Außerdem können Sie Ihren Event Hub-Namespace, Event Hub-Namen, Namen der SAS-Richtlinie und Primärschlüssel hinzufügen. 

Cloud Shell unterstützt **nano**, **vim** und **emacs** sowie einen Visual Studio Code-ähnlichen Editor mit dem Namen **code**. Geben Sie einfach den Namen des gewünschten Editors ein, um ihn in der Umgebung zu starten. Wir verwenden in der nächsten Einheit den Editor **code**.

## <a name="summary"></a>Zusammenfassung

Absender- und Empfängeranwendungen müssen mit spezifischen Informationen für die Event Hub-Umgebung konfiguriert werden. Sie legen ein Speicherkonto an, wenn Ihre Empfängeranwendung Nachrichten in Blob Storage speichert. Wenn Ihre Anwendung auf GitHub gehostet wird, müssen Sie sie in Ihrem lokalen Verzeichnis klonen. Texteditoren wie **nano** werden verwendet, um Ihren Namespace der Anwendung hinzuzufügen.