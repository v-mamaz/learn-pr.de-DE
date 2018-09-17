<span data-ttu-id="b5cde-101">Nachdem Sie Ihren Event Hub erstellt und konfiguriert haben, müssen Sie Anwendungen für das Senden und Empfangen von Ereignisdatenströmen konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="b5cde-101">After you have created and configured your event hub, you'll need to configure applications to send and receive event data streams.</span></span>

<span data-ttu-id="b5cde-102">Eine Zahlungsabwicklungslösung verwendet beispielsweise eine Form von Absenderanwendung, um die Kreditkartendaten des Kunden zu erfassen, und eine Empfängeranwendung, um die Gültigkeit der Kreditkarte zu verifizieren.</span><span class="sxs-lookup"><span data-stu-id="b5cde-102">For example, a payment processing solution will use some form of sender application to collect customer's credit card data and a receiver application to verify that the credit card is valid.</span></span>

<span data-ttu-id="b5cde-103">Obwohl es Unterschiede gibt, wie eine Java-Anwendung konfiguriert ist, gelten im Vergleich mit einer .NET-Anwendung allgemeine Grundsätze, gemäß denen Anwendungen die Verbindung mit einem Event Hub und das erfolgreiche Senden oder Empfangen von Nachrichten ermöglicht werden können.</span><span class="sxs-lookup"><span data-stu-id="b5cde-103">Although there are differences in how a Java application is configured, compared to a .NET application, there are general principles for enabling applications to connect to an event hub, and to successfully send or receive messages.</span></span> <span data-ttu-id="b5cde-104">Obwohl sich die Bearbeitung von Java-Konfigurationstextdateien von der Vorbereitung einer.NET-Anwendung mit Visual Studio unterscheidet, sind die Grundsätze dieselben.</span><span class="sxs-lookup"><span data-stu-id="b5cde-104">So, although the process of editing Java configuration text files is different to preparing a .NET application using Visual Studio, the principles are the same.</span></span>

## <a name="what-are-the-minimum-event-hub-application-requirements"></a><span data-ttu-id="b5cde-105">Was sind die Mindestanforderungen einer Event Hub-Anwendung?</span><span class="sxs-lookup"><span data-stu-id="b5cde-105">What are the minimum Event Hub application requirements?</span></span>

<span data-ttu-id="b5cde-106">Um eine Anwendung für das Senden von Nachrichten an einen Event Hub zu konfigurieren, müssen Sie die folgenden Informationen angeben, damit die Anwendung Anmeldeinformationen für die Verbindung erstellen kann:</span><span class="sxs-lookup"><span data-stu-id="b5cde-106">To configure an application to send messages to an event hub, you must provide the following information, so that the application can create connection credentials:</span></span>

- <span data-ttu-id="b5cde-107">Name des Event Hub-Namespace</span><span class="sxs-lookup"><span data-stu-id="b5cde-107">Event hub namespace name</span></span>
- <span data-ttu-id="b5cde-108">Event Hub-Name</span><span class="sxs-lookup"><span data-stu-id="b5cde-108">Event hub name</span></span>
- <span data-ttu-id="b5cde-109">Name der freigegebenen Zugriffsrichtlinie</span><span class="sxs-lookup"><span data-stu-id="b5cde-109">Shared access policy name</span></span>
- <span data-ttu-id="b5cde-110">Primärer freigegebener Zugriffsschlüssel</span><span class="sxs-lookup"><span data-stu-id="b5cde-110">Primary shared access key</span></span>

<span data-ttu-id="b5cde-111">Um eine Anwendung für das Empfangen von Nachrichten von einen Event Hub zu konfigurieren, geben Sie die folgenden Informationen an, damit die Anwendung Anmeldeinformationen für die Verbindung erstellen kann:</span><span class="sxs-lookup"><span data-stu-id="b5cde-111">To configure an application to receive messages from an event hub, provide the following information, so that the application can create connection credentials:</span></span>

