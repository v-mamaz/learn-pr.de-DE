<span data-ttu-id="daba5-101">Angenommen, Sie arbeiten mit einer lokalen PostgreSQL-Datenbank.</span><span class="sxs-lookup"><span data-stu-id="daba5-101">Let's assume that you're using an on-premises PostgreSQL database.</span></span> <span data-ttu-id="daba5-102">Sie verwalten sämtliche Sicherheitsaspekte und haben alle Zugriffe auf Ihre Server mit den Standardfirewallregeln auf PostgreSQL-Serverebene gesperrt.</span><span class="sxs-lookup"><span data-stu-id="daba5-102">You're managing all security aspects and you've locked down all access to your servers using the standard PostgreSQL server-level firewall rules.</span></span> <span data-ttu-id="daba5-103">Sie wissen mittlerweile, wie Sie die gleichen Firewallregeln auf Serverebene in Azure konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="daba5-103">You now have a good understanding of how to configure the same server-level firewall rules in Azure.</span></span>

<span data-ttu-id="daba5-104">Als Nächstes stellen wir eine Verbindung mit einem der zuvor erstellten Azure Database for PostgreSQL-Server her.</span><span class="sxs-lookup"><span data-stu-id="daba5-104">Let's connect to one of the Azure Database for PostgreSQL servers that you created.</span></span>

## <a name="allow-azure-service-access"></a><span data-ttu-id="daba5-105">Zulassen des Zugriffs auf Azure-Dienste</span><span class="sxs-lookup"><span data-stu-id="daba5-105">Allow Azure service access</span></span>

<span data-ttu-id="daba5-106">Bevor Sie beginnen, müssen Sie den Zugriff auf Azure-Dienste zulassen, wenn Sie mithilfe von PowerShell und `psql` eine Verbindung mit Ihrem Server herstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="daba5-106">Before we begin, you'll have to allow access to Azure services if you want to use PowerShell and `psql` to connect to your server.</span></span> <span data-ttu-id="daba5-107">Zur Erinnerung: Der Zugriff kann auf zwei Arten zugelassen werden.</span><span class="sxs-lookup"><span data-stu-id="daba5-107">Recall that you can allow access in two ways.</span></span>

<span data-ttu-id="daba5-108">Die erste Möglichkeit besteht darin, **Zugriff auf Azure-Dienste erlauben** zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="daba5-108">Your first option is to enable **Allow access to Azure services**.</span></span> <span data-ttu-id="daba5-109">Wenn Sie den Zugriff zulassen, wird eine Firewallregel erstellt. Diese wird jedoch nicht in die Liste mit den benutzerdefinierten Regeln aufgenommen, die Sie erstellen.</span><span class="sxs-lookup"><span data-stu-id="daba5-109">Allowing access will create a firewall rule even though the rule isn't entered in the list of custom rules you create.</span></span>

<span data-ttu-id="daba5-110">Die zweite Möglichkeit besteht darin, eine Firewallregel zu erstellen, die den Zugriff auf alle IP-Adressen zulässt.</span><span class="sxs-lookup"><span data-stu-id="daba5-110">Your second option is to create a firewall rule that allows access to all IP addresses.</span></span> <span data-ttu-id="daba5-111">Die Regel enthält die IP-Adresse für den Client, auf dem PowerShell ausgeführt wird und über den Sie `psql` ausführen.</span><span class="sxs-lookup"><span data-stu-id="daba5-111">The rule will include the IP address for the client running PowerShell that you'll use to execute `psql` from.</span></span>

<span data-ttu-id="daba5-112">Darüber hinaus müssen Sie die Option **SSL-Verbindung erzwingen** deaktivieren.</span><span class="sxs-lookup"><span data-stu-id="daba5-112">You also need to disable the **Enforce SSL connection** option.</span></span>

### <a name="create-a-firewall-rule"></a><span data-ttu-id="daba5-113">Erstellen einer Firewallregel</span><span class="sxs-lookup"><span data-stu-id="daba5-113">Create a firewall rule</span></span>

