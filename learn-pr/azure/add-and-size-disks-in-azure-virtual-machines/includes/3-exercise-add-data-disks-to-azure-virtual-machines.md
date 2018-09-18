<span data-ttu-id="6e65e-101">In dieser Übung wird angenommen, dass Ihr Unternehmen einen SMTP-E-Mail-Server (Simple Mail Transfer Protocol) verwendet.</span><span class="sxs-lookup"><span data-stu-id="6e65e-101">In this exercise, let's assume your company runs a Simple Mail Transfer Protocol (SMTP) email server.</span></span> <span data-ttu-id="6e65e-102">Sie möchten diesen Server zu Azure migrieren.</span><span class="sxs-lookup"><span data-stu-id="6e65e-102">You want to migrate this server into Azure.</span></span> <span data-ttu-id="6e65e-103">Sie möchten eingehende Nachrichten für Ihre eigene Domäne auf dem SMTP-Server in einem Ordner namens „Drop“ auf einer dedizierten VHD speichern.</span><span class="sxs-lookup"><span data-stu-id="6e65e-103">You want the SMTP server to store incoming messages for your own domain in a folder called "Drop" on a dedicated VHD.</span></span>

<span data-ttu-id="6e65e-104">Das Ziel dieser Übung ist, einen virtuellen Windows-Computer (VM) zu erstellen und eine neue virtuelle Festplatte (VHD) namens „Incoming“ für das Verzeichnis „Drop“ anzufügen.</span><span class="sxs-lookup"><span data-stu-id="6e65e-104">The goal of the exercise is to create a Windows virtual machine (VM) and attach a new virtual hard disk (VHD) called "Incoming" to store the "Drop" directory.</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="6e65e-105">Anmelden bei Azure</span><span class="sxs-lookup"><span data-stu-id="6e65e-105">Sign in to Azure</span></span>
<!---TODO: Need update for sanbox?--->

