<span data-ttu-id="4f1b6-101">Nachdem der virtuelle Computer erstellt wurde, können wir über andere Befehle Informationen über ihn erhalten.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-101">Now that a virtual machine has been created, we can get information about it through other commands.</span></span>

<span data-ttu-id="4f1b6-102">Beginnen wir mit `vm list`.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-102">Let's start with `vm list`.</span></span>

```azurecli
az vm list
```

<span data-ttu-id="4f1b6-103">Dieser Befehl gibt _alle_ virtuelle Computer zurück, die in diesem Abonnement definiert sind.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-103">This command will return _all_ virtual machines defined in this subscription.</span></span> <span data-ttu-id="4f1b6-104">Die Ausgabe kann über den Parameter `--resource-group` auf eine bestimmte Ressourcengruppe gefiltert werden.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-104">The output can be filtered to a specific resource group through the `--resource-group` parameter.</span></span> 

## <a name="output-types"></a><span data-ttu-id="4f1b6-105">Ausgabetypen</span><span class="sxs-lookup"><span data-stu-id="4f1b6-105">Output types</span></span>
<span data-ttu-id="4f1b6-106">Beachten Sie, dass der Standardantworttyp für alle Befehle, die wir bisher ausgeführt haben, JSON ist.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-106">Notice that the default response type for all the commands we've done so far is JSON.</span></span> <span data-ttu-id="4f1b6-107">Das ist gut für die Skripterstellung, aber die meisten finden es schwerer zu lesen.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-107">This is great for scripting - but most people find it harder to read.</span></span> <span data-ttu-id="4f1b6-108">Sie können den Ausgabestil für jede Antwort mit dem Flag `--output` ändern.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-108">You can change the output style for any response through the `--output` flag.</span></span> <span data-ttu-id="4f1b6-109">Probieren Sie beispielsweise den folgenden Befehl in Azure Cloud Shell aus, um den anderen Ausgabestil anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-109">For example, try the following command in Azure Cloud Shell to see the different output style.</span></span>

```azurecli
az vm list --output table
```

<span data-ttu-id="4f1b6-110">Neben `table` können Sie `json` (Standard), `jsonc` (farbiger JSON-Code) oder `tsv` (durch Tabulatoren getrennte Werte) angeben.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-110">Along with `table`, you can specify `json` (the default), `jsonc` (colorized JSON), or `tsv` (Table-Separated Values).</span></span> <span data-ttu-id="4f1b6-111">Probieren Sie einige Varianten mit dem oben genannten Befehl aus, um den Unterschied zu sehen.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-111">Try a few variations with the above command to see the difference.</span></span>

## <a name="getting-the-ip-address"></a><span data-ttu-id="4f1b6-112">Abrufen der IP-Adresse</span><span class="sxs-lookup"><span data-stu-id="4f1b6-112">Getting the IP address</span></span>

<span data-ttu-id="4f1b6-113">Eine andere nützlicher Befehl ist `vm list-ip-addresses`, mit dem die öffentlichen und privaten IP-Adressen eines virtuellen Computers aufgelistet werden.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-113">Another useful command is `vm list-ip-addresses`, which will list the public and private IP addresses for a VM.</span></span> <span data-ttu-id="4f1b6-114">Wenn sie sich ändern oder Sie sie während der Erstellung nicht erfasst haben, können Sie sie jederzeit abrufen.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-114">If they change, or you didn't capture them during creation, you can retrieve them at any time.</span></span>

```azurecli
az vm list-ip-addresses -n SampleVM -o table
```

<span data-ttu-id="4f1b6-115">Gibt Folgendes zurück:</span><span class="sxs-lookup"><span data-stu-id="4f1b6-115">This returns:</span></span>

```
VirtualMachine    PublicIPAddresses    PrivateIPAddresses
----------------  -------------------  --------------------
SampleVM          168.61.54.62         10.0.0.4
```