- <span data-ttu-id="b5cde-112">Name des Event Hub-Namespace</span><span class="sxs-lookup"><span data-stu-id="b5cde-112">Event hub namespace name</span></span>
- <span data-ttu-id="b5cde-113">Event Hub-Name</span><span class="sxs-lookup"><span data-stu-id="b5cde-113">Event hub name</span></span>
- <span data-ttu-id="b5cde-114">Name der freigegebenen Zugriffsrichtlinie</span><span class="sxs-lookup"><span data-stu-id="b5cde-114">Shared access policy name</span></span>
- <span data-ttu-id="b5cde-115">Primärer freigegebener Zugriffsschlüssel</span><span class="sxs-lookup"><span data-stu-id="b5cde-115">Primary shared access key</span></span>
- <span data-ttu-id="b5cde-116">Speicherkontoname</span><span class="sxs-lookup"><span data-stu-id="b5cde-116">Storage account name</span></span>
- <span data-ttu-id="b5cde-117">Verbindungszeichenfolge für das Speicherkonto</span><span class="sxs-lookup"><span data-stu-id="b5cde-117">Storage account connection string</span></span>
- <span data-ttu-id="b5cde-118">Name des Containers mit dem Speicherkonto</span><span class="sxs-lookup"><span data-stu-id="b5cde-118">Storage account container name</span></span>

<span data-ttu-id="b5cde-119">Wenn Sie über eine Empfängeranwendung verfügen, die Nachrichten in Azure Blob Storage speichert, müssen Sie auch zunächst ein Speicherkonto einrichten.</span><span class="sxs-lookup"><span data-stu-id="b5cde-119">If you have a receiver application that stores messages in Azure Blob Storage, you'll also need to first configure a storage account.</span></span>

## <a name="the-azure-cli-commands-for-creating-a-general-purpose-standard-storage-account"></a><span data-ttu-id="b5cde-120">Die Azure CLI-Befehle zum Erstellen eines universellen Standardspeicherkontos</span><span class="sxs-lookup"><span data-stu-id="b5cde-120">The Azure CLI commands for creating a general-purpose standard storage account</span></span>

1. <span data-ttu-id="b5cde-121">Erstellen Sie ein universelles Speicherkonto (Version 2) in Ihrer Ressourcengruppe, und nutzen Sie denselben Standort des Azure-Rechenzentrums, an dem Sie die Ressourcengruppe erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="b5cde-121">Create a general-purpose V2 Storage account in your resource group, and the same Azure datacenter location that you used when creating the resource group.</span></span>

    ```azurecli
    az storage account create --name <storage account name> --resource-group <resource group name> --location <location> --sku Standard_RAGRS --encryption blob
    ```

1. <span data-ttu-id="b5cde-122">Um auf diesen Speicher zugreifen zu können, benötigen Sie einen Zugriffsschlüssel für das Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="b5cde-122">To access this storage, you'll need a storage account access key.</span></span> <span data-ttu-id="b5cde-123">Zeigen Sie die Zugriffsschlüssel an, die dem Speicherkonto zugeordnet sind.</span><span class="sxs-lookup"><span data-stu-id="b5cde-123">View the access keys that are associated with the storage account.</span></span>

    ```azurecli
    az storage account keys list --account-name <storage account name> --resource-group <resource group name>
    ```

1. <span data-ttu-id="b5cde-124">Speichern Sie den **key1** zugeordneten Wert.</span><span class="sxs-lookup"><span data-stu-id="b5cde-124">Save the value associated with **key1**.</span></span>

1. <span data-ttu-id="b5cde-125">Sie benötigen auch die Verbindungsdetails für das Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="b5cde-125">You will also need the connection details for the storage account.</span></span> <span data-ttu-id="b5cde-126">Zeigen Sie die Verbindungszeichenfolge für das Speicherkonto an.</span><span class="sxs-lookup"><span data-stu-id="b5cde-126">View the connection string for the storage account.</span></span>

    ```azurecli
    az storage account show-connection-string -n <storage account name> -g <resource group name>
    ```

