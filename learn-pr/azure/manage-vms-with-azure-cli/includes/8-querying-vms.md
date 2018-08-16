<span data-ttu-id="1814a-101">Nachdem eine VM erstellt wurde, können wir Informationen über andere Befehle abrufen.</span><span class="sxs-lookup"><span data-stu-id="1814a-101">Now that a virtual machine has been created, we can get information about it through other commands.</span></span>

<span data-ttu-id="1814a-102">Beginnen wir mit `vm list`.</span><span class="sxs-lookup"><span data-stu-id="1814a-102">Let's start with `vm list`.</span></span>

```azurecli
az vm list
```

<span data-ttu-id="1814a-103">Dieser Befehl gibt _alle_ virtuelle Computer, die in diesem Abonnement definiert.</span><span class="sxs-lookup"><span data-stu-id="1814a-103">This command will return _all_ virtual machines defined in this subscription.</span></span> <span data-ttu-id="1814a-104">Die Ausgabe gefiltert werden kann, um eine bestimmte Ressourcengruppe über das `--resource-group` Parameter.</span><span class="sxs-lookup"><span data-stu-id="1814a-104">The output can be filtered to a specific resource group through the `--resource-group` parameter.</span></span> 

## <a name="output-types"></a><span data-ttu-id="1814a-105">Ausgabetypen</span><span class="sxs-lookup"><span data-stu-id="1814a-105">Output types</span></span>
<span data-ttu-id="1814a-106">Beachten Sie, dass der Standardtyp für die Antwort für alle Befehle, die bis jetzt wir haben JSON ist.</span><span class="sxs-lookup"><span data-stu-id="1814a-106">Notice that the default response type for all the commands we've done so far is JSON.</span></span> <span data-ttu-id="1814a-107">Dies eignet sich hervorragend für scripting –, aber die meisten Personen finden es schwieriger zu lesen.</span><span class="sxs-lookup"><span data-stu-id="1814a-107">This is great for scripting - but most people find it harder to read.</span></span> <span data-ttu-id="1814a-108">Sie können den Ausgabe-Stil für alle Antworten durch Ändern der `--output` Flag.</span><span class="sxs-lookup"><span data-stu-id="1814a-108">You can change the output style for any response through the `--output` flag.</span></span> <span data-ttu-id="1814a-109">Versuchen Sie z. B. den folgenden Befehl in Cloud Shell den Stil für die andere Ausgabe angezeigt.</span><span class="sxs-lookup"><span data-stu-id="1814a-109">For example, try the following command in the Cloud Shell to see the different output style.</span></span>

```azurecli
az vm list --output table
```

<span data-ttu-id="1814a-110">Zusammen mit `table`, können Sie angeben, `json` (Standardeinstellung), `jsonc` (Farbiger JSON-Code), oder `tsv` (Table-Separated Werte).</span><span class="sxs-lookup"><span data-stu-id="1814a-110">Along with `table`, you can specify `json` (the default), `jsonc` (colorized JSON), or `tsv` (Table-Separated Values).</span></span> <span data-ttu-id="1814a-111">Versuchen Sie es einige Varianten mit der oben genannten Befehl aus, um den Unterschied zu sehen.</span><span class="sxs-lookup"><span data-stu-id="1814a-111">Try a few variations with the above command to see the difference.</span></span>

## <a name="getting-the-ip-address"></a><span data-ttu-id="1814a-112">Die IP-Adresse</span><span class="sxs-lookup"><span data-stu-id="1814a-112">Getting the IP address</span></span>

<span data-ttu-id="1814a-113">Eine andere nützliche Befehl `vm list-ip-addresses`, die werden die öffentlichen und privaten IP-Adressen für einen virtuellen Computer aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="1814a-113">Another useful command is `vm list-ip-addresses`, which will list the public and private IP addresses for a VM.</span></span> <span data-ttu-id="1814a-114">Wenn sie ändern oder Sie nicht diese erfassen, während der Erstellung können Sie sie zu einem beliebigen Zeitpunkt abrufen.</span><span class="sxs-lookup"><span data-stu-id="1814a-114">If they change, or you didn't capture them during creation you can retrieve them at any time.</span></span>

```azurecli
az vm list-ip-addresses -n SampleVM -o table
```

<span data-ttu-id="1814a-115">Gibt Folgendes zurück:</span><span class="sxs-lookup"><span data-stu-id="1814a-115">This returns:</span></span>

```
VirtualMachine    PublicIPAddresses    PrivateIPAddresses
----------------  -------------------  --------------------
SampleVM          168.61.54.62         10.0.0.4
```

