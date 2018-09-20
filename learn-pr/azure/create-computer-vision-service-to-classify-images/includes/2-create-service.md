
## <a name="what-is-microsoft-cognitive-services"></a>Was ist Microsoft Cognitive Services?

Microsoft Cognitive Services ist eine Sammlung von Algorithmen für maschinelles Lernen, die als Dienst für alle Benutzer verfügbar ist. Statt diese Intelligenz selbst von Grund auf zu erstellen, können wir diese Dienste für Sehen, Sprache, Wissen und Suche verwenden. Sie können jeden Dienst kostenlos ausprobieren. Wenn Sie sich dafür entscheiden, einen Dienst in Ihre App zu integrieren, müssen Sie die Registrierung für ein kostenpflichtiges Abonnement durchführen. Wir konzentrieren uns auf die Maschinelles Sehen-API in diesem Modell.

> [!TIP]
> Im [Cognitive Services-Verzeichnis](https://azure.microsoft.com/services/cognitive-services/directory/) finden Sie eine Liste mit sämtlichen Cognitive Services. 

## <a name="what-is-the-computer-vision-api"></a>Was ist die Maschinelles Sehen-API?

Die Maschinelles Sehen-API stellt Algorithmen für die Verarbeitung von Abbildungen und die Rückgabe von Einblicken bereit. Sie können beispielsweise herausfinden, ob eine Abbildung potenziell anstößige Inhalte aufweist oder mithilfe der API alle Gesichter in einer Abbildung finden. Die API verfügt auch über weitere Funktionen, wie z.B. das Schätzen von dominanten Farben und Akzentfarben, das Kategorisieren des Inhalts von Abbildungen sowie das Beschreiben einer Abbildung in vollständigen Sätzen auf Englisch. Darüber hinaus kann die Maschinelles Sehen-API zur effektiven Darstellung großer Bilder auf intelligente Weise Miniaturansichten generieren.

> [!TIP]
> Die Maschinelles Sehen-API ist weltweit in vielen Regionen verfügbar. Unter [Verfügbare Produkte nach Region](https://azure.microsoft.com/global-infrastructure/services/?products=cognitive-services&regions=all) können Sie nach der nächstgelegenen Region suchen.

Sie können mit der Maschinelles Sehen-API folgende Aktionen ausführen:

- Analysieren von Bildern, um Erkenntnisse zu gewinnen
- Extrahieren von gedrucktem Text aus Bildern mittels optischer Zeichenerkennung (Optical Character Recognition, OCR).
- Erkennen von gedrucktem und handschriftlichem Text in Bildern
- Erkennen von Prominenten und Sehenswürdigkeiten
- Analysieren von Videos 
- Generieren von Miniaturansichten eines Bilds 

## <a name="how-to-call-the-computer-vision-api"></a>Aufrufen der Maschinelles Sehen-API

Sie rufen die Maschinelles Sehen-API in Ihrer Anwendung über Clientbibliotheken oder direkt über die REST-API auf. In diesem Modul rufen wir die REST-API auf. So rufen Sie die API auf:

1. Abrufen eines API-Zugriffsschlüssels

    Wenn Sie sich für ein Maschinelles Sehen-Dienstkonto registrieren, werden Ihnen Zugriffsschlüssel zugewiesen. Im Header **jeder** Anforderung muss ein Schlüssel übergeben werden. 

1. POST-Aufruf in der API

    Formatieren Sie die URL wie folgt: **Region**.api.cognitive.microsoft.com/vision/v2.0/**Ressource**/**[Parameter]** 

    - **Region**: die Region, in der Sie das Konto erstellt, z.B. *westus*.
    - **Ressource**: Die von Ihnen aufgerufene Maschinelles Sehen-Ressource, z.B. `analyze`, `describe`, `generateThumbnail`, `ocr`, `models`, `recognizeText` oder `tag`.

    Sie können das zu verarbeitende Bild entweder als unformatiertes Binärbild oder als Bild-URL übermitteln.

    Der Anforderungsheader muss den Abonnementschlüssel enthalten, der Zugriff auf diese API ermöglicht.

1. Analysieren der Antwort

    Die Antwort enthält den Einblick, den die Maschinelles Sehen-API als JSON-Nutzlust in Ihr Bild hatte.

Angenommen, Sie haben ein Maschinelles Sehen-Abonnement in der Region `westus` erstellt und einen Abonnementschlüssel für den Zugriff auf die API erhalten. Geben wir diesem Schlüssel den fiktiven Wert `xxxx-xxxxx-xxxx-xxxx`. Nun möchten Sie für ein Bild unter `http://example.com/images/test.jpg` eine Miniaturansicht generieren. Unter Verwendung von `generateThumbnail` würde die Anforderung wie folgt aussehen.

```
curl POST "https://westus2.api.cognitive.microsoft.com/vision/v2.0/generateThumbnail
-H "Content-Type: application/json"
-H "Ocp-Apim-Subscription-Key: {xxxx-xxxxx-xxxx-xxxx}"
-d "{'url':'http://example.com/images/test.jpg'}"
```

In diesem Modul führen wir alle Übungen in der Azure CLI mithilfe der integrierten Cloud Shell aus. Lassen Sie uns mehr über dieses Setup herausfinden.

## <a name="what-is-the-azure-cli"></a>Was ist die Azure CLI?

Die Azure CLI ist das plattformübergreifende Befehlszeilentool von Microsoft zum Verwalten von Azure-Ressourcen. Sie steht für macOS, Linux und Windows sowie unter Verwendung von [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) im Browser zur Verfügung.

> [!IMPORTANT]
> Es gibt aktuell zwei Versionen der Azure CLI: Azure CLI 1.0 und Azure CLI 2.0. Wir verwenden hier die neueste Version, Azure CLI 2.0, die empfohlen wird, außer wenn Sie ältere Skripts ausführen. Azure CLI 1.0 wird mit dem Befehl `azure` gestartet, und Azure CLI 2.0 mit dem Befehl `az`.

## <a name="az-cognitiveservices-commands"></a>„az cognitiveservices“-Befehle

Die Azure CLI enthält den Befehl `cognitiveservices` zum Verwalten von Cognitive Services-Konten in Azure. Wir können verschiedene Unterbefehle bereitstellen, um bestimmte Aufgaben auszuführen. Dies sind die am häufigsten verwendeten:

| Unterbefehl | Beschreibung |
|-------------|-------------|
| `list` | Auflisten der verfügbaren Azure Cognitive Services-Konten. |
| `account show` | Abrufen der Details eines Azure Cognitive Services-Kontos. |
| `account create` | Erstellen eines Azure Cognitive Services-Kontos. |
| `account delete` | Löschen eines Azure Cognitive Services-Kontos. |
| `keys list` | Auflisten der Details eines Azure Cognitive Services-Kontos. |

Lassen Sie uns nun mithilfe der Azure CLI ein Cognitive Services-Konto.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-cognitive-services-account"></a>Erstellen eines Cognitive Services-Kontos

Für Aufrufe in der Maschinelles Sehen-API benötigen Wir einen API-Zugriffsschlüssel. Damit wir Zugriffsschlüssel abrufen können, benötigen wir ein Cognitive Services-Konto für die Maschinelles Sehen-API. Wir verwenden `az cognitiveservices create` zum Erstellen des Kontos in unserem Abonnement.

 Mit dem Befehl `az cognitiveservices create` wird ein Cognitive Services-Konto in einer Ressourcengruppe erstellt.  Die folgenden fünf Parameter müssen beim Aufrufen dieses Befehls angegeben werden.

> [!Tip]
> Die meisten Flags für Azure CLI-Parameter können so abgekürzt werden, dass sie aus einem einzelnen Zeichen bestehen. Wir könnten beispielsweise `-l` anstelle von `--location` sagen. Die lange Form wird aus Gründen der Übersichtlichkeit verwendet.

| Parameter | Beschreibung |
|-----------|-------------|
| `resource-group` | Die Ressourcengruppe, zu der das Cognitive Services-Konto gehört. Verwenden Sie in dieser interaktiven Sandboxsitzung <rgn>[Sandbox-Ressourcengruppenname]</rgn> |
| `kind` | Der API-Name des Cognitive Services-Kontos. |
| `name` | Der Name des Cognitive Services-Kontos. |
| `sku` | Die SKU des Cognitive Services-Kontos.|
| `location` | Der Standort oder die Region, von dem bzw. von der aus Sie Aufrufe in dieser API durchführen möchten. Wählen Sie mindestens einen Standort aus der nachfolgenden Liste aus. |

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)] 

