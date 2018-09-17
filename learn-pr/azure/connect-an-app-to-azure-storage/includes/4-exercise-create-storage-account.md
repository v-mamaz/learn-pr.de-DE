Nachdem wir nun über eine App verfügen, benötigen wir ein Azure-Speicherkonto, mit dem wir arbeiten können. Im Modul **Erstellen eines Azure-Speicherkontos** haben wir ein Speicherkonto über das Azure-Portal erstellt. Diesmal verwenden wir die Azure-Befehlszeilenschnittstelle.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="use-the-azure-cli-to-create-an-azure-storage-account"></a>Erstellen eines Azure-Speicherkontos mithilfe der Azure-Befehlszeilenschnittstelle

Wir verwenden den Befehl `az storage account create`, um ein neues Speicherkonto zu erstellen. Dieser Befehl verfügt über mehrere Parameter, die wir angeben müssen (oder sollten), um die gewünschte Konfiguration zu erhalten.

> [!div class="mx-tableFixed"]
> | Option | Beschreibung |
> |--------|-------------|
> | `--name` | Ein **Speicherkontoname**. Der Name wird zum Generieren der öffentlichen URL verwendet, über die auf die Daten im Konto zugegriffen wird. Der Speicherkontoname muss in Azure eindeutig sein. Er muss 3 bis 24 Zeichen lang sein und darf nur Kleinbuchstaben und Ziffern enthalten. |
> | `--resource-group` | Verwenden Sie <rgn>[Name der Sandbox-Ressourcengruppe]</rgn>, um das Speicherkonto in der kostenlosen Sandbox zu platzieren. |
> | `--location` | Wählen Sie einen Ort in Ihrer Nähe aus. |
> | `--kind` | Diese Angabe bestimmt den _Typ_ des Speicherkontos. Mögliche Optionen sind unter anderem „BlobStorage“, „Storage“ und „StorageV2“. |
> | `--sku` | Diese Angabe bestimmt die Leistung und das Replikationsmodell des Speicherkontos. Mögliche Optionen sind unter anderem „Premium_LRS“, „Standard_GRS“, „Standard_LRS“, „Standard_RAGRS“ und „Standard_ZRS“. |
> | `--access-tier` | Die **Zugriffsebene** ist nur für Blob Storage relevant. Mögliche Optionen: „Kalte Ebene“ und „Heiße Ebene“. Die **heiße Zugriffsebene** ist ideal für häufig verwendete Daten. Die **kalte Zugriffsebene** eignet sich hingegen besser für selten genutzte Daten. Beachten Sie, dass dadurch nur der _Standardwert_ festgelegt wird: Bei der Bloberstellung können Sie einen anderen Wert für die Daten festlegen. |
    
Erstellen Sie anhand der obigen Tabelle eine Befehlszeile in Cloud Shell auf der rechten Seite, um das Konto zu erstellen.
- Verwenden Sie einen eindeutigen Namen – beispielsweise „photostore“ mit Ihren Initialen und einer Zufallszahl. Ist der Name nicht eindeutig, tritt ein Fehler auf.
- Normalerweise wird eine neue Ressourcengruppe für die Ressourcen der einer erstellt. In diesem Fall verwenden wir jedoch die Sandbox-Ressourcengruppe.
- Legen Sie die **SKU** auf „Standard_LRS“ fest, um Standardspeicher mit lokaler Replikation zu verwenden, was für dieses Beispiel vollkommen ausreicht.
- Legen Sie die **Zugriffsebene** auf „Kalte Ebene“ fest.

### <a name="selecting-a-location"></a>Auswählen eines Standorts
<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

### <a name="example-command"></a>Beispielbefehl

```bash
az storage account create \
        --name <name> \
        --resource-group <rgn>[Sandbox resource group name]</rgn> \
        --location <region> \
        --kind StorageV2 \
        --sku Standard_LRS \ 
        --access-tier Cold
```

> [!TIP]
> Ausführlichere Informationen zu Speicherkontooptionen finden Sie bei Interesse unter **Erstellen eines Azure-Speicherkontos**.

Die Bereitstellung des Kontos dauert einige Minuten. In der Zwischenzeit können wir uns die APIs ansehen, die mit diesem Konto verwendet werden.