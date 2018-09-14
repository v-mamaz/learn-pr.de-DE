
## <a name="what-is-microsoft-cognitive-services"></a>Was ist Microsoft Cognitive Services?

Microsoft Cognitive Services handelt es sich um einen Satz von Machine learning-Algorithmen, die als Dienst für alle Benutzer verfügbar. Anstelle dieses Intelligence für unsere apps von Grund auf neu erstellen, können wir diese Dienste für Bildanalyse, Spracherkennung, wissen und Suche verwenden. Sie können jeden Dienst kostenlos testen. Wenn Sie einen Dienst in Ihre app integrieren möchten, registrieren Sie ein kostenpflichtiges Abonnement. Wir konzentrieren wir unsere Aufmerksamkeit auf die Computer Vision-API in diesem Modell.

> [!TIP]
> Um eine Liste aller Cognitive Services anzuzeigen, sehen Sie sich die [Cognitive Services-Verzeichnis](https://azure.microsoft.com/services/cognitive-services/directory/). 

## <a name="what-is-the-computer-vision-api"></a>Was ist das Computer Vision-API?

Das Computer Vision-API bietet die Algorithmen für die Bearbeitung von Bildern und Insights zurück. Beispielsweise können Sie feststellen, ob ein Bild ausgereifte Inhalt oder sie alle die Gesichter in einem Bild suchen können. Es enthält auch andere Funktionen wie dominanten und Akzentfarben schätzen und kategorisieren den Inhalt des Images, die ein Bild mit vollständigen englischen Sätzen beschreibt. Darüber hinaus können sie auch auf intelligente Weise Miniaturansichten der Bilder zum Anzeigen von großen Bildern effektiv generieren.

> [!TIP]
> Das Computer Vision-API ist in vielen Regionen auf der ganzen Welt verfügbar. Die Region in Ihrer Nähe finden Sie unter den [verfügbare Produkte nach Region](https://azure.microsoft.com/global-infrastructure/services/?products=cognitive-services&regions=all).

Sie können das Computer Vision-API zu verwenden:

- Analysieren Sie Bilder Einblicke
- Extrahieren Sie gedruckten Text aus Bildern mittels optischer zeichenerkennung (OCR).
- Gedruckte und handschriftlichen Text aus Bildern zu erkennen
- Berühmte Personen und Orientierungspunkte erkennen
- Analysieren von Videos 
- Generieren einer Miniaturansicht eines Bilds 

## <a name="how-to-call-the-computer-vision-api"></a>Gewusst wie: Aufrufen der maschinelles sehen-API

Sie haben Computer Vision in Ihrer Anwendung mithilfe von Clientbibliotheken oder der REST-API direkt aufrufen. Wir rufen die REST-API in diesem Modul. So erstellen Sie einen Aufruf

1. Abrufen eines API-Zugriffsschlüssels

    Zugriffsschlüssel werden zugewiesen werden, wenn Sie sich für ein maschinelles sehen-Dienstkonto registrieren. Ein Schlüssel muss im Header des übergeben werden **jeder** Anforderung. 

1. Stellen Sie einen POST-Aufruf an die API

    Formatieren Sie die URL folgendermaßen: **Region**.api.cognitive.microsoft.com/vision/v2.0/**Ressource**/**[Parameter]** 

    - **Region** : die Region, in dem Sie das Konto erstellt, z. B. haben *Westus*.
    - **Ressource** – die maschinelles sehen-Ressource, die Sie wie z. B. Aufrufen `analyze`, `describe`, `generateThumbnail`, `ocr`, `models`, `recognizeText`, `tag`.

    Sie können das Bild, das verarbeitet werden, entweder als eine Binärdatei raw-Image oder eine Bild-URL angeben.

    Der Anforderungsheader muss den Abonnementschlüssel enthalten, der Zugriff auf diese API ermöglicht.

1. Analyse der Antwort

    Die Antwort enthält die Erkenntnis, die das Computer Vision-API zu Ihrem Bild als eine JSON-Nutzlast musste.

Angenommen, Sie Abonnement in der maschinelles sehen erstellt die `westus` Region und einen Abonnementschlüssel, auf die API zugreifen. Probieren Sie der Taste fiktiven Wert `xxxx-xxxxx-xxxx-xxxx`. Jetzt möchten Sie eine Miniaturansicht zu generieren, wenn ein Bild im Pfad `http://example.com/images/test.jpg`. Mithilfe von `generateThumbnail`, würde die Anforderung wie folgt aussehen.

```
curl POST "https://westus2.api.cognitive.microsoft.com/vision/v2.0/generateThumbnail
-H "Content-Type: application/json"
-H "Ocp-Apim-Subscription-Key: {xxxx-xxxxx-xxxx-xxxx}"
-d "{'url':'http://example.com/images/test.jpg'}"
```

In diesem Modul werden wir alle Übungen in der Azure-Befehlszeilenschnittstelle ausführen, mithilfe der integrierten Cloud-Shell. Wir wollen nun etwas mehr Informationen zu diesem Setup.

## <a name="what-is-the-azure-cli"></a>Was ist der Azure-Befehlszeilenschnittstelle

Die Azure CLI ist das plattformübergreifende Befehlszeilentool von Microsoft zum Verwalten von Azure-Ressourcen. Sie steht für macOS, Linux und Windows sowie unter Verwendung von [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) im Browser zur Verfügung.

> [!IMPORTANT]
> Es gibt aktuell zwei Versionen der Azure CLI: Azure CLI 1.0 und Azure CLI 2.0. Wir verwenden hier die neueste Version, Azure CLI 2.0, die empfohlen wird, außer wenn Sie ältere Skripts ausführen. Die Azure CLI 1.0 wird mit dem Befehl „`azure`“ gestartet, die Azure CLI 2.0 mit dem Befehl „`az`“.

## <a name="az-cognitiveservices-commands"></a>AZ Cognitiveservices-Befehlen

Die Azure CLI enthält die `cognitiveservices` Befehl aus, um die Cognitive Services-Konten in Azure zu verwalten. Wir können verschiedene Unterbefehle bereitstellen, um bestimmte Aufgaben auszuführen. Dies sind die am häufigsten verwendeten:

| Unterbefehl | Beschreibung |
|-------------|-------------|
| `list` | Listet die verfügbare Azure Cognitive Services-Konten. |
| `account show` | Rufen Sie die Details eines Azure Cognitive Services-Kontos. |
| `account create` | Erstellen eines Azure Cognitive Services-Kontos an. |
| `account delete` | Löschen eines Azure Cognitive Services-Kontos. |
| `keys list` | Listet die Schlüssel eines Azure Cognitive Services-Kontos an. |

Erstellen Sie ein Cognitive Services wir mit der Azure CLI.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-cognitive-services-account"></a>Erstellen Sie ein Cognitive Services-Konto.

Wir benötigen einen API-Zugriffsschlüssel für das Computer Vision-API aufrufen. Um Zugriffstasten zu erhalten, benötigen wir ein Cognitive Services-Konto an, für die Computer Vision-API. Wir verwenden `az cognitiveservices create` um das Konto in unserem Abonnement zu erstellen.

 Der Befehl `az cognitiveservices create` wird verwendet, um ein Cognitive Services-Konto in einer Ressourcengruppe zu erstellen.  Die folgenden fünf Parameter müssen angegeben werden, beim Aufrufen dieses Befehls.

> [!Tip]
> Die meisten Flags für das Azure-CLI-Parameter können in ein einzelnes Zeichen abgekürzt werden. Angenommen, wir könnten sagen `-l` anstelle von `--location`. Die lange Form wird aus Gründen der Übersichtlichkeit verwendet.

| Parameter | Beschreibung |
|-----------|-------------|
| `resource-group` | Die Ressourcengruppe, die die cognitive Services-Konto besitzen soll. Verwenden Sie in dieser Sitzung interaktive Sandbox <rgn>[Sandkasten Resource Group-Name]</rgn> |
| `kind` | Der Name der API der cognitive Services-Konto. |
| `location` | Der Speicherort oder die Region, von dem auf diese API-Aufrufe werden sollen. |
| `name` | Cognitive Services-Kontonamen. |
| `sku` | Die Sku des cognitive Services-Konto.|

1. Führen Sie in Azure Cloud Shell folgenden Befehl aus:

> [!Tip]
> Azure CLI-Befehle in diesem Modul werden als mehrzeilige Befehle aus, um den horizontalen Bildlauf zu reduzieren, geschrieben. Sie können diese Befehle für einzeilige Befehle konvertieren, wenn Sie möchten. 

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)] 