Führen Sie in Azure Cloud Shell folgenden Befehl aus. Stellen Sie sicher, dass Sie `[location]` durch einen Standort in Ihrer Nähe ersetzen.

```azurecli
az cognitiveservices account create \
--kind ComputerVision \
--name ComputerVisionService \
--sku S1 \
--resource-group <rgn>[Sandbox resource group name]</rgn> \
--location [location]
```

> [!NOTE]
> Merken Sie sich den ausgewählten Standort. Sie müssen alle Aufrufe in der API von dieser Region aus durchführen.

Wir haben ein Cognitive Services-Konto für die **Maschinelles Lernen**-API erstellt. Wir haben die SKU *S1* ausgewählte und unserem Konto den Namen **ComputerVisionService** gegeben. Unser Konto gehört zur Ressourcengruppe **<rgn>[Sandbox-Ressourcengruppenname]</rgn>**, und wir rufen die API von dem im Parameter `--location` festgelegten Standort aus auf. 

Sobald die Erstellung des Cognitive Services-Kontos durch den Befehl abgeschlossen ist, erhalten Sie eine JSON-Antwort. Diese beinhaltet, dass die Eigenschaft **provisioningState** auf **Erfolgreich** festgelegt ist.

## <a name="get-an-access-key"></a>Abrufen eines Zugriffsschlüssels