> [!NOTE]
> <span data-ttu-id="1814a-116">Beachten Sie, dass die Verwendung von Kurzsyntax für die `--output` kennzeichnen als `-o`.</span><span class="sxs-lookup"><span data-stu-id="1814a-116">Notice that we are using a shorthand syntax for the `--output` flag as `-o`.</span></span> <span data-ttu-id="1814a-117">Die meisten Parameter für Azure CLI-Befehlen können es sich um Shortend auf eine einzelne Gedankenstriche und der Buchstabe sein.</span><span class="sxs-lookup"><span data-stu-id="1814a-117">Most parameters to Azure CLI commands can be shortend to a single dash and letter.</span></span> <span data-ttu-id="1814a-118">Z. B. `--name` verkürzt werden kann, um `-n` und `--resource-group` zu `-g`.</span><span class="sxs-lookup"><span data-stu-id="1814a-118">For example, `--name` can be shortened to `-n` and `--resource-group` to `-g`.</span></span> <span data-ttu-id="1814a-119">Dies ist praktisch für die Eingabe, aber es wird empfohlen, den Namen der Option "vollständig" aus Gründen der Übersichtlichkeit in Skripts verwenden.</span><span class="sxs-lookup"><span data-stu-id="1814a-119">This is handy for typing, but we recommend using the full option name in scripts for clarity.</span></span> <span data-ttu-id="1814a-120">Überprüfen Sie die Dokumentation für die Details zu den einzelnen Befehlen.</span><span class="sxs-lookup"><span data-stu-id="1814a-120">Check the documentation for details on each command.</span></span>

## <a name="getting-vm-details"></a><span data-ttu-id="1814a-121">Abrufen von Details zum virtuellen Computer</span><span class="sxs-lookup"><span data-stu-id="1814a-121">Getting VM details</span></span>

<span data-ttu-id="1814a-122">Wir können weitere ausführliche Informationen zu einem bestimmten virtuellen Computer nach Name oder Id mithilfe der `vm show` Befehl.</span><span class="sxs-lookup"><span data-stu-id="1814a-122">We can get more detailed information about a specific virtual machine by name or id using the `vm show` command.</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM
```

<span data-ttu-id="1814a-123">Dadurch wird einen ziemlich großen JSON-Block mit unterschiedlichsten Informationen zu den virtuellen Computer, einschließlich NAS-Geräte, Netzwerkschnittstellen und alle der Objekt-IDs für Ressourcen, denen mit der virtuellen Computer verbunden ist, zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="1814a-123">This will return a fairly large JSON block with all sorts of information about the VM including attached storage devices, network interfaces, and all of the object IDs for resources that the VM is connected to.</span></span> <span data-ttu-id="1814a-124">In diesem Fall wir können in einem Tabellenformat ändern, aber der, die fast alle relevanten Daten.</span><span class="sxs-lookup"><span data-stu-id="1814a-124">Again, we could change to a table format, but that omits almost all of the interesting data.</span></span> <span data-ttu-id="1814a-125">Stattdessen können Sie sich nun um eine integrierte Abfragesprache für JSON aufgerufen [JMESPath](http://jmespath.org/).</span><span class="sxs-lookup"><span data-stu-id="1814a-125">Instead, we can turn to a built-in query language for JSON called [JMESPath](http://jmespath.org/).</span></span>

## <a name="adding-filters-to-queries-with-jmespath"></a><span data-ttu-id="1814a-126">Hinzufügen von Filtern zu Abfragen mit JMESPath</span><span class="sxs-lookup"><span data-stu-id="1814a-126">Adding filters to queries with JMESPath</span></span>

<span data-ttu-id="1814a-127">JMESPath ist eine Abfragesprache nach Industriestandard so konzipiert, JSON-Objekte.</span><span class="sxs-lookup"><span data-stu-id="1814a-127">JMESPath is an industry standard query language built around JSON objects.</span></span> <span data-ttu-id="1814a-128">Die einfachste Abfrage wird an eine _Bezeichner_ , der einen Schlüssel im JSON-Objekt auswählt.</span><span class="sxs-lookup"><span data-stu-id="1814a-128">The simplest query is to specify an _identifier_ that selects a key in the JSON object.</span></span>

<span data-ttu-id="1814a-129">Angenommen, das Objekt:</span><span class="sxs-lookup"><span data-stu-id="1814a-129">For example, given the object:</span></span>

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

<span data-ttu-id="1814a-130">Wir können die Abfrage `people` zurückzugebenden das Array von Werten für die `people` Array.</span><span class="sxs-lookup"><span data-stu-id="1814a-130">We can use the query `people` to return the array of values for the `people` array.</span></span> <span data-ttu-id="1814a-131">Wenn wir wollen da _eine_ der Personen, wir können einen Indexer verwenden: z. B. `people[1]` zurück:</span><span class="sxs-lookup"><span data-stu-id="1814a-131">If we just want _one_ of the people, we can use an indexer: for example, `people[1]` would return:</span></span>

```json
{
    "name": "Barney",
    "age": 25
}
```

<span data-ttu-id="1814a-132">Wir können auch hinzufügen, bestimmte Qualifizierer, der zurückgegeben würde nur die `Fred` und `Wilma` Objekte.</span><span class="sxs-lookup"><span data-stu-id="1814a-132">We can also add specific qualifiers,  that would return just the `Fred` and `Wilma` objects.</span></span> 

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

<span data-ttu-id="1814a-133">Schließlich können wir die Ergebnisse eingeschränkt werden durch eine SELECT-Anweisung hinzufügen: `people[?age > '25'].[name]` , die nur die Namen zurückgibt:</span><span class="sxs-lookup"><span data-stu-id="1814a-133">Finally, we can constrain the results by adding a select: `people[?age > '25'].[name]` that returns just the names:</span></span>

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

<span data-ttu-id="1814a-134">JMESQuery verfügt über mehrere andere interessante Abfragefeatures.</span><span class="sxs-lookup"><span data-stu-id="1814a-134">JMESQuery has several other interesting query features.</span></span> <span data-ttu-id="1814a-135">Wenn Sie Zeit haben, sehen Sie sich die [Onlinelernprogramm](http://jmespath.org/tutorial.html) auf der [JMESPath.org](http://jmespath.org/) Standort.</span><span class="sxs-lookup"><span data-stu-id="1814a-135">When you have time, check out the [online tutorial](http://jmespath.org/tutorial.html) available on the [JMESPath.org](http://jmespath.org/) site.</span></span>

## <a name="filtering-our-azure-cli-queries"></a><span data-ttu-id="1814a-136">Filtern von unseren Azure-Befehlszeilenschnittstelle Abfragen</span><span class="sxs-lookup"><span data-stu-id="1814a-136">Filtering our Azure CLI queries</span></span>

<span data-ttu-id="1814a-137">Grundlegende Kenntnisse zu JMES Abfragen, können wir Speichereinheiten hinzufügen, auf die Daten, die zurückgegeben wird, von Abfragen wie die `vm show` Befehl.</span><span class="sxs-lookup"><span data-stu-id="1814a-137">With a basic understanding of JMES queries, we can add filers to the data being returned by queries like the `vm show` command.</span></span> <span data-ttu-id="1814a-138">Beispielsweise können wir den Namen des Administratorbenutzers abrufen:</span><span class="sxs-lookup"><span data-stu-id="1814a-138">For example, we can retrieve the admin user name:</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "osProfile.adminUsername"
```

