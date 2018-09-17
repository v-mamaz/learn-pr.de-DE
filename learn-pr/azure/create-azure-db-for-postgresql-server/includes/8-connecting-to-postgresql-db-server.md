<span data-ttu-id="9cf94-101">Angenommen, Sie arbeiten mit einer lokalen PostgreSQL-Datenbank.</span><span class="sxs-lookup"><span data-stu-id="9cf94-101">Lets' assume you're using an on-premises PostgreSQL database.</span></span> <span data-ttu-id="9cf94-102">Sie verwalten sämtliche Sicherheitsaspekte und haben den gesamten Zugriff auf Ihre Server mit den standardmäßigen Firewallregeln auf PostgreSQL-Serverebene gesperrt.</span><span class="sxs-lookup"><span data-stu-id="9cf94-102">You're managing all security aspects and locked down all access to your servers using the standard PostgreSQL server level firewall rules.</span></span> <span data-ttu-id="9cf94-103">Sie wissen, wie Sie die gleichen Firewallregeln auf Serverebene in Azure konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="9cf94-103">You now have a good understanding of how to configure the same server level firewall rules in Azure.</span></span>

<span data-ttu-id="9cf94-104">Nun haben Sie die Möglichkeit, mithilfe von `psql` eine Verbindung mit einem der zuvor erstellten Azure Database for PostgreSQL-Server herzustellen.</span><span class="sxs-lookup"><span data-stu-id="9cf94-104">You now have the chance to connect to one of the previous Azure Databases for PostgreSQL servers you created using `psql`.</span></span>

## <a name="allow-azure-service-access"></a><span data-ttu-id="9cf94-105">Zulassen des Zugriffs für Azure-Dienste</span><span class="sxs-lookup"><span data-stu-id="9cf94-105">Allow Azure service access</span></span>

<span data-ttu-id="9cf94-106">Vorbereitung:</span><span class="sxs-lookup"><span data-stu-id="9cf94-106">Before we begin.</span></span> <span data-ttu-id="9cf94-107">Sie müssen den Zugriff auf Azure-Dienste zulassen, wenn Sie mithilfe von PowerShell und `psql` eine Verbindung mit Ihrem Server herstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="9cf94-107">You'll have to allow access to Azure services if you want to use PowerShell and `psql` to connect to your server.</span></span> <span data-ttu-id="9cf94-108">Zur Erinnerung: Zugriff kann auf zwei Arten zugelassen werden.</span><span class="sxs-lookup"><span data-stu-id="9cf94-108">Recall, that you can allow access in two ways.</span></span>

<span data-ttu-id="9cf94-109">Die erste Möglichkeit besteht darin, **Zugriff auf Azure-Dienste erlauben** zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="9cf94-109">Your first option is to enable **Allow access to Azure services**.</span></span> <span data-ttu-id="9cf94-110">Wenn Sie den Zugriff zulassen, wird eine Firewallregel erstellt. Diese wird jedoch nicht in die Liste mit den benutzerdefinierten Regeln aufgenommen, die Sie erstellen.</span><span class="sxs-lookup"><span data-stu-id="9cf94-110">Allowing access will create a firewall rule even though the rule isn't entered in the list of custom rules you create.</span></span>

<span data-ttu-id="9cf94-111">Die zweite Möglichkeit besteht darin, eine Firewallregel zu erstellen, die den Zugriff auf alle IP-Adressen zulässt.</span><span class="sxs-lookup"><span data-stu-id="9cf94-111">Your second option is to create a firewall rule that allows access to all IP addresses.</span></span> <span data-ttu-id="9cf94-112">Die Regel enthält die IP-Adresse für den Client, auf dem PowerShell ausgeführt wird und von dem aus Sie `psql` ausführen.</span><span class="sxs-lookup"><span data-stu-id="9cf94-112">The rule will include the IP address for the client running PowerShell that you'll use to execute `psql` from.</span></span>

<span data-ttu-id="9cf94-113">Darüber hinaus müssen Sie **SSL-Verbindung erzwingen** deaktivieren.</span><span class="sxs-lookup"><span data-stu-id="9cf94-113">You also need to disable the **Enforce SSL connection**.</span></span>

<span data-ttu-id="9cf94-114">Legen wir los.</span><span class="sxs-lookup"><span data-stu-id="9cf94-114">Let's begin.</span></span>