```azurecli
az cognitiveservices account create \
--kind ComputerVision \
--location westus2 \
--name ComputerVisionService \
--sku F0 \
--resource-group <rgn>[Sandbox resource group name]</rgn>
```

Hier erstellt es ein cognitive Services-Konto für die **ComputerVision** API. Wir haben uns für die SKU "free" *F0* und mit dem Namen unser Kontos **ComputerVisionService**. Das Konto ist im Besitz der Ressourcengruppe **<rgn>[Ressourcengruppennamen Sandkasten]</rgn>** und wir rufen die API, von dem Speicherort, die wir auf die `--location` Parameter. In diesem Beispiel werden darf, Aufrufe von westus2. Aufrufe von einer beliebigen anderen Region wird zu einem Fehler führen.

Nach Abschluss des Befehls, die cognitive Services-Konto erstellen, erhalten Sie eine JSON-Antwort, einschließlich **ProvisioningState** -Eigenschaftensatz auf **erfolgreich**. Hier ist ein Beispiel für eine erfolgreiche Antwort aussieht.

<!-- TODO: find out the default location! -->

```json
{
  "endpoint": "https://westus2.api.cognitive.microsoft.com/vision/v2.0",
  "etag": "\"5c0070e5-0000-0000-0000-5b98cafa0000\"",
  "id": "/subscriptions/ae49d8aa-de86-418a-ba8c-4e9f3add2620/resourceGroups/ComputerVisionRG/providers/Microsoft.CognitiveServices/accounts/ComputerVisionService",
  "internalId": "437c9519bead47e6ba4b8e0842c1f76f",
  "kind": "ComputerVision",
  "location": "westus2",
  "name": "ComputerVisionService",
  "provisioningState": "Succeeded",
  "resourceGroup": "ComputerVisionRG",
  "sku": {
    "name": "F0",
    "tier": null
  },
  "tags": null,
  "type": "Microsoft.CognitiveServices/accounts"
}
```