<span data-ttu-id="1814a-139">Wir können die Größe, die an den virtuellen Computer zugewiesen:</span><span class="sxs-lookup"><span data-stu-id="1814a-139">We can get the size assigned to our VM:</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query hardwareProfile.vmSize
```

<span data-ttu-id="1814a-140">Oder um alle für die Netzwerkschnittstellen-IDs abzurufen, können Sie die Abfrage verwenden:</span><span class="sxs-lookup"><span data-stu-id="1814a-140">Or to retrieve all the IDs for your network interfaces, you can use the query:</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "networkProfile.networkInterfaces[].id"
```

<span data-ttu-id="1814a-141">Dieses Verfahren für die Abfrage funktioniert mit jedem Azure-CLI-Befehl und kann zum Abrufen von bestimmten Bits der Daten in der Befehlszeile verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="1814a-141">This query technique will work with any Azure CLI command and can be used to pull specific bits of data out on the command line.</span></span> <span data-ttu-id="1814a-142">Es ist hilfreich für die Skripterstellung als auch – Sie können z. B. einen Wert aus Ihrem Azure-Konto abrufen und in einer Umgebung oder ein Skript-Variable zu speichern.</span><span class="sxs-lookup"><span data-stu-id="1814a-142">It is useful for scripting as well - for example, you can pull a value out of your Azure account and store it in an environment or script variable.</span></span> <span data-ttu-id="1814a-143">Wenn Sie es auf diese Weise verwenden möchten, ist ein nützliches Flag Hinzufügen der `--output tsv` Parameter (die kann in der Kurzform `-o tsv`).</span><span class="sxs-lookup"><span data-stu-id="1814a-143">If you decide to use it this way, a useful flag to add is the `--output tsv` parameter (which can be shortened to `-o tsv`).</span></span> <span data-ttu-id="1814a-144">Dadurch wird die Ergebnisse in per Tabulator getrennte Werte zurückgegeben, die nur die tatsächlichen Datenwerte mit Registerkarte Trennzeichen enthalten.</span><span class="sxs-lookup"><span data-stu-id="1814a-144">This will return the results in tab-separated values that only include the actual data values with tab separators.</span></span>

<span data-ttu-id="1814a-145">Als Beispiel</span><span class="sxs-lookup"><span data-stu-id="1814a-145">As an example,</span></span>

```azurecli
az vm show --resource-group ExerciseResources --name SampleVM --query "networkProfile.networkInterfaces[].id" -o tsv
```

<span data-ttu-id="1814a-146">Gibt den Text zurück: `/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Network/networkInterfaces/SampleVMVMNic`</span><span class="sxs-lookup"><span data-stu-id="1814a-146">returns the text: `/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Network/networkInterfaces/SampleVMVMNic`</span></span>
