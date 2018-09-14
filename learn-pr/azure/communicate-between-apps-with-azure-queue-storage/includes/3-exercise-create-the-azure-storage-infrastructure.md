Sie haben herausgefunden, dass Datenverkehrsspitzen die Logikschicht überfordern. Sie haben eine Warteschlange zwischen dem Front-End und der Logikschicht in Ihre Anwendung zum Hochladen von Artikeln eingefügt, um dies zu bewältigen.

Der erste Schritt beim Erstellen einer Warteschlange besteht darin, das Azure Storage-Konto zu erstellen, in dem Ihre Daten gespeichert werden sollen.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-storage-account-with-the-azure-cli"></a>Erstellen eines Speicherkontos mit Azure CLI

> [!TIP] 
> Normalerweise würden Sie zunächst ein neues Projekt erstellen eine _Ressourcengruppe_ um alle zugehörigen Ressourcen zu speichern. In diesem Fall wir verwenden die Azure-Sandbox bietet eine Ressourcengruppe namens <rgn>[Ressourcengruppennamen Sandkasten]</rgn>.

1. Wenn Ihnen rechts in Cloud Shell eine Auswahl angezeigt wird, wählen Sie Bash aus.

1. Verwenden der `az storage account create` Befehl aus, um das Speicherkonto zu erstellen. Sie müssen mehrere Parameter angeben:

| Parameter | Wert |
|-----------|-------|
| `--name`  | Legt den Namen fest. Denken Sie daran, dass Speicherkonten den Namen zum Generieren einer öffentlichen URL verwenden. Deshalb muss dieser eindeutig sein. Darüber hinaus muss der Kontoname zwischen 3 und 24 Zeichen enthalten und darf nur aus Zahlen und Kleinbuchstaben bestehen. Es wird empfohlen, dass Sie das Präfix **articles** mit einer zufälligen Zahl als Suffix verwenden, aber Sie können auch einen beliebigen Namen verwenden. |
| `-g`        | Stellt die **Ressourcengruppe**, verwenden Sie <rgn>[Ressourcengruppennamen Sandkasten]</rgn> als Wert. |
| `--kind`    | Legt die **speicherkontotyp** -verwenden Sie _StorageV2_ um ein allgemeines V2-Konto zu erstellen. |
| `-l`        | Legt die **Speicherort** unabhängig vom Besitzer Gruppe der Ressource. Dies ist optional, aber so können Sie die Warteschlange in einer anderen Region als die Ressourcengruppe platzieren. |
| `--sku`     | Legt die **Duplizierungen und Speicheranforderungen Typ**, wird standardmäßig _Standard_RAGRS_. Verwenden Sie _Standard_LRS_, damit der Speicher nur innerhalb des Rechenzentrums lokal redundant ist. |

<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

Hier sehen Sie eine Beispielbefehlszeile, die die obigen Parameter verwendet. Stellen Sie sicher, dass die `--name` und `--location` Parameter, wenn Sie sich entscheiden, können Sie mit diesem Befehl Kopieren und einfügen.

```azurecli
az storage account create --name [unique-name] -g <rgn>[Sandbox resource group name]</rgn> --kind StorageV2 -l [location-name] --sku Standard_LRS
```