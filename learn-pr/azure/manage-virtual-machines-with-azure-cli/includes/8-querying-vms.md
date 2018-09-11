Nachdem der virtuelle Computer erstellt wurde, können wir über andere Befehle Informationen über ihn erhalten.

Beginnen wir mit `vm list`.

```azurecli
az vm list
```

Dieser Befehl gibt _alle_ virtuelle Computer zurück, die in diesem Abonnement definiert sind. Die Ausgabe kann über den Parameter `--resource-group` auf eine bestimmte Ressourcengruppe gefiltert werden. 

## <a name="output-types"></a>Ausgabetypen
Beachten Sie, dass der Standardantworttyp für alle Befehle, die wir bisher ausgeführt haben, JSON ist. Das ist gut für die Skripterstellung, aber die meisten finden es schwerer zu lesen. Sie können den Ausgabestil für jede Antwort mit dem Flag `--output` ändern. Probieren Sie beispielsweise den folgenden Befehl in Azure Cloud Shell aus, um den anderen Ausgabestil anzuzeigen.

```azurecli
az vm list --output table
```

Neben `table` können Sie `json` (Standard), `jsonc` (farbiger JSON-Code) oder `tsv` (durch Tabulatoren getrennte Werte) angeben. Probieren Sie einige Varianten mit dem oben genannten Befehl aus, um den Unterschied zu sehen.

## <a name="getting-the-ip-address"></a>Abrufen der IP-Adresse

Eine andere nützlicher Befehl ist `vm list-ip-addresses`, mit dem die öffentlichen und privaten IP-Adressen eines virtuellen Computers aufgelistet werden. Wenn sie sich ändern oder Sie sie während der Erstellung nicht erfasst haben, können Sie sie jederzeit abrufen.

```azurecli
az vm list-ip-addresses -n SampleVM -o table
```

Dadurch wird Folgendes zurückgegeben:

```
VirtualMachine    PublicIPAddresses    PrivateIPAddresses
----------------  -------------------  --------------------
SampleVM          168.61.54.62         10.0.0.4
```

> [!TIP]
> Beachten Sie, dass wir eine Kurzsyntax für das Flag `--output` als `-o` verwenden. Die meisten Parameter von Azure CLI-Befehlen können auf einen einzigen Bindestrich und Buchstaben verkürzt werden. `--name` kann beispielsweise zu `-n` und `--resource-group` zu `-g` verkürzt werden. Dies ist praktisch für die Eingabe, aber wir empfehlen aus Gründen der Übersichtlichkeit, in Skripts den vollständigen Namen der Option zu verwenden. Weitere Informationen zu den einzelnen Befehlen finden Sie in der Dokumentation.

## <a name="getting-vm-details"></a>Abrufen von VM-Details

Mit dem Befehl `vm show` können wir detailliertere Informationen zu einem bestimmten virtuellen Computer nach Name oder ID abrufen.

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM
```

Dies gibt einen recht großen JSON-Block mit allen möglichen Informationen zur VM zurück. Dazu gehören angeschlossene Speichergeräte, Netzwerkschnittstellen und alle Objekt-IDs für Ressourcen, mit denen die VM verbunden ist. Auch hier könnten wir zu einem Tabellenformat wechseln, aber dabei entfallen nahezu alle interessanten Daten. Stattdessen können wir auf eine integrierte Abfragesprache für JSON mit dem Namen [JMESPath](http://jmespath.org/) zurückgreifen.

## <a name="adding-filters-to-queries-with-jmespath"></a>Hinzufügen von Filtern zu Abfragen mit JMESPath

JMESPath ist eine branchenübliche Abfragesprache, die auf JSON-Objekten basiert. Die einfachste Abfrage ist die Angabe eines _Bezeichners_, der einen Schlüssel im JSON-Objekt auswählt.

Betrachten wir beispielsweise das Objekt:

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

Wir können die Abfrage `people` verwenden, um das Array der Werte für das Array `people` zurückzugeben. Wenn wir nur _eine_ der Personen wünschen, können wir einen Indexer verwenden. `people[1]` würde z.B. Folgendes zurückgeben:

```json
{
    "name": "Barney",
    "age": 25
}
```

Wir können auch bestimmte Qualifizierer hinzufügen, die auf der Grundlage einiger Kriterien eine Teilmenge der Objekte zurückgeben würden. Das Hinzufügen des `people[?age > '25']`-Qualifizierers würde beispielsweise Folgendes zurückgeben:

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

Zum Schluss können wir die Ergebnisse durch Hinzufügen einer Auswahl (`people[?age > '25'].[name]`) einschränken, die nur die Namen zurückgibt:

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

JMESQuery bietet mehrere andere interessante Abfragefunktionen. Wenn Sie Zeit haben, sehen Sie sich das [Onlinetutorial](http://jmespath.org/tutorial.html) auf der Website [JMESPath.org](http://jmespath.org/) an.

## <a name="filtering-our-azure-cli-queries"></a>Filtern unserer Azure CLI-Abfragen

Mit einem grundlegenden Verständnis von JMES-Abfragen können wir den Daten Filer hinzufügen, die von Abfragen wie dem `vm show`-Befehl zurückgegeben werden. Zum Beispiel können wir den Benutzernamen des Administrators abrufen:

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "osProfile.adminUsername"
```

Wir können die Größe bestimmen, die unserer VM zugewiesen wird:

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query hardwareProfile.vmSize
```

Oder um alle IDs Ihrer Netzwerkschnittstellen abzurufen, können Sie diese Abfrage verwenden:

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "networkProfile.networkInterfaces[].id"
```

Diese Abfragetechnik funktioniert mit jedem Azure CLI-Befehl und kann verwendet werden, um bestimmte Daten über die Befehlszeile abzurufen. Sie ist auch für die Skripterstellung nützlich, denn Sie können z.B. einen Wert aus Ihrem Azure-Account abrufen und in einer Umgebungs- oder Skriptvariablen speichern. Wenn Sie sich entscheiden, sie auf diese Weise zu verwenden, ist der Parameter `--output tsv` (der auf `-o tsv` verkürzt werden kann) ein nützliches Flag, das hinzugefügt werden muss. Dadurch werden die Ergebnisse in mit Tabulatoren getrennten Werten zurückgegeben, die nur die tatsächlichen Datenwerte mit Tabulatortrennzeichen enthalten.

Beispiel:

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "networkProfile.networkInterfaces[].id" -o tsv
```

gibt diesen Text zurück: `/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Network/networkInterfaces/SampleVMVMNic`