Sobald wir unser Konto erfolgreich erstellt haben, können wir die Abonnementschlüssel, oder Zugriffsschlüssel, für dieses Konto abrufen.

1. Führen Sie in Azure Cloud Shell folgenden Befehl aus:

    ```azurecli
    az cognitiveservices account keys list \
    --name ComputerVisionService \
    --resource-group <rgn>[Sandbox resource group name]</rgn>
    ```
    
    Der obige Befehl gibt die Schlüssel zurück, die dem Cognitive Services-Konto **ComputerVisionService** zugeordnet sind, das zu der angegebenen Ressourcengruppe gehört. Zwei Schlüssel werden zurückgegeben, einer davon ist ein Ersatzschlüssel. Die Schlüssel sind schwer zu merken. Daher speichern wir den ersten Schlüssel in einer Variable, die wir für sämtliche Aufrufe in der API verwenden werden.

2.  Führen Sie in Azure Cloud Shell folgenden Befehl aus:

    ```azurecli
    key=$(az cognitiveservices account keys list \
    --name ComputerVisionService \
    --resource-group <rgn>[Sandbox resource group name]</rgn> \
    --query key1 -o tsv)
    ```
    
    Die Azure CLI 2.0 verwendet das Argument `--query`, um eine JMESPath-Abfrage für die Ergebnisse von Befehlen auszuführen. JMESPath ist eine Abfragesprache für JSON, die es ermöglicht, Daten aus der CLI-Ausgabe auszuwählen und zu präsentieren. Diese Abfragen werden für die JSON-Ausgabe vor einer anderen Anzeigeformatierung ausgeführt.
    Das Argument `--query` wird von allen Befehlen in der Azure CLI unterstützt. 
    
    In unserem Beispiel wird die Liste der Schlüssel für einen Eintrag mit dem Namen „key1“ abgefragt und das Ergebnis im **TSV**-Format ausgegeben. In diesem Format werden Anführungszeichen um den Zeichenfolgenwert entfernt. Wir weisen das Ergebnis der Variable **Schlüssel** zu.
    
    > [!IMPORTANT]
    > Dieser Schlüssel wird während des gesamten Moduls verwendet. Sie sollten Ihn daher am besten in einer Variable speichern. Wenn Sie den Wert verlieren oder die Variable gelöscht wird, führen Sie den Befehl erneut zum Festlegen einer Variable aus.  

3. Führen Sie in Azure Cloud Shell den folgenden Befehl aus, um den Wert unseres Schlüssels anzuzeigen:

    ```azurecli
    echo $key
    ```

Nun, da wir über ein Konto und einen Schlüssel verfügen, können wir einige Aufrufe in der API durchführen.