1. <span data-ttu-id="6e65e-106">Melden Sie sich beim [Azure-Portal](https://portal.azure.com/?azure-portal=true) an.</span><span class="sxs-lookup"><span data-stu-id="6e65e-106">Sign in to the [Azure portal](https://portal.azure.com/?azure-portal=true).</span></span>

## <a name="create-a-windows-vm-in-the-azure-portal"></a><span data-ttu-id="6e65e-107">Erstellen einer Windows-VM im Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="6e65e-107">Create a Windows VM in the Azure portal</span></span>

<span data-ttu-id="6e65e-108">Um eine VM zum Hosten des SMTP-Servers mit den Datenlaufwerken zu erstellen, gehen Sie folgendermaßen vor:</span><span class="sxs-lookup"><span data-stu-id="6e65e-108">To create a VM to host the SMTP server with its data drives, follow these steps:</span></span>

1. <span data-ttu-id="6e65e-109">Wählen Sie im Azure-Portal oben links **Ressource erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-109">Choose **Create a resource** in the upper left corner of the Azure portal.</span></span>

1. <span data-ttu-id="6e65e-110">Suchen Sie im Suchfeld oberhalb der Liste der Azure Marketplace-Ressourcen nach **Windows Server 2016 Datacenter**, und wählen Sie dann **Erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-110">In the search box above the list of Azure Marketplace resources, search for and select **Windows Server 2016 Datacenter**, and then choose **Create**.</span></span>

1. <span data-ttu-id="6e65e-111">Geben Sie im Bereich **Grundlagen**, der auf der rechten Seite geöffnet wird, die folgenden Eigenschaftswerte ein.</span><span class="sxs-lookup"><span data-stu-id="6e65e-111">In the **Basics** pane that opens to the right, enter the following property values.</span></span> 


|<span data-ttu-id="6e65e-112">Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="6e65e-112">Property</span></span>  |<span data-ttu-id="6e65e-113">Wert</span><span class="sxs-lookup"><span data-stu-id="6e65e-113">Value</span></span>  |<span data-ttu-id="6e65e-114">Hinweise</span><span class="sxs-lookup"><span data-stu-id="6e65e-114">Notes</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="6e65e-115">Name</span><span class="sxs-lookup"><span data-stu-id="6e65e-115">Name</span></span>     |   <span data-ttu-id="6e65e-116">**MailSenderVM**</span><span class="sxs-lookup"><span data-stu-id="6e65e-116">**MailSenderVM**</span></span>      |         |
|<span data-ttu-id="6e65e-117">VM-Datenträgertyp</span><span class="sxs-lookup"><span data-stu-id="6e65e-117">VM disk type</span></span>     |  <span data-ttu-id="6e65e-118">**HDD Standard**</span><span class="sxs-lookup"><span data-stu-id="6e65e-118">**Standard HDD**</span></span>       |   <span data-ttu-id="6e65e-119">Wählen Sie diesen Wert aus der Dropdownliste aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-119">Select this value from the dropdown.</span></span>      |
|<span data-ttu-id="6e65e-120">Benutzername</span><span class="sxs-lookup"><span data-stu-id="6e65e-120">User name</span></span>     |  <span data-ttu-id="6e65e-121">**mailmaster**</span><span class="sxs-lookup"><span data-stu-id="6e65e-121">**mailmaster**</span></span>       |         |
|<span data-ttu-id="6e65e-122">Kennwort</span><span class="sxs-lookup"><span data-stu-id="6e65e-122">Password</span></span>     |  <span data-ttu-id="6e65e-123">Das Kennwort muss mindestens zwölf Zeichen lang sein und die [definierten Anforderungen an die Komplexität](https://docs.microsoft.com/azure/virtual-machines/windows/faq#what-are-the-password-requirements-when-creating-a-vm) erfüllen.</span><span class="sxs-lookup"><span data-stu-id="6e65e-123">The password must be at least 12 characters long and meet the [defined complexity requirements](https://docs.microsoft.com/azure/virtual-machines/windows/faq#what-are-the-password-requirements-when-creating-a-vm).</span></span>       | <span data-ttu-id="6e65e-124">Sie müssen sich diesen Benutzernamen und das Kennwort merken, da beides im gesamten Modul verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="6e65e-124">Make sure to remember this user name and password because we'll use them throughout the module.</span></span>         |
|<span data-ttu-id="6e65e-125">Abonnement</span><span class="sxs-lookup"><span data-stu-id="6e65e-125">Subscription</span></span>     |  <span data-ttu-id="6e65e-126">Wählen Sie Ihr Abonnement aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-126">Choose your subscription.</span></span>       |  <span data-ttu-id="6e65e-127">Wählen Sie diesen Wert aus der Dropdownliste aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-127">Select this value from the dropdown.</span></span>       |
|<span data-ttu-id="6e65e-128">Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="6e65e-128">Resource group</span></span>     |  <span data-ttu-id="6e65e-129">Klicken Sie auf **Neu erstellen**, und geben Sie dann **MailInfrastructure** ein.</span><span class="sxs-lookup"><span data-stu-id="6e65e-129">Select **Create new**, and then type **MailInfrastructure**.</span></span>       |  <span data-ttu-id="6e65e-130">Wir sammeln alle Ressourcen, die in diesem Modul verwendet werden, in einer Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="6e65e-130">We'll gather all resource used in this module into one resource group.</span></span>       |
|<span data-ttu-id="6e65e-131">Standort</span><span class="sxs-lookup"><span data-stu-id="6e65e-131">Location</span></span>     |   <span data-ttu-id="6e65e-132">Ein Standort in Ihrer Nähe.</span><span class="sxs-lookup"><span data-stu-id="6e65e-132">A location near you.</span></span>      | <span data-ttu-id="6e65e-133">Wählen Sie diesen Wert aus der Dropdownliste aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-133">Select this value from the dropdown.</span></span>        |

4. <span data-ttu-id="6e65e-134">Wählen Sie unten auf der Seite **Grundlagen** die Option **OK** aus, um mit dem Konfigurationsbereich **Größe** fortzufahren.</span><span class="sxs-lookup"><span data-stu-id="6e65e-134">Select **OK** at the bottom of the **Basics** page to continue to the **Size** configuration pane.</span></span>

1. <span data-ttu-id="6e65e-135">Suchen Sie im Konfigurationsbereich **Größe** nach **B1ms**, und wählen Sie sie aus, und klicken Sie dann auf **Auswählen**.</span><span class="sxs-lookup"><span data-stu-id="6e65e-135">In the **Size** configuration pane, search for and select **B1ms**, and then click **Select**.</span></span>

1. <span data-ttu-id="6e65e-136">Klicken Sie im Bereich **Einstellungen** unter **Verwaltete Datenträger verwenden** auf **Nein**.</span><span class="sxs-lookup"><span data-stu-id="6e65e-136">In the **Settings** pane, under **Use managed disks**, click **No**.</span></span> <span data-ttu-id="6e65e-137">Verwaltete Datenträger werden später in diesem Modul erörtert.</span><span class="sxs-lookup"><span data-stu-id="6e65e-137">We'll discuss managed disks later in this module.</span></span>

1. <span data-ttu-id="6e65e-138">Wählen Sie in der Dropdownliste **Öffentliche Eingangsports hinzufügen** den Port **RDP (3389)** aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-138">In the **Select public inbound ports** dropdown list, select **RDP (3389)**.</span></span> <span data-ttu-id="6e65e-139">Wir verwenden diesen Port für den Remotezugriff auf die VM, nachdem sie erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="6e65e-139">We'll use this port to remote into our VM after it's created.</span></span>

1. <span data-ttu-id="6e65e-140">Behalten Sie für alle anderen Einstellungen die Standardwerte bei, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="6e65e-140">Leave all the other settings at their default, and then click **OK**.</span></span>

1. <span data-ttu-id="6e65e-141">Prüfen Sie im Bereich **Erstellen** die Konfiguration.</span><span class="sxs-lookup"><span data-stu-id="6e65e-141">In the **Create** pane, review the configuration.</span></span>

1. <span data-ttu-id="6e65e-142">Wenn Sie die Konfiguration geprüft haben, wählen Sie **Erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-142">When you have reviewed the configuration,  select **Create**.</span></span> <span data-ttu-id="6e65e-143">Azure erstellt und startet die neue VM.</span><span class="sxs-lookup"><span data-stu-id="6e65e-143">Azure creates and starts the new VM.</span></span>

> [!TIP]
> <span data-ttu-id="6e65e-144">Das Erstellen Ihrer VM und deren Bereitstellung in Azure kann einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="6e65e-144">Creating your VM and deploying it in Azure can take a few minutes.</span></span> <span data-ttu-id="6e65e-145">Sie können den Fortschritt im Hub **Benachrichtigungen** überwachen.</span><span class="sxs-lookup"><span data-stu-id="6e65e-145">You can watch the progress in the **Notifications** hub.</span></span> <span data-ttu-id="6e65e-146">Beim Abschluss zeigt Azure ein Benachrichtigungsdialogfeld an.</span><span class="sxs-lookup"><span data-stu-id="6e65e-146">Azure will display a notification dialog when it finishes.</span></span>

## <a name="add-an-empty-data-disk-to-our-vm"></a><span data-ttu-id="6e65e-147">Hinzufügen eines leeren Datenträgers zur VM</span><span class="sxs-lookup"><span data-stu-id="6e65e-147">Add an empty data disk to our VM</span></span>

<span data-ttu-id="6e65e-148">Wir nennen den Datenträger, auf dem das Verzeichnis „Drop“ für den SMTP-Server gespeichert wird, „Incoming“.</span><span class="sxs-lookup"><span data-stu-id="6e65e-148">We're going to name the disk stores the "Drop" directory for your SMTP server "Incoming".</span></span> <span data-ttu-id="6e65e-149">Fügen Sie mit den folgenden Schritten dem Server einen neuen leeren Datenträger hinzu:</span><span class="sxs-lookup"><span data-stu-id="6e65e-149">Let's add a new empty disk to the server using the following steps:</span></span>

1. <span data-ttu-id="6e65e-150">Wählen Sie im Navigationsbereich auf der linken Seite unter **FAVORITEN** die Option **Virtuelle Computer** aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-150">In the navigation on the left, under **FAVORITES**, select **Virtual machines**.</span></span>

1. <span data-ttu-id="6e65e-151">Wählen Sie in der Liste der VMs **MailSenderVM** aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-151">In the list of VMs, select **MailSenderVM**.</span></span>

1. <span data-ttu-id="6e65e-152">Wählen Sie auf der linken Seite im Konfigurationsmenü von **MailSenderVM** unter **EINSTELLUNGEN** die Option **Datenträger** aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-152">Under **SETTINGS** of the **MailSenderVM** configuration menu on the left, select **Disks**.</span></span>

1. <span data-ttu-id="6e65e-153">Wählen Sie unter **Datenträger** die Option **Datenträger hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-153">Under **Data disks**, select **Add data disk**.</span></span>

1. <span data-ttu-id="6e65e-154">Legen Sie im Bereich **Nicht verwaltete Datenträger anfügen** die folgenden Eigenschaften fest.</span><span class="sxs-lookup"><span data-stu-id="6e65e-154">In the **Attach unmanaged disks** pane, set the following properties.</span></span>


|<span data-ttu-id="6e65e-155">Eigenschaft</span><span class="sxs-lookup"><span data-stu-id="6e65e-155">Property</span></span>  |<span data-ttu-id="6e65e-156">Wert</span><span class="sxs-lookup"><span data-stu-id="6e65e-156">Value</span></span>  |<span data-ttu-id="6e65e-157">Hinweise</span><span class="sxs-lookup"><span data-stu-id="6e65e-157">Notes</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="6e65e-158">Name</span><span class="sxs-lookup"><span data-stu-id="6e65e-158">Name</span></span>     |   <span data-ttu-id="6e65e-159">**MailSenderVMIncoming**</span><span class="sxs-lookup"><span data-stu-id="6e65e-159">**MailSenderVMIncoming**</span></span>      |         |
|<span data-ttu-id="6e65e-160">Quelltyp</span><span class="sxs-lookup"><span data-stu-id="6e65e-160">Source type</span></span>     |  <span data-ttu-id="6e65e-161">**Neu (leerer Datenträger)**</span><span class="sxs-lookup"><span data-stu-id="6e65e-161">**New (empty disk)**</span></span>       |   <span data-ttu-id="6e65e-162">Wählen Sie diesen Wert aus der Dropdownliste aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-162">Select this value from the dropdown.</span></span>       |
|<span data-ttu-id="6e65e-163">Kontotyp</span><span class="sxs-lookup"><span data-stu-id="6e65e-163">Account type</span></span>     |  <span data-ttu-id="6e65e-164">**HDD Standard**</span><span class="sxs-lookup"><span data-stu-id="6e65e-164">**Standard HDD**</span></span>       |  <span data-ttu-id="6e65e-165">Wählen Sie diesen Wert aus der Dropdownliste aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-165">Select this value from the dropdown.</span></span>        |


6. <span data-ttu-id="6e65e-166">Wählen Sie links neben dem Feld **Speichercontainer** die Option **Durchsuchen** aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-166">To the left of the **Storage container** field, select **Browse**.</span></span>

1. <span data-ttu-id="6e65e-167">Suchen Sie in der Liste der Speicherkonten nach dem Speicherkonto, dessen Name mit **mailinfrastructure** beginnt, und wählen Sie es aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-167">In the list of storage accounts, search for the storage account whose name begins with **mailinfrastructure** and select it.</span></span>

1. <span data-ttu-id="6e65e-168">Klicken Sie in der Liste der Container auf **VHDs**, und wählen Sie dann **Auswählen** aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-168">In the list of containers, click **vhds** and then choose **Select**.</span></span>

1. <span data-ttu-id="6e65e-169">Wählen Sie auf dem Bildschirm **Nicht verwalteten Datenträger anfügen** die Option **OK** aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-169">Back on the **Attach unmanaged disk** screen, select **OK**.</span></span>

1. <span data-ttu-id="6e65e-170">Wählen Sie auf dem Bildschirm **MailSenderVM – Datenträger** die Option **Speichern** aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-170">Back on the **MailSenderVM - Disks** screen, select **Save**.</span></span>

<span data-ttu-id="6e65e-171">Wir haben jetzt einen Datenträger namens **MainSenderVMIncoming** definiert.</span><span class="sxs-lookup"><span data-stu-id="6e65e-171">We've now defined a disk called **MainSenderVMIncoming**.</span></span> <span data-ttu-id="6e65e-172">Um den Datenträger zu verwenden, müssen wir ihn zunächst partitionieren und formatieren, wenn wir uns bei der VM anmelden.</span><span class="sxs-lookup"><span data-stu-id="6e65e-172">To use the disk, we'll first need to partition and format it when we log into the VM.</span></span> 

## <a name="partition-and-format-a-data-disk"></a><span data-ttu-id="6e65e-173">Partitionieren und Formatieren eines Datenträgers</span><span class="sxs-lookup"><span data-stu-id="6e65e-173">Partition and format a data disk</span></span>

<span data-ttu-id="6e65e-174">Wie bei physischen Datenträgern müssen Sie auf einer VHD eine Partition initialisieren und formatieren, bevor sie verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="6e65e-174">As with physical disks, initiate and format a partition on a VHD before it can be used.</span></span>

### <a name="log-into-our-windows-vm-using-rdp"></a><span data-ttu-id="6e65e-175">Anmelden bei der Windows-VM über RDP</span><span class="sxs-lookup"><span data-stu-id="6e65e-175">Log into our Windows VM using RDP</span></span>

1. <span data-ttu-id="6e65e-176">Wählen Sie auf dem Hauptbildschirm des virtuellen Computers **MailSenderVM** die Option **Übersicht** aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-176">In the **MailSenderVM** virtual machine main screen, select **Overview**.</span></span>

1. <span data-ttu-id="6e65e-177">Wählen Sie auf dem Übersichtsbildschirm oben links **Verbinden** aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-177">Select **Connect** from the top left of the overview screen.</span></span>

1. <span data-ttu-id="6e65e-178">Wählen Sie im Dialogfeld **Herstellen einer Verbindung mit dem virtuellen Computer** auf der rechten Seite **RDP-Datei herunterladen** aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-178">In the **Connect to virtual machine** dialog that opens on the right, select **Download to RDP File**.</span></span>

   ![Screenshot des Dialogfelds „Herstellen einer Verbindung mit dem virtuellen Computer“ mit hervorgehobener Schaltfläche „RDP-Datei herunterladen“.](../media-draft/download-rdp.png)

4. <span data-ttu-id="6e65e-180">Eine Datei namens **MailSenderVM.rdp** wird in Ihren lokalen Ordner `Downloads` heruntergeladen.</span><span class="sxs-lookup"><span data-stu-id="6e65e-180">A file called **MailSenderVM.rdp** is downloaded to your local `Downloads` folder.</span></span> <span data-ttu-id="6e65e-181">Diese Datei ist die Datei mit der Remotedesktopkonfiguration für den virtuellen Computer „MailSenderVM“.</span><span class="sxs-lookup"><span data-stu-id="6e65e-181">This file is the remote desktop configuration file for the MailSenderVM virtual machine.</span></span> <span data-ttu-id="6e65e-182">Öffnen Sie die Datei, um die Verbindung herzustellen.</span><span class="sxs-lookup"><span data-stu-id="6e65e-182">Open the file to start the connection process.</span></span>

1. <span data-ttu-id="6e65e-183">Klicken Sie im Dialogfeld **Remotedesktopverbindung** auf **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="6e65e-183">In the **Remote Desktop Connection** dialog, click **Connect**.</span></span>

1. <span data-ttu-id="6e65e-184">Klicken Sie im Dialogfeld **Windows-Sicherheit** auf **Anderes Konto verwenden**.</span><span class="sxs-lookup"><span data-stu-id="6e65e-184">In the **Windows Security** dialog, click **Use another account**.</span></span>

1. <span data-ttu-id="6e65e-185">Geben Sie im Textfeld **Benutzername** den Text **mailmaster** ein.</span><span class="sxs-lookup"><span data-stu-id="6e65e-185">In the **Username** textbox, type **mailmaster**.</span></span>

1. <span data-ttu-id="6e65e-186">Geben Sie im Textfeld **Kennwort** das Kennwort ein, das Sie in dieser Übung für diesen Benutzernamen eingegeben haben.</span><span class="sxs-lookup"><span data-stu-id="6e65e-186">In the **Password** textbox, type the password you entered for this user name in this exercise.</span></span> 

1. <span data-ttu-id="6e65e-187">Klicken Sie im Dialogfeld **Remotedesktopverbindung** auf **Ja**.</span><span class="sxs-lookup"><span data-stu-id="6e65e-187">In the **Remote Desktop Connection** dialog, click **Yes**.</span></span>

<span data-ttu-id="6e65e-188">Eine Remotedesktopsitzung mit dem virtuellen Computer wird gestartet.</span><span class="sxs-lookup"><span data-stu-id="6e65e-188">A remote desktop session to the virtual machine is now started.</span></span> <span data-ttu-id="6e65e-189">Die erste Anmeldung kann einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="6e65e-189">It might take a few moments to sign in for the first time.</span></span> <span data-ttu-id="6e65e-190">Wenn die Anmeldung abgeschlossen ist, wird das Tool **Server-Manager** auf dem Bildschirm angezeigt.</span><span class="sxs-lookup"><span data-stu-id="6e65e-190">When sign-in is finished, the **Server Manager** tool will be displayed on the screen.</span></span>

### <a name="partition-and-format-our-data-disk-using-server-manager"></a><span data-ttu-id="6e65e-191">Partitionieren und Formatieren des Datenträgers mit dem Server-Manager</span><span class="sxs-lookup"><span data-stu-id="6e65e-191">Partition and format our data disk using Server Manager</span></span>

1. <span data-ttu-id="6e65e-192">Wenn **Server-Manager** angezeigt wird, wählen im Navigationsbereich auf der linken Seite **Datei- und Speicherdienste** aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-192">When **Server Manager** is displayed, select **File and Storage Services** in the navigation on the left.</span></span>

1. <span data-ttu-id="6e65e-193">Wählen Sie unter **Volumes** die Option **Datenträger** aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-193">Under **Volumes**, select **Disks**.</span></span>

1. <span data-ttu-id="6e65e-194">In der Liste der Datenträger ist der Datenträger **0** der Betriebssystemdatenträger, und der Datenträger **1** ist der temporäre Datenträger.</span><span class="sxs-lookup"><span data-stu-id="6e65e-194">In the list of disks, disk **0** is the operating system disk and disk **1** is the temporary disk.</span></span> <span data-ttu-id="6e65e-195">Wählen Sie den Datenträger **2** aus. Dies ist die VHD, die Sie gerade hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="6e65e-195">Select disk **2**, which is the new VHD you just added.</span></span>

1. <span data-ttu-id="6e65e-196">Wählen Sie oben im Bereich **VOLUMES** die Option **AUFGABEN** und dann **Neues Volume** aus. Das Menü befindet sich oben rechts auf dem Bildschirm.</span><span class="sxs-lookup"><span data-stu-id="6e65e-196">At the top of the **VOLUMES** pane, select **TASKS** followed by **New Volume...**. The menu is in the top right of the screen as follows.</span></span>

   ![Screenshot des erweiterten Menüs „AUFGABEN“ mit drei Menüelementen.](../media-draft/tasks-menu.png)


1. <span data-ttu-id="6e65e-199">Klicken Sie im Assistenten **Neues Volume** auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="6e65e-199">In the **New Volume** wizard, click **Next**.</span></span>

1. <span data-ttu-id="6e65e-200">Wählen Sie auf der Seite **Server und Datenträger auswählen** die Einträge **MailSenderVM** und **Datenträger 2** aus, und klicken Sie dann auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="6e65e-200">In the **Select server and disk** page, select **MailSenderVM** and **Disk 2**, and then click **Next**.</span></span>

1. <span data-ttu-id="6e65e-201">Klicken Sie im Dialogfeld **Datenträger offline oder nicht initialisiert** auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="6e65e-201">In the **Offline or Uninitiated Disk** dialog, click **OK**.</span></span>

1. <span data-ttu-id="6e65e-202">Klicken Sie auf der Seite **Geben Sie die Größe des Volumes an** auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="6e65e-202">In the **Specify the size of the volume** page, click **Next**.</span></span>

1. <span data-ttu-id="6e65e-203">Wählen Sie auf der Seite **Einen Laufwerkbuchstaben zuweisen** den Buchstaben **F:** und dann **Weiter** aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-203">In the **Assign a drive letter** page, select **F:** followed by **Next**.</span></span>

1. <span data-ttu-id="6e65e-204">Geben Sie auf der Seite **Dateisystemeinstellungen auswählen** im Textfeld **Volumebezeichnung** den Namen **Incoming** ein, und wählen Sie dann **Weiter** aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-204">In the **Select file system settings** page, in the **Volume label** textbox, type **Incoming** and then select **Next**.</span></span>

1. <span data-ttu-id="6e65e-205">Wählen Sie auf der Seite **Auswahl bestätigen** die Option **Erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-205">In the **Confirm selections** page, select **Create**.</span></span> <span data-ttu-id="6e65e-206">Windows initialisiert den Datenträger und formatiert die neue Partition.</span><span class="sxs-lookup"><span data-stu-id="6e65e-206">Windows initiates the disk and formats the new partition.</span></span>

1. <span data-ttu-id="6e65e-207">Wählen Sie auf der Seite **Abschluss** die Option **Schließen** aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-207">In the **Completion** page, select **Close**.</span></span>

<span data-ttu-id="6e65e-208">Sehen wir uns das neue Datenträgervolume im Datei-Explorer an.</span><span class="sxs-lookup"><span data-stu-id="6e65e-208">Let's have a look at our new disk volume in File Explorer.</span></span> 
1. <span data-ttu-id="6e65e-209">Öffnen Sie den **Datei-Explorer**.</span><span class="sxs-lookup"><span data-stu-id="6e65e-209">Open **File Explorer**.</span></span>

1. <span data-ttu-id="6e65e-210">Klicken Sie im Navigationsbereich auf der linken Seite auf **Dieser PC**, und doppelklicken Sie dann auf **Incoming (F:)**.</span><span class="sxs-lookup"><span data-stu-id="6e65e-210">In the navigation in the left, click **This PC** and then double-click **Incoming (F:)**.</span></span>

1. <span data-ttu-id="6e65e-211">Wählen Sie **Start** und dann **Neuer Ordner** aus.</span><span class="sxs-lookup"><span data-stu-id="6e65e-211">Select **Home**, and then **New Folder**.</span></span>

1. <span data-ttu-id="6e65e-212">Geben Sie **Drop** ein, und drücken Sie dann die EINGABETASTE.</span><span class="sxs-lookup"><span data-stu-id="6e65e-212">Type **Drop** and then press Enter.</span></span>

<span data-ttu-id="6e65e-213">Wir haben jetzt auf der VHD ein neues Volume namens **Incoming** und auf dem Volume einen Ordner namens **Drop** erstellt.</span><span class="sxs-lookup"><span data-stu-id="6e65e-213">We now have a new volume created on our VHD called **Incoming**, and we've created a folder called **Drop** on that volume.</span></span>  

1. <span data-ttu-id="6e65e-214">Schließen Sie Windows-Explorer.</span><span class="sxs-lookup"><span data-stu-id="6e65e-214">Close Windows Explorer.</span></span>

1. <span data-ttu-id="6e65e-215">Klicken Sie auf der **Taskleiste** auf die Schaltfläche **Start**, klicken Sie auf die Schaltfläche **Ein/Aus**, und klicken Sie dann auf **Trennen**.</span><span class="sxs-lookup"><span data-stu-id="6e65e-215">On the **Task Bar**, click the **Start** button, click the **Power** button, and then click **Disconnect**.</span></span>

<span data-ttu-id="6e65e-216">Herzlichen Glückwunsch!</span><span class="sxs-lookup"><span data-stu-id="6e65e-216">Congratulations!</span></span> <span data-ttu-id="6e65e-217">Sie haben erfolgreich eine Windows-VM erstellt, eine neue VHD angefügt, auf der VHD ein Volume erstellt und dem Volume einen Ordner hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="6e65e-217">You've successfully created a Windows VM, attached a new VHD, created a volume on that VHD and added a folder to that volume.</span></span> <span data-ttu-id="6e65e-218">Der Datenträgertyp, den wir für die neue VHD verwendet haben, war **HDD Standard**.</span><span class="sxs-lookup"><span data-stu-id="6e65e-218">If you recall, the disk type we used for the new VHD was a **Standard HDD**.</span></span> <span data-ttu-id="6e65e-219">In der nächsten Einheit lernen Sie die Unterschiede zwischen Standardspeicher und Storage Premium kennen.</span><span class="sxs-lookup"><span data-stu-id="6e65e-219">In the next unit, we'll learn the differences between standard and premium storage.</span></span> 
