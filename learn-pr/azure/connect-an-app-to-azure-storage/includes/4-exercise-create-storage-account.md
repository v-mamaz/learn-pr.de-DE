Nachdem Sie nun über eine App verfügen, benötigen Sie ein Azure-Speicherkonto, mit dem Sie arbeiten können.

## <a name="use-the-azure-cli-to-create-an-azure-storage-account"></a>Erstellen eines Azure-Speicherkontos mithilfe der Azure CLI

Sie verwenden den Befehl `az storage account create`, um ein neues Speicherkonto zu erstellen. Es gibt einige Parameter, um die Konfiguration des Speicherkontos zu steuern.

> [!div class="mx-tableFixed"]
> | Option | Beschreibung |
> |--------|-------------|
> | `--name` | Ein **Speicherkontoname**. Der Name wird zum Generieren der öffentlichen URL verwendet, über die auf die Daten im Konto zugegriffen wird. Dieser Name muss unter allen vorhandenen Speicherkontonamen in Azure eindeutig sein. Er muss 3 bis 24 Zeichen lang sein und darf nur Kleinbuchstaben und Ziffern enthalten. |
> | `--resource-group` | Verwenden Sie **<rgn>[Name der Sandboxressourcengruppe]</rgn>**, um das Speicherkonto in der kostenlosen Sandbox zu platzieren. |
> | `--location` | Wählen Sie einen Standortort in Ihrer Nähe aus (s. unten). |
> | `--kind` | Diese Angabe bestimmt den _Typ_ des Speicherkontos. Zu den verfügbaren Optionen gehören `BlobStorage`, `Storage` und `StorageV2`. |
> | `--sku` | Diese Angabe bestimmt die Leistung und das Replikationsmodell des Speicherkontos. Zu den verfügbaren Optionen gehören `Premium_LRS`, `Standard_GRS`, `Standard_LRS`, `Standard_RAGRS` und `Standard_ZRS`. |
> | `--access-tier` | Die **Zugriffsebene** ist nur für Blob Storage relevant. Zur Auswahl stehen die Optionen [`Cool` \| `Hot`]. Die **heiße Zugriffsebene** ist ideal für häufig verwendete Daten. Die **kalte Zugriffsebene** eignet sich hingegen besser für selten genutzte Daten. Beachten Sie, dass dadurch nur der _Standardwert_ festgelegt wird: Wenn Sie einen Blob erstellen, können Sie einen anderen Wert für die Daten festlegen. |
    
Erstellen Sie anhand der obigen Tabelle eine Befehlszeile in Cloud Shell auf der rechten Seite, um das Konto zu erstellen.
- Verwenden Sie einen eindeutigen Namen. Empfohlen wird ein Wert wie „Fotospeicher“ zusammen mit Ihren Initialen und einer Zufallszahl. Ist der Name nicht eindeutig, tritt ein Fehler auf.
- Normalerweise erstellen Sie eine neue Ressourcengruppe für die Ressourcen Ihrer App. In diesem Fall verwenden Sie jedoch die Sandboxressourcengruppe **<rgn>[Name der Sandboxressourcengruppe]</rgn>**.
- Legen Sie die **SKU** auf „Standard_LRS“ fest. Dadurch wird ein Standardspeicher mit lokaler Replikation verwendet, der für dieses Beispiel ausreichend ist.
- Legen Sie die **Zugriffsebene** auf „Kalte Ebene“ fest.

### <a name="selecting-a-location"></a>Auswählen eines Standorts
<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

### <a name="example-command"></a>Beispielbefehl

```azurecli
az storage account create \
        --name <name> \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --location <region> \
        --kind StorageV2 \
        --sku Standard_LRS \
        --access-tier Cool
```

> [!TIP]
> Ausführlichere Informationen zu Speicherkontooptionen finden Sie bei Interesse im Modul **Erstellen eines Azure-Speicherkontos**.

Die Bereitstellung des Kontos nimmt einige Minuten in Anspruch. In der Zwischenzeit können wir uns die APIs ansehen, die mit diesem Konto verwendet werden.