> [!NOTE]
> Wenn es sich bei Ihrem Azure-Abonnement bereits einen Computer Vision cognitive Services-Konto eingerichtet wurde die **F0** Sku, bevor Sie diesen Befehl ausführen, sehen Sie die folgende Meldung:
>
> `Only one free account is allowed for account type 'ComputerVision'` 
>
> Sie verwenden dieses Konto für dieses Modul oder ändern Sie die Sku in der `az cognitiveservices account create` Befehl *S1* oder einer anderen Sku.

## <a name="get-an-access-key"></a>Abrufen eines Zugriffsschlüssels

Sobald wir unsere Konto erfolgreich erstellt haben können, wir die Abonnementschlüssel abrufen oder Zugriffsschlüssel für dieses Konto.

1. Führen Sie in Azure Cloud Shell folgenden Befehl aus:

```azurecli
az cognitiveservices account keys list \
--name ComputerVisionService \
--resource-group <rgn>[Sandbox resource group name]</rgn>
```

Der obige Befehl gibt die wird aufgerufen, die cognitive Services-Konto zugeordneten Schlüssel **ComputerVisionService**, deren Besitzer der angegebenen Ressourcengruppe. Es gibt zwei Schlüssel: einer ist ein spare-Schlüssel. Die Schlüssel sind schwer zu merken, damit wir den ersten Schlüssel in einer Variablen speichern müssen, die wir für alle Aufrufe der API verwenden.

2.  Führen Sie in Azure Cloud Shell folgenden Befehl aus:

```azurecli
key=$(az cognitiveservices account keys list \
--name ComputerVisionService \
--resource-group <rgn>[Sandbox resource group name]</rgn> \
--query key1 -o tsv)
```

Der Azure CLI 2.0 verwendet die `--query` Argument für eine JMESPath-Abfrage auf die Ergebnisse von Befehlen auszuführen. JMESPath ist eine Abfragesprache für JSON, die es ermöglicht, Daten aus der CLI-Ausgabe auszuwählen und zu präsentieren. Diese Abfragen werden in der JSON-Ausgabe vor jedem anzeigeformatierung ausgeführt.
Das Argument `--query` wird von allen Befehlen der Azure-Befehlszeilenschnittstelle unterstützt. 

In unserem Beispiel wir zum Abfragen der Liste der Schlüssel für einen Eintrag mit dem Namen "key1" und das Ergebnis **Tsv** Format. Dieses Format wird entfernt, Angebote, um den Zeichenfolgenwert. Wir weisen das Ergebnis einer Variablen **Schlüssel**.

> [!IMPORTANT]
> Wir werden diesen Schlüssel während des gesamten im Modul verwenden, also in einer Variablen speichern eine gute Idee. Wenn Sie den Wert verlieren oder die Variable nicht festgelegt wird, führen Sie den Befehl erneut aus, um es festgelegt.  

3. Um den Wert für unsere Schlüssel anzuzeigen, führen Sie den folgenden Befehl in Azure Cloud Shell aus:

```azurecli
echo $key
```

Nun, wir ein Konto und einen Schlüssel haben, ist es Zeit, einige der API-Aufrufe.