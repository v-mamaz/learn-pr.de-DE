Nun, da es sich um eine app verfügen, benötigen wir arbeiten mit Azure Storage-Konto an. Wir erstellt haben, diesen mithilfe der Azure-Portal in der **erstellen Sie ein Azure Storage-Konto** Modul. Der Azure-Befehlszeilenschnittstelle verwenden wir dieses Mal.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="use-the-azure-cli-to-create-an-azure-storage-account"></a>Verwenden Sie die Azure CLI zum Erstellen von Azure Storage-Konto

Wir verwenden die `az storage account create` Befehl aus, um ein neues Speicherkonto erstellen. Es dauert mehrere Parameter, die wir bereitstellen möchten (oder sollten) sie können Sie konfigurieren sollten.

> [!div class="mx-tableFixed"]
> | Option | Beschreibung |
> |--------|-------------|
> | `--name` | Ein **speicherkontonamen**. Der Name wird zum Generieren der öffentlichen URL für den Zugriff auf die Daten im Konto verwendet werden. Sie müssen für alle vorhandenen speicherkontonamen in Azure eindeutig sein. Er muss 3 bis 24 Zeichen lang sein und darf nur Kleinbuchstaben und Ziffern enthalten. |
> | `--resource-group` | Verwendung <rgn>[Ressourcengruppennamen Sandkasten]</rgn> , das Speicherkonto, das in der kostenlosen Sandbox zu platzieren. |
> | `--location` | Wählen Sie einen Standort in Ihrer Nähe, (siehe unten). |
> | `--kind` | Dadurch wird bestimmt, das Speicherkonto _Typ_. Unter anderem `BlobStorage`, `Storage`, und `StorageV2`. |
> | `--sku` | Diese entscheidet Konto Leistungs- und Speichermodell. Unter anderem `Premium_LRS`, `Standard_GRS`, `Standard_LRS`, `Standard_RAGRS`, und `Standard_ZRS`. |
> | `--access-tier` | Die **Zugriffsebene** ist nur für Blob-Speicher verwendet wird, werden die verfügbaren Optionen sind [`Cool` | `Hot`]. Die **heiße Zugriffsebene** eignet sich ideal für häufig verwendete Daten und die **kalte Zugriffsebene** ist besser für selten genutzte Daten. Beachten Sie, dass dies nur die _Standard_ Wert&mdash;, wenn Sie einen Blob erstellt haben, können Sie einen anderen Wert für die Daten festlegen. |
    
Verwenden Sie in der obigen Tabelle, erstellen Sie eine Befehlszeile in der Cloud Shell auf der rechten Seite, um das Konto erstellen.
- Verwenden Sie einen eindeutigen Namen. Es wird empfohlen, etwa "Photostore" mit Ihren Initialen und eine zufällige Zahl. Sie erhalten einen Fehler, wenn er nicht eindeutig ist.
- Normalerweise würden Sie eine neue Ressourcengruppe, um Ihre app-Ressourcen enthalten, aber in diesem Fall verwenden Sie die Sandbox-Ressourcengruppe erstellen.
- Verwenden Sie "Standard_LRS" für die **Sku**. Diese wird verwenden Standardspeicher mit lokale Replikation, die für dieses Beispiel ausreichend.
- Verwenden von "Kalt" für die **Zugriff auf die Ebene**.

### <a name="selecting-a-location"></a>Auswählen eines Orts
<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

### <a name="example-command"></a>Beispielbefehl

```azurecli
az storage account create \
        --name <name> \
        --resource-group <rgn>[Sandbox resource group name]</rgn> \
        --location <region> \
        --kind StorageV2 \
        --sku Standard_LRS \ 
        --access-tier Cool
```

> [!TIP]
> Wenn Sie Informationen zu die Optionen für das Speicherkonto sind, stellen Sie sicher, durchlaufen die **erstellen Sie ein Azure Storage-Konto** , in denen wir Sie ausführlich wechseln.

Es dauert einige Minuten, bis das Konto bereitstellen. Während es sich bei Azure an, die arbeitet, sehen wir uns auf die APIs, die wir für dieses Konto verwendet werden.