> [!NOTE]
> <span data-ttu-id="4f1b6-116">Beachten Sie, dass wir eine Kurzsyntax für das Flag `--output` als `-o` verwenden.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-116">Notice that we are using a shorthand syntax for the `--output` flag as `-o`.</span></span> <span data-ttu-id="4f1b6-117">Die meisten Parameter von Azure CLI-Befehlen können auf einen einzigen Bindestrich und Buchstaben verkürzt werden.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-117">Most parameters to Azure CLI commands can be shortened to a single dash and letter.</span></span> <span data-ttu-id="4f1b6-118">`--name` kann beispielsweise zu `-n` und `--resource-group` zu `-g` verkürzt werden.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-118">For example, `--name` can be shortened to `-n` and `--resource-group` to `-g`.</span></span> <span data-ttu-id="4f1b6-119">Dies ist praktisch für die Eingabe, aber wir empfehlen aus Gründen der Übersichtlichkeit, in Skripts den vollständigen Namen der Option zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-119">This is handy for typing, but we recommend using the full option name in scripts for clarity.</span></span> <span data-ttu-id="4f1b6-120">Weitere Informationen zu den einzelnen Befehlen finden Sie in der Dokumentation.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-120">Check the documentation for details on each command.</span></span>

## <a name="getting-vm-details"></a><span data-ttu-id="4f1b6-121">Abrufen von VM-Details</span><span class="sxs-lookup"><span data-stu-id="4f1b6-121">Getting VM details</span></span>

<span data-ttu-id="4f1b6-122">Mit dem Befehl `vm show` können wir detailliertere Informationen zu einem bestimmten virtuellen Computer nach Name oder ID abrufen.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-122">We can get more detailed information about a specific virtual machine by name or ID using the `vm show` command.</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM
```

<span data-ttu-id="4f1b6-123">Dies gibt einen recht großen JSON-Block mit allen möglichen Informationen zur VM zurück. Dazu gehören angeschlossene Speichergeräte, Netzwerkschnittstellen und alle Objekt-IDs für Ressourcen, mit denen die VM verbunden ist.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-123">This will return a fairly large JSON block with all sorts of information about the VM, including attached storage devices, network interfaces, and all of the object IDs for resources that the VM is connected to.</span></span> <span data-ttu-id="4f1b6-124">Auch hier könnten wir zu einem Tabellenformat wechseln, aber dabei entfallen nahezu alle interessanten Daten.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-124">Again, we could change to a table format, but that omits almost all of the interesting data.</span></span> <span data-ttu-id="4f1b6-125">Stattdessen können wir auf eine integrierte Abfragesprache für JSON mit dem Namen [JMESPath](http://jmespath.org/) zurückgreifen.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-125">Instead, we can turn to a built-in query language for JSON called [JMESPath](http://jmespath.org/).</span></span>

## <a name="adding-filters-to-queries-with-jmespath"></a><span data-ttu-id="4f1b6-126">Hinzufügen von Filtern zu Abfragen mit JMESPath</span><span class="sxs-lookup"><span data-stu-id="4f1b6-126">Adding filters to queries with JMESPath</span></span>

<span data-ttu-id="4f1b6-127">JMESPath ist eine branchenübliche Abfragesprache, die auf JSON-Objekten basiert.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-127">JMESPath is an industry-standard query language built around JSON objects.</span></span> <span data-ttu-id="4f1b6-128">Die einfachste Abfrage ist die Angabe eines _Bezeichners_, der einen Schlüssel im JSON-Objekt auswählt.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-128">The simplest query is to specify an _identifier_ that selects a key in the JSON object.</span></span>

<span data-ttu-id="4f1b6-129">Betrachten wir beispielsweise das Objekt:</span><span class="sxs-lookup"><span data-stu-id="4f1b6-129">For example, given the object:</span></span>

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

<span data-ttu-id="4f1b6-130">Wir können die Abfrage `people` verwenden, um das Array der Werte für das Array `people` zurückzugeben.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-130">We can use the query `people` to return the array of values for the `people` array.</span></span> <span data-ttu-id="4f1b6-131">Wenn wir nur _eine_ der Personen wünschen, können wir einen Indexer verwenden.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-131">If we just want _one_ of the people, we can use an indexer.</span></span> <span data-ttu-id="4f1b6-132">`people[1]` würde z.B. Folgendes zurückgeben:</span><span class="sxs-lookup"><span data-stu-id="4f1b6-132">For example, `people[1]` would return:</span></span>

```json
{
    "name": "Barney",
    "age": 25
}
```

<span data-ttu-id="4f1b6-133">Wir können auch spezifische Qualifizierer hinzufügen, die nur die Objekte `Fred` und `Wilma` zurückgeben würden.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-133">We can also add specific qualifiers that would return just the `Fred` and `Wilma` objects.</span></span> 

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

<span data-ttu-id="4f1b6-134">Schließlich können wir die Ergebnisse durch Hinzufügen einer Auswahl (`people[?age > '25'].[name]`) einschränken, die nur die Namen zurückgibt:</span><span class="sxs-lookup"><span data-stu-id="4f1b6-134">Finally, we can constrain the results by adding a select: `people[?age > '25'].[name]` that returns just the names:</span></span>

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

<span data-ttu-id="4f1b6-135">JMESQuery bietet mehrere andere interessante Abfragefunktionen.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-135">JMESQuery has several other interesting query features.</span></span> <span data-ttu-id="4f1b6-136">Wenn Sie Zeit haben, sehen Sie sich das [Onlinetutorial](http://jmespath.org/tutorial.html) auf der Website [JMESPath.org](http://jmespath.org/) an.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-136">When you have time, check out the [online tutorial](http://jmespath.org/tutorial.html) available on the [JMESPath.org](http://jmespath.org/) site.</span></span>

## <a name="filtering-our-azure-cli-queries"></a><span data-ttu-id="4f1b6-137">Filtern unserer Azure CLI-Abfragen</span><span class="sxs-lookup"><span data-stu-id="4f1b6-137">Filtering our Azure CLI queries</span></span>

<span data-ttu-id="4f1b6-138">Mit einem grundlegenden Verständnis von JMES-Abfragen können wir den Daten Filer hinzufügen, die von Abfragen wie dem `vm show`-Befehl zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-138">With a basic understanding of JMES queries, we can add filers to the data being returned by queries like the `vm show` command.</span></span> <span data-ttu-id="4f1b6-139">Zum Beispiel können wir den Benutzernamen des Administrators abrufen:</span><span class="sxs-lookup"><span data-stu-id="4f1b6-139">For example, we can retrieve the admin user name:</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "osProfile.adminUsername"
```