1. <span data-ttu-id="b5cde-127">Speichern Sie den **connectionString** zugeordneten Wert.</span><span class="sxs-lookup"><span data-stu-id="b5cde-127">Save the value associated with the **connectionString**.</span></span>

1. <span data-ttu-id="b5cde-128">Nachrichten werden in einem Container in Ihrem Speicherkonto gespeichert.</span><span class="sxs-lookup"><span data-stu-id="b5cde-128">Messages will be stored in a container within your storage account.</span></span> <span data-ttu-id="b5cde-129">Erstellen Sie einen Container in Ihrem Speicherkonto, indem Sie `<connection string>` mit der Verbindungszeichenfolge aus dem vorherigen Schritt verwenden.</span><span class="sxs-lookup"><span data-stu-id="b5cde-129">Create a container in your storage account, using `<connection string>` with the connection string from the previous step.</span></span>

    ```azurecli
    az storage container create -n <container> --connection-string "<connection string>"
    ```

## <a name="shell-command-for-cloning-an-application-github-repository"></a><span data-ttu-id="b5cde-130">Shell-Befehl zum Klonen des GitHub-Repositorys einer Anwendung</span><span class="sxs-lookup"><span data-stu-id="b5cde-130">Shell command for cloning an application GitHub repository</span></span>

<span data-ttu-id="b5cde-131">Git ist ein Tool für die Zusammenarbeit, das ein verteiltes Versionsverwaltungsmodell verwendet und für die gemeinschaftliche Arbeit an Software- und Dokumentationsprojekten konzipiert ist.</span><span class="sxs-lookup"><span data-stu-id="b5cde-131">Git is a collaboration tool that uses a distributed version control model, and is designed for collaborative working on software and documentation projects.</span></span> <span data-ttu-id="b5cde-132">Git-Clients sind für mehrere Plattformen, darunter Windows, verfügbar, und die Git-Befehlszeile ist in der Bash Cloud Shell von Azure enthalten.</span><span class="sxs-lookup"><span data-stu-id="b5cde-132">Git clients are available for multiple platforms, including Windows, and the Git command line is included in the Azure Bash cloud shell.</span></span> <span data-ttu-id="b5cde-133">GitHub ist ein webbasierter Hostingdienst für Git-Repositorys.</span><span class="sxs-lookup"><span data-stu-id="b5cde-133">GitHub is a web-based hosting service for Git repositories.</span></span> 

<span data-ttu-id="b5cde-134">Wenn Sie eine Anwendung haben, die als Projekt in GitHub gehostet wird, können Sie eine lokale Kopie des Projekts erstellen, indem Sie dessen Repository mit dem Befehl **git clone** klonen.</span><span class="sxs-lookup"><span data-stu-id="b5cde-134">If you have an application that is hosted as a project in GitHub, you can make a local copy of the project, by cloning its repository using the **git clone** command.</span></span>

1. <span data-ttu-id="b5cde-135">Klonen Sie ein Repository in Ihr Basisverzeichnis.</span><span class="sxs-lookup"><span data-stu-id="b5cde-135">Clone a repository to your home directory.</span></span>

    ```azurecli
      git clone https://github.com/<project repository>
    ```

## <a name="shell-commands-for-preparing-an-application"></a><span data-ttu-id="b5cde-136">Shellbefehle für das Vorbereiten einer Anwendung</span><span class="sxs-lookup"><span data-stu-id="b5cde-136">Shell commands for preparing an application</span></span>

