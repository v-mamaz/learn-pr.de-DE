Sie haben herausgefunden, dass Datenverkehrsspitzen die Logikschicht überfordern. Sie haben eine Warteschlange zwischen dem Front-End und der Logikschicht in Ihre Anwendung zum Hochladen von Artikeln eingefügt, um dies zu bewältigen.

Der erste Schritt beim Erstellen einer Warteschlange besteht darin, das Azure Storage-Konto zu erstellen, in dem Ihre Daten gespeichert werden sollen.

## <a name="create-a-storage-account-with-the-azure-cli"></a>Erstellen eines Speicherkontos mit Azure CLI

Erstellen Sie zunächst eine Azure-Ressourcengruppe, die das Speicherkonto enthalten soll.

1. Wenn Ihnen rechts in Cloud Shell eine Auswahl angezeigt wird, wählen Sie Bash aus.

2. Verwenden Sie den Azure CLI-Befehl `az group create`, um eine neue Ressourcengruppe zu erstellen. Geben Sie ihr den Namen **ExerciseResources**, und platzieren Sie sie an einem Standort in Ihrer Nähe. 
    - Im folgenden Beispiel wird „eastus“ (USA, Osten) als Standort verwendet.

    ```azurecli
    az group create -n ExerciseResources --location eastus
    ```
        
2. Führen Sie als Nächstes den Befehl `az storage account create` aus, um das Speicherkonto zu erstellen. Sie müssen mehrere Parameter angeben:

| Parameter | Wert |
|-----------|-------|
| `--name`  | Legt den Namen fest. Denken Sie daran, dass Speicherkonten den Namen zum Generieren einer öffentlichen URL verwenden. Deshalb muss dieser eindeutig sein. Darüber hinaus muss der Kontoname zwischen 3 und 24 Zeichen enthalten und darf nur aus Zahlen und Kleinbuchstaben bestehen. Es wird empfohlen, dass Sie das Präfix **articles** mit einer zufälligen Zahl als Suffix verwenden, aber Sie können auch einen beliebigen Namen verwenden. |
| `-g`        | Stellt die Ressourcengruppe bereit, verwenden Sie **ExerciseResources** als Wert. |
| `--kind`    | Legt den Typ des Speicherkontos fest. Verwenden Sie **StorageV2**, um ein allgemeines V2-Konto zu erstellen. |
| `-l`        | Legt den Speicherort unabhängig vom Besitzer der Ressourcengruppe fest. Dies ist optional, aber so können Sie die Warteschlange in einer anderen Region als die Ressourcengruppe platzieren. |
| `--sku`     | Legt den Kontotyp fest, standardmäßig wird **Standard_RAGRS** verwendet, was für diese Demonstration jedoch zu weit gehen würde. Verwenden Sie **Standard_LRS**, damit der Speicher nur innerhalb des Rechenzentrums lokal redundant ist. |

Hier sehen Sie eine Beispielbefehlszeile, die die obigen Parameter verwendet. Stellen Sie sicher, dass Sie den `--name`-Parameter in etwas Eindeutiges ändern, wenn Sie diesen Befehl kopieren und einfügen möchten.

```azurecli
az storage account create --name <name> -g ExerciseResources --kind StorageV2 -l eastus --sku Standard_LRS
```