1. <span data-ttu-id="daba5-114">Melden Sie sich beim [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) mit dem gleichen Konto an, über das Sie die Sandbox aktiviert haben.</span><span class="sxs-lookup"><span data-stu-id="daba5-114">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="daba5-115">Navigieren Sie zu der Serverressource, für die Sie eine Firewallregel erstellen möchten.</span><span class="sxs-lookup"><span data-stu-id="daba5-115">Navigate to the server resource for which you would like to create a firewall rule.</span></span>

1. <span data-ttu-id="daba5-116">Wählen Sie die Option **Verbindungssicherheit** aus, um auf der rechten Seite das entsprechende Blatt zu öffnen.</span><span class="sxs-lookup"><span data-stu-id="daba5-116">Select the **Connection Security** option to open the connection security blade to the right.</span></span>

    ![Screenshot des Azure-Portals mit Abschnitt „Verbindungssicherheit“ auf dem Ressourcenblatt „PostgreSQL-Datenbank“](../media/7-db-security-settings.png)

<span data-ttu-id="daba5-118">Zur Erinnerung: Sie möchten den Zugriff auf PowerShell-Clients zulassen, auf denen `psql` ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="daba5-118">Recall that you want to allow access to PowerShell clients running `psql`.</span></span>

<span data-ttu-id="daba5-119">Verwenden Sie dazu eine der folgenden Methoden:</span><span class="sxs-lookup"><span data-stu-id="daba5-119">You can choose to either:</span></span>

- <span data-ttu-id="daba5-120">Legen Sie **Zugriff auf Azure-Dienste erlauben** auf **EIN** fest.</span><span class="sxs-lookup"><span data-stu-id="daba5-120">Set **Allow access to Azure services** to **ON**</span></span>
- <span data-ttu-id="daba5-121">Legen Sie **SSL-Verbindung erzwingen** auf **DEAKTIVIERT** fest.</span><span class="sxs-lookup"><span data-stu-id="daba5-121">Set **Enforce SSL connection** to **DISABLED**</span></span>
- <span data-ttu-id="daba5-122">Klicken Sie auf die Schaltfläche **Speichern**, um die Änderungen zu speichern.</span><span class="sxs-lookup"><span data-stu-id="daba5-122">Click the **Save** button to save your changes</span></span>

<span data-ttu-id="daba5-123">Oder: Fügen Sie eine Firewallregel hinzu, um den Zugriff auf alle IP-Adressen zuzulassen.</span><span class="sxs-lookup"><span data-stu-id="daba5-123">Or, you can add a firewall rule to allow access to all IP addresses by adding a firewall rule.</span></span> <span data-ttu-id="daba5-124">Verwenden Sie folgende Werte:</span><span class="sxs-lookup"><span data-stu-id="daba5-124">Use the following values:</span></span>

- <span data-ttu-id="daba5-125">Regelname: `AllowAll`</span><span class="sxs-lookup"><span data-stu-id="daba5-125">Rule Name: `AllowAll`</span></span>
- <span data-ttu-id="daba5-126">Start-IP: `0.0.0.0`</span><span class="sxs-lookup"><span data-stu-id="daba5-126">Start IP: `0.0.0.0`</span></span>
- <span data-ttu-id="daba5-127">End-IP: `255.255.255.255`</span><span class="sxs-lookup"><span data-stu-id="daba5-127">End IP: `255.255.255.255`</span></span>
- <span data-ttu-id="daba5-128">Legen Sie **SSL-Verbindung erzwingen** auf **DEAKTIVIERT** fest.</span><span class="sxs-lookup"><span data-stu-id="daba5-128">Set **Enforce SSL connection** to **DISABLED**</span></span>
- <span data-ttu-id="daba5-129">Klicken Sie auf die Schaltfläche **Speichern**, um die Änderungen zu speichern.</span><span class="sxs-lookup"><span data-stu-id="daba5-129">Click the **Save** button to save your changes</span></span>

