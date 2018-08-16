Nachdem eine VM erstellt wurde, können wir Informationen über andere Befehle abrufen.

Beginnen wir mit `vm list`.

```azurecli
az vm list
```

Dieser Befehl gibt _alle_ virtuelle Computer, die in diesem Abonnement definiert. Die Ausgabe gefiltert werden kann, um eine bestimmte Ressourcengruppe über das `--resource-group` Parameter. 

## <a name="output-types"></a>Ausgabetypen
Beachten Sie, dass der Standardtyp für die Antwort für alle Befehle, die bis jetzt wir haben JSON ist. Dies eignet sich hervorragend für scripting –, aber die meisten Personen finden es schwieriger zu lesen. Sie können den Ausgabe-Stil für alle Antworten durch Ändern der `--output` Flag. Versuchen Sie z. B. den folgenden Befehl in Cloud Shell den Stil für die andere Ausgabe angezeigt.

```azurecli
az vm list --output table
```

Zusammen mit `table`, können Sie angeben, `json` (Standardeinstellung), `jsonc` (Farbiger JSON-Code), oder `tsv` (Table-Separated Werte). Versuchen Sie es einige Varianten mit der oben genannten Befehl aus, um den Unterschied zu sehen.

## <a name="getting-the-ip-address"></a>Die IP-Adresse

Eine andere nützliche Befehl `vm list-ip-addresses`, die werden die öffentlichen und privaten IP-Adressen für einen virtuellen Computer aufgelistet. Wenn sie ändern oder Sie nicht diese erfassen, während der Erstellung können Sie sie zu einem beliebigen Zeitpunkt abrufen.

```azurecli
az vm list-ip-addresses -n SampleVM -o table
```

Gibt Folgendes zurück:

```
VirtualMachine    PublicIPAddresses    PrivateIPAddresses
----------------  -------------------  --------------------
SampleVM          168.61.54.62         10.0.0.4
```

> [!NOTE]
> Beachten Sie, dass die Verwendung von Kurzsyntax für die `--output` kennzeichnen als `-o`. Die meisten Parameter für Azure CLI-Befehlen können es sich um Shortend auf eine einzelne Gedankenstriche und der Buchstabe sein. Z. B. `--name` verkürzt werden kann, um `-n` und `--resource-group` zu `-g`. Dies ist praktisch für die Eingabe, aber es wird empfohlen, den Namen der Option "vollständig" aus Gründen der Übersichtlichkeit in Skripts verwenden. Überprüfen Sie die Dokumentation für die Details zu den einzelnen Befehlen.

## <a name="getting-vm-details"></a>Abrufen von Details zum virtuellen Computer

Wir können weitere ausführliche Informationen zu einem bestimmten virtuellen Computer nach Name oder Id mithilfe der `vm show` Befehl.

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM
```

Dadurch wird einen ziemlich großen JSON-Block mit unterschiedlichsten Informationen zu den virtuellen Computer, einschließlich NAS-Geräte, Netzwerkschnittstellen und alle der Objekt-IDs für Ressourcen, denen mit der virtuellen Computer verbunden ist, zurückgegeben. In diesem Fall wir können in einem Tabellenformat ändern, aber der, die fast alle relevanten Daten. Stattdessen können Sie sich nun um eine integrierte Abfragesprache für JSON aufgerufen [JMESPath](http://jmespath.org/).

## <a name="adding-filters-to-queries-with-jmespath"></a>Hinzufügen von Filtern zu Abfragen mit JMESPath

JMESPath ist eine Abfragesprache nach Industriestandard so konzipiert, JSON-Objekte. Die einfachste Abfrage wird an eine _Bezeichner_ , der einen Schlüssel im JSON-Objekt auswählt.

Angenommen, das Objekt:

```json
{
  "people": [
    {
      "name": "Fred",
      "age": 28
    },
    {
      "name": "Barney",
      "age": 25
    },
    {
      "name": "Wilma",
      "age": 27
    }
  ]
}
```

Wir können die Abfrage `people` zurückzugebenden das Array von Werten für die `people` Array. Wenn wir wollen da _eine_ der Personen, wir können einen Indexer verwenden: z. B. `people[1]` zurück:

```json
{
    "name": "Barney",
    "age": 25
}
```

Wir können auch hinzufügen, bestimmte Qualifizierer, der zurückgegeben würde nur die `Fred` und `Wilma` Objekte. 

```json
[
  {
    "name": "Fred",
    "age": 28
  },
  {
    "name": "Wilma",
    "age": 27
  }
]
```

Schließlich können wir die Ergebnisse eingeschränkt werden durch eine SELECT-Anweisung hinzufügen: `people[?age > '25'].[name]` , die nur die Namen zurückgibt:

```json
[
  [
    "Fred"
  ],
  [
    "Wilma"
  ]
]
```

JMESQuery verfügt über mehrere andere interessante Abfragefeatures. Wenn Sie Zeit haben, sehen Sie sich die [Onlinelernprogramm](http://jmespath.org/tutorial.html) auf der [JMESPath.org](http://jmespath.org/) Standort.

## <a name="filtering-our-azure-cli-queries"></a>Filtern von unseren Azure-Befehlszeilenschnittstelle Abfragen

Grundlegende Kenntnisse zu JMES Abfragen, können wir Speichereinheiten hinzufügen, auf die Daten, die zurückgegeben wird, von Abfragen wie die `vm show` Befehl. Beispielsweise können wir den Namen des Administratorbenutzers abrufen:

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "osProfile.adminUsername"
```

Wir können die Größe, die an den virtuellen Computer zugewiesen:

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query hardwareProfile.vmSize
```

Oder um alle für die Netzwerkschnittstellen-IDs abzurufen, können Sie die Abfrage verwenden:

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "networkProfile.networkInterfaces[].id"
```

Dieses Verfahren für die Abfrage funktioniert mit jedem Azure-CLI-Befehl und kann zum Abrufen von bestimmten Bits der Daten in der Befehlszeile verwendet werden. Es ist hilfreich für die Skripterstellung als auch – Sie können z. B. einen Wert aus Ihrem Azure-Konto abrufen und in einer Umgebung oder ein Skript-Variable zu speichern. Wenn Sie es auf diese Weise verwenden möchten, ist ein nützliches Flag Hinzufügen der `--output tsv` Parameter (die kann in der Kurzform `-o tsv`). Dadurch wird die Ergebnisse in per Tabulator getrennte Werte zurückgegeben, die nur die tatsächlichen Datenwerte mit Registerkarte Trennzeichen enthalten.

Als Beispiel

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "networkProfile.networkInterfaces[].id" -o tsv
```

Gibt den Text zurück: `/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Network/networkInterfaces/SampleVMVMNic`