<span data-ttu-id="9cf94-115">Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an.</span><span class="sxs-lookup"><span data-stu-id="9cf94-115">Sign in to [the Azure portal](https://portal.azure.com?azure-portal=true).</span></span> <span data-ttu-id="9cf94-116">Navigieren Sie zu der Serverressource, für die Sie eine Firewallregel erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="9cf94-116">Navigate to the server resource for which you would like to create a firewall rule.</span></span>

<span data-ttu-id="9cf94-117">Wählen Sie die Option **Verbindungssicherheit** aus, um auf der rechten Seite das entsprechende Blatt zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="9cf94-117">Select the **Connection Security** option to open the connection security blade to the right.</span></span>

![Sicherheitseinstellungen für die PostgreSQL-Datenbank](../media-draft/7-db-security-settings.png)

<span data-ttu-id="9cf94-119">Zur Erinnerung: Sie möchten den Zugriff auf PowerShell-Clients zulassen, auf denen `psql` ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="9cf94-119">Recall, you want to allow access to PowerShell clients running `psql`.</span></span>

<span data-ttu-id="9cf94-120">Verwenden Sie eines der folgenden Verfahren:</span><span class="sxs-lookup"><span data-stu-id="9cf94-120">You can choose to either:</span></span>

- <span data-ttu-id="9cf94-121">Legen Sie **Zugriff auf Azure-Dienste erlauben** auf **EIN** fest.</span><span class="sxs-lookup"><span data-stu-id="9cf94-121">Set **Allow access to Azure services** to **ON**</span></span>
- <span data-ttu-id="9cf94-122">Legen Sie **SSL-Verbindung erzwingen** auf **DEAKTIVIERT** fest.</span><span class="sxs-lookup"><span data-stu-id="9cf94-122">Set **Enforce SSL connection** to **DISABLED**</span></span>
- <span data-ttu-id="9cf94-123">Klicken Sie auf die Schaltfläche **Speichern**, um die Änderungen zu speichern.</span><span class="sxs-lookup"><span data-stu-id="9cf94-123">Click the **Save** button to save your changes</span></span>

<span data-ttu-id="9cf94-124">Oder: Fügen Sie eine Firewallregel hinzu, um den Zugriff auf alle IP-Adressen zuzulassen.</span><span class="sxs-lookup"><span data-stu-id="9cf94-124">Or, you can add a firewall rule to allow access to all IP addresses by adding a firewall rule.</span></span> <span data-ttu-id="9cf94-125">Verwenden Sie folgende Werte:</span><span class="sxs-lookup"><span data-stu-id="9cf94-125">Use the following values:</span></span>

- <span data-ttu-id="9cf94-126">Regelname: `AllowAll`</span><span class="sxs-lookup"><span data-stu-id="9cf94-126">Rule Name: `AllowAll`</span></span>
- <span data-ttu-id="9cf94-127">Start-IP: `0.0.0.0`</span><span class="sxs-lookup"><span data-stu-id="9cf94-127">Start IP: `0.0.0.0`</span></span>
- <span data-ttu-id="9cf94-128">End-IP: `255.255.255.255`</span><span class="sxs-lookup"><span data-stu-id="9cf94-128">End IP: `255.255.255.255`</span></span>
- <span data-ttu-id="9cf94-129">Legen Sie **SSL-Verbindung erzwingen** auf **DEAKTIVIERT** fest.</span><span class="sxs-lookup"><span data-stu-id="9cf94-129">Set **Enforce SSL connection** to **DISABLED**</span></span>
- <span data-ttu-id="9cf94-130">Klicken Sie auf die Schaltfläche **Speichern**, um die Änderungen zu speichern.</span><span class="sxs-lookup"><span data-stu-id="9cf94-130">Click the **Save** button to save your changes</span></span>

> [!Warning]
> <span data-ttu-id="9cf94-131">Wenn Sie diese Firewallregel erstellen, kann über jede IP-Adresse im Internet versucht werden, eine Verbindung mit Ihrem Server herzustellen.</span><span class="sxs-lookup"><span data-stu-id="9cf94-131">Creating this firewall rule will allow any IP address on the Internet to attempt to connect to your server.</span></span> <span data-ttu-id="9cf94-132">Ohne Benutzername und Kennwort können Clients zwar nicht auf den Server zugreifen, aktivieren Sie diese Regel aber dennoch mit Bedacht und nur, wenn Sie verstehen, was das für die Sicherheit bedeutet.</span><span class="sxs-lookup"><span data-stu-id="9cf94-132">Even though clients will not be able access the server without the username and password, enable this rule with caution and make sure you understand the security implications.</span></span> <span data-ttu-id="9cf94-133">In Produktionsumgebungen lassen Sie den Zugriff nur für bestimmte Client-IP-Adressen zu.</span><span class="sxs-lookup"><span data-stu-id="9cf94-133">In production environments, you'll only allow access to specific client IP addresses.</span></span>

<span data-ttu-id="9cf94-134">Für die nächsten Schritte benötigen wir eine Azure Cloud Shell-Sitzung.</span><span class="sxs-lookup"><span data-stu-id="9cf94-134">For the next steps, you'll start an Azure Cloud Shell session.</span></span> <span data-ttu-id="9cf94-135">In diesem Lab wird `bash` als Befehlszeilenumgebung verwendet.</span><span class="sxs-lookup"><span data-stu-id="9cf94-135">This lab uses `bash` as the command-line environment.</span></span>

- <span data-ttu-id="9cf94-136">Öffnen Sie Cloud Shell über das Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="9cf94-136">Open the Cloud Shell from the Azure portal.</span></span> <span data-ttu-id="9cf94-137">Klicken Sie im [Azure-Portal](https://portal.azure.com?azure-portal=true) auf die Schaltfläche „Cloud Shell öffnen“:</span><span class="sxs-lookup"><span data-stu-id="9cf94-137">Go to [Azure portal](https://portal.azure.com?azure-portal=true) and click the Open Cloud Shell button:</span></span>

  ![Cloud Shell-Schaltfläche](../media-draft/cloud-shell-button.png)

- <span data-ttu-id="9cf94-139">Sollten Sie über mehrere Abonnements verfügen, vergewissern Sie sich, dass Sie das richtige Abonnement verwenden, wenn Sie dazu aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="9cf94-139">In case you have several subscriptions, check to make sure you're using the correct subscription when asked.</span></span> <span data-ttu-id="9cf94-140">Sie können auch den folgenden Befehl ausführen, um das aktive Abonnement festzulegen.</span><span class="sxs-lookup"><span data-stu-id="9cf94-140">You can also run the following command to set the active subscription.</span></span> <span data-ttu-id="9cf94-141">Vergessen Sie nicht, die Nullen durch Ihre Abonnement-ID zu ersetzen.</span><span class="sxs-lookup"><span data-stu-id="9cf94-141">Remember to replace the zeros with your subscription identifier.</span></span>

   ```bash
   az account set --subscription 00000000-0000-0000-0000-000000000000
   ```

- <span data-ttu-id="9cf94-142">Verbinden Sie psql mithilfe des folgenden Befehls mit Ihrem Server:</span><span class="sxs-lookup"><span data-stu-id="9cf94-142">Connect psql to your server using the following command:</span></span>

  ```bash
  psql --host=<server-name>.postgres.database.azure.com --username=<admin-user>@<server-name> --dbname=postgres
  ```

   <span data-ttu-id="9cf94-143">`server-name` und `admin-user` sind die Werte, die Sie beim Erstellen des Servers für Ihr Administratorkonto ausgewählt haben.</span><span class="sxs-lookup"><span data-stu-id="9cf94-143">Recall, `server-name`, and `admin-user` are the values you chose for the administrator account when you created the server.</span></span> <span data-ttu-id="9cf94-144">`postgres` ist die standardmäßige Verwaltungsdatenbank, mit der jeder PostgreSQL-Server erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="9cf94-144">`postgres` is the default management database every PostgreSQL server is created with.</span></span> <span data-ttu-id="9cf94-145">Sie werden zur Eingabe des Kennworts aufgefordert, das Sie beim Erstellen des Servers angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="9cf94-145">You'll be prompted for the password you provided when you created the server.</span></span>

- <span data-ttu-id="9cf94-146">Führen Sie nach erfolgreicher Verbindungsherstellung den Befehl `\l` aus, um alle Datenbanken aufzulisten.</span><span class="sxs-lookup"><span data-stu-id="9cf94-146">Once successfully connected, execute the `\l` command to list all databases.</span></span>

   <span data-ttu-id="9cf94-147">Daraufhin werden mindestens zwei Standarddatenbanken zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="9cf94-147">This command will result in two or more default databases returned from.</span></span>

- <span data-ttu-id="9cf94-148">Wenn Sie auf Ihrem Server keine weiteren psql-Vorgänge mehr ausführen möchten, führen Sie den Befehl `\q` aus, um `psql` zu beenden.</span><span class="sxs-lookup"><span data-stu-id="9cf94-148">When you're finished executing psql operations on your server, execute the command `\q` to quit `psql`.</span></span>

- <span data-ttu-id="9cf94-149">Führen Sie abschließend den Befehl `exit` aus, um Cloud Shell zu beenden.</span><span class="sxs-lookup"><span data-stu-id="9cf94-149">Finally, to exit Cloud Shell, execute the command `exit`.</span></span>