<span data-ttu-id="4f1b6-140">Wir können die Größe bestimmen, die unserer VM zugewiesen wird:</span><span class="sxs-lookup"><span data-stu-id="4f1b6-140">We can get the size assigned to our VM:</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query hardwareProfile.vmSize
```

<span data-ttu-id="4f1b6-141">Oder um alle IDs Ihrer Netzwerkschnittstellen abzurufen, können Sie diese Abfrage verwenden:</span><span class="sxs-lookup"><span data-stu-id="4f1b6-141">Or to retrieve all the IDs for your network interfaces, you can use the query:</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "networkProfile.networkInterfaces[].id"
```

<span data-ttu-id="4f1b6-142">Diese Abfragetechnik funktioniert mit jedem Azure CLI-Befehl und kann verwendet werden, um bestimmte Daten über die Befehlszeile abzurufen.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-142">This query technique will work with any Azure CLI command and can be used to pull specific bits of data out on the command line.</span></span> <span data-ttu-id="4f1b6-143">Sie ist auch für die Skripterstellung nützlich, denn Sie können z.B. einen Wert aus Ihrem Azure-Account abrufen und in einer Umgebungs- oder Skriptvariablen speichern.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-143">It is useful for scripting as well - for example, you can pull a value out of your Azure account and store it in an environment or script variable.</span></span> <span data-ttu-id="4f1b6-144">Wenn Sie sich entscheiden, sie auf diese Weise zu verwenden, ist der Parameter `--output tsv` (der auf `-o tsv` verkürzt werden kann) ein nützliches Flag, das hinzugefügt werden muss.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-144">If you decide to use it this way, a useful flag to add is the `--output tsv` parameter (which can be shortened to `-o tsv`).</span></span> <span data-ttu-id="4f1b6-145">Dadurch werden die Ergebnisse in mit Tabulatoren getrennten Werten zurückgegeben, die nur die tatsächlichen Datenwerte mit Tabulatortrennzeichen enthalten.</span><span class="sxs-lookup"><span data-stu-id="4f1b6-145">This will return the results in tab-separated values that only include the actual data values with tab separators.</span></span>

<span data-ttu-id="4f1b6-146">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="4f1b6-146">As an example,</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "networkProfile.networkInterfaces[].id" -o tsv
```

<span data-ttu-id="4f1b6-147">gibt diesen Text zurück: `/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Network/networkInterfaces/SampleVMVMNic`</span><span class="sxs-lookup"><span data-stu-id="4f1b6-147">returns the text: `/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Network/networkInterfaces/SampleVMVMNic`</span></span>