> [!Warning]
> <span data-ttu-id="daba5-130">Wenn Sie diese Firewallregel erstellen, kann über jede IP-Adresse im Internet versucht werden, eine Verbindung mit Ihrem Server herzustellen.</span><span class="sxs-lookup"><span data-stu-id="daba5-130">Creating this firewall rule will allow any IP address on the Internet to attempt to connect to your server.</span></span> <span data-ttu-id="daba5-131">In Produktionsumgebungen sollte der Zugriff nur für bestimmte Client-IP-Adressen zugelassen werden.</span><span class="sxs-lookup"><span data-stu-id="daba5-131">In production environments, you'll want to restrict access to specific IP addresses.</span></span>

### <a name="connect-to-the-database-with-psql"></a><span data-ttu-id="daba5-132">Herstellen einer Datenbankverbindung mit psql</span><span class="sxs-lookup"><span data-stu-id="daba5-132">Connect to the database with psql</span></span>

1. <span data-ttu-id="daba5-133">Stellen Sie auf der rechten Seite in Azure Cloud Shell mithilfe des folgenden Befehls eine Verbindung zwischen psql und Ihrem Server her.</span><span class="sxs-lookup"><span data-stu-id="daba5-133">In the Azure Cloud Shell on the right, connect PSQL to your server using the following command.</span></span> <span data-ttu-id="daba5-134">Ersetzen Sie dabei den Server- und den Administratornamen.</span><span class="sxs-lookup"><span data-stu-id="daba5-134">Make sure to replace the server name and admin name.</span></span>

    ```bash
    psql --host=<server-name>.postgres.database.azure.com --username=<admin-user>@<server-name> --dbname=postgres
    ```

    <span data-ttu-id="daba5-135">Verwenden Sie die Werte, die Sie für `server-name` und `admin-user` gewählt haben.</span><span class="sxs-lookup"><span data-stu-id="daba5-135">Use the values you chose for the `server-name`, and `admin-user`.</span></span>

1. <span data-ttu-id="daba5-136">**postgres** ist die standardmäßige Verwaltungsdatenbank, mit der jeder PostgreSQL-Server erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="daba5-136">**postgres** is the default management database every PostgreSQL server is created with.</span></span> <span data-ttu-id="daba5-137">Sie werden zur Eingabe des Kennworts aufgefordert, das Sie beim Erstellen des Servers angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="daba5-137">You'll be prompted for the password you provided when you created the server.</span></span>

1. <span data-ttu-id="daba5-138">Führen Sie nach erfolgreicher Verbindungsherstellung den Befehl <kbd>\l</kbd> aus, um alle Datenbanken aufzulisten.</span><span class="sxs-lookup"><span data-stu-id="daba5-138">Once successfully connected, execute the <kbd>\l</kbd> command to list all databases.</span></span> <span data-ttu-id="daba5-139">Daraufhin werden mindestens zwei Standarddatenbanken zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="daba5-139">This command will result in two or more default databases returned.</span></span>

1. <span data-ttu-id="daba5-140">Drücken Sie <kbd>q</kbd>, um die Liste zu schließen.</span><span class="sxs-lookup"><span data-stu-id="daba5-140">Hit <kbd>q</kbd> to exit the list.</span></span>

1. <span data-ttu-id="daba5-141">Sie können auch andere psql-Befehle ausprobieren.</span><span class="sxs-lookup"><span data-stu-id="daba5-141">You can try other PSQL commands.</span></span>
    - <kbd>\?</kbd> <span data-ttu-id="daba5-142">dient zum Aufrufen der Hilfe.</span><span class="sxs-lookup"><span data-stu-id="daba5-142">to get help.</span></span>
    - <span data-ttu-id="daba5-143"><kbd>\dt</kbd> dient zum Auflisten der Tabellen.</span><span class="sxs-lookup"><span data-stu-id="daba5-143"><kbd>\dt</kbd> to list the tables.</span></span>

1. <span data-ttu-id="daba5-144">Wenn Sie auf Ihrem Server keine weiteren psql-Vorgänge mehr ausführen möchten, führen Sie den Befehl <kbd>\q</kbd> aus, um psql zu beenden.</span><span class="sxs-lookup"><span data-stu-id="daba5-144">When you're finished executing PSQL operations on your server, execute the command <kbd>\q</kbd> to quit PSQL.</span></span>