1. <span data-ttu-id="b5cde-137">Sie können nun einen Editor wie **Nano** einsetzen, um die Anwendung zu bearbeiten und den Namespace und Namen Ihres Event Hubs, den Namen der freigegebenen Zugriffsrichtlinie und den Primärschlüssel hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="b5cde-137">You can now use an editor, such as **nano** to edit the application and add your event hub namespace, event hub name, shared access policy name, and primary key.</span></span> <span data-ttu-id="b5cde-138">Nano ist ein einfacher Texteditor, der für Linux und andere Unix-ähnliche Betriebssysteme sowie auch in der Bash Cloud Shell von Azure zur Verfügung steht.</span><span class="sxs-lookup"><span data-stu-id="b5cde-138">Nano is a simple text editor available for Linux and other Unix-like operating systems; it is also available in the Azure Bash cloud shell.</span></span> <span data-ttu-id="b5cde-139">Verwenden Sie diesen Befehl z.B. zum Öffnen einer Java-Anwendungsdatei im **Nano**-Editor.</span><span class="sxs-lookup"><span data-stu-id="b5cde-139">For example, use this command to open a Java application file in the **nano** editor.</span></span>

    ```azurecli
    nano <application>.java
    ```

1. <span data-ttu-id="b5cde-140">Je nachdem, wie Ihre Anwendungen entwickelt werden, müssen Sie die Anwendung möglicherweise kompilieren oder einen Build dafür erstellen, nachdem Sie die Konfigurationsinformationen für den Event Hub hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="b5cde-140">Depending on how your applications are developed, you may need to compile or build the application after you've added the event hub configuration information.</span></span> <span data-ttu-id="b5cde-141">Die Java-Anwendungen, die in der nächsten Einheit verwendet werden, müssen beispielsweise mithilfe eines Tools wie Apache **Maven** erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="b5cde-141">For example, the Java applications used in the next unit need to be built using a tool such as Apache **Maven**.</span></span> <span data-ttu-id="b5cde-142">Maven kompiliert JAVA-Dateien in CLASS-Dateien oder packt sie zu JAR-Dateien.</span><span class="sxs-lookup"><span data-stu-id="b5cde-142">Maven compiles .java files into .class files or packages them into .jar files.</span></span> <span data-ttu-id="b5cde-143">Maven ist in der Bash Cloud Shell verfügbar. Zum Erstellen der Java-Anwendung verwenden Sie **mvn**-Befehle.</span><span class="sxs-lookup"><span data-stu-id="b5cde-143">Maven is available from the Bash cloud shell; to build the Java application, you use **mvn** commands.</span></span> <span data-ttu-id="b5cde-144">Verwenden Sie diesen mvn-Befehl, um eine Java-Anwendung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="b5cde-144">Use this mvn command to build a Java  application.</span></span>

    ```azurecli
    mvn clean package -DskipTests
    ```

## <a name="summary"></a><span data-ttu-id="b5cde-145">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="b5cde-145">Summary</span></span>

<span data-ttu-id="b5cde-146">Absender- und Empfängeranwendungen müssen mit spezifischen Informationen für die Event Hub-Umgebung konfiguriert werden.</span><span class="sxs-lookup"><span data-stu-id="b5cde-146">Sender and receiver applications must be configured with specific information about the event hub environment.</span></span> <span data-ttu-id="b5cde-147">Sie legen ein Speicherkonto an, wenn Ihre Empfängeranwendung Nachrichten in Blob Storage speichert.</span><span class="sxs-lookup"><span data-stu-id="b5cde-147">You create a storage account if your receiver application stores messages in Blob Storage.</span></span> <span data-ttu-id="b5cde-148">Wenn Ihre Anwendung auf GitHub gehostet wird, müssen Sie sie in Ihr lokales Verzeichnis klonen.</span><span class="sxs-lookup"><span data-stu-id="b5cde-148">If your application is hosted on GitHub, you have to clone it to your local directory.</span></span> <span data-ttu-id="b5cde-149">Texteditoren wie **Nano** werden verwendet, um Ihren Namespace der Anwendung hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="b5cde-149">Text editors, such as **nano** is used to  add your namespace to the application.</span></span>