
<span data-ttu-id="c1209-101">In der vorherigen Übung haben wir mit dem Azure-Portal die folgenden Aufgaben durchgeführt.</span><span class="sxs-lookup"><span data-stu-id="c1209-101">In the previous exercise, we performed the following tasks using the Azure portal.</span></span>

- <span data-ttu-id="c1209-102">Anzeigen des Cachestatus für den Betriebssystemdatenträger</span><span class="sxs-lookup"><span data-stu-id="c1209-102">View OS disk cache status</span></span>
- <span data-ttu-id="c1209-103">Ändern der Cacheeinstellungen des Betriebssystemdatenträgers</span><span class="sxs-lookup"><span data-stu-id="c1209-103">Change the cache settings of the OS disk</span></span>
- <span data-ttu-id="c1209-104">Hinzufügen eines Datenträgers zum virtuellen Computer</span><span class="sxs-lookup"><span data-stu-id="c1209-104">Add a data disk to the VM</span></span>
- <span data-ttu-id="c1209-105">Ändern des Cachetyps auf einem neuen Datenträger</span><span class="sxs-lookup"><span data-stu-id="c1209-105">Change caching type on a new data disk</span></span>

<span data-ttu-id="c1209-106">Wir üben diese Vorgänge nun mit Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1209-106">Let's practice these operations using Azure PowerShell.</span></span> <span data-ttu-id="c1209-107">Wir verwenden den virtuellen Computer, den wir in der vorherigen Übung erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="c1209-107">We're going to use the VM we created in the previous exercise.</span></span> <span data-ttu-id="c1209-108">Für die Vorgänge in dieser Übung wird Folgendes vorausgesetzt:</span><span class="sxs-lookup"><span data-stu-id="c1209-108">The operations in this lab assume:</span></span>

- <span data-ttu-id="c1209-109">Der virtuelle Computer ist vorhanden und hat den Namen **fotoshareVM**.</span><span class="sxs-lookup"><span data-stu-id="c1209-109">Our VM exists and is called **fotoshareVM**</span></span>
- <span data-ttu-id="c1209-110">Der virtuelle Computer ist in einer Ressourcengruppe mit dem Namen **fotoshare-rg** enthalten.</span><span class="sxs-lookup"><span data-stu-id="c1209-110">Our VM lives in a resource group called **fotoshare-rg**</span></span>

<span data-ttu-id="c1209-111">Falls Sie andere Namen verwendet haben, können Sie diese Werte einfach entsprechend ersetzen.</span><span class="sxs-lookup"><span data-stu-id="c1209-111">If you've gone with a different set of names, just replace these values with yours.</span></span> 

<span data-ttu-id="c1209-112">Hier ist der aktuelle Status unserer VM-Datenträger aus der letzten Übung angegeben.</span><span class="sxs-lookup"><span data-stu-id="c1209-112">Here's the current state of our VM disks from the last exercise.</span></span> 

![Screenshot: Betriebssystemdatenträger und Datenträger, jeweils mit schreibgeschütztem Caching](../media-draft/disks-final-config-portal.PNG)

<span data-ttu-id="c1209-114">Wir haben das Portal verwendet, um das Feld **HOSTZWISCHENSPEICHERUNG** für den Betriebssystemdatenträger und den anderen Datenträger festzulegen.</span><span class="sxs-lookup"><span data-stu-id="c1209-114">We used the portal to set the \***HOST CACHING** field for both the OS and data disks.</span></span> <span data-ttu-id="c1209-115">Behalten Sie diesen Ausgangszustand im Hinterkopf, während wir die folgenden Schritte durcharbeiten.</span><span class="sxs-lookup"><span data-stu-id="c1209-115">Keep this initial state in mind as we work through the following steps.</span></span> 

### <a name="set-up-some-variables"></a><span data-ttu-id="c1209-116">Einrichten einiger Variablen</span><span class="sxs-lookup"><span data-stu-id="c1209-116">Set up some variables</span></span>
<span data-ttu-id="c1209-117">Zuerst speichern wir einige Ressourcennamen zur späteren Verwendung.</span><span class="sxs-lookup"><span data-stu-id="c1209-117">First, let's  store some resource names so we can use them later.</span></span>

<span data-ttu-id="c1209-118">Verwenden Sie das Azure Cloud Shell-Terminalfenster auf der rechten Seite, um die folgenden PowerShell-Befehle auszuführen.</span><span class="sxs-lookup"><span data-stu-id="c1209-118">Use the Azure Cloud Shell terminal on the right to run the following Powershell commands.</span></span> 

```powershell
$myRgName = "fotoshare-rg"
$myVMName = "fotoshareVM"
```

> [!TIP]
> <span data-ttu-id="c1209-119">Sie müssen diese Variablen erneut festlegen, wenn der Timeout für Ihre Cloud Shell-Sitzung erreicht ist. Nach Möglichkeit sollten Sie die gesamte Übung also in einer Sitzung durcharbeiten.</span><span class="sxs-lookup"><span data-stu-id="c1209-119">You'll have to set these variables again if your Cloud Shell session times out. So, if possible, work through this entire lab in a single session.</span></span> 

### <a name="get-info-about-our-vm"></a><span data-ttu-id="c1209-120">Abrufen von Informationen zum virtuellen Computer</span><span class="sxs-lookup"><span data-stu-id="c1209-120">Get info about our VM</span></span>

<span data-ttu-id="c1209-121">Führen Sie den folgenden Befehl aus, um die Eigenschaften für den virtuellen Computer zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="c1209-121">Run the following command to get back the properties of our VM.</span></span>
 
```powershell
$myVM = Get-AzureRmVM -ResourceGroupName $myRgName -VMName $myVMName
```
<span data-ttu-id="c1209-122">Wir speichern die Antwort in der Variablen `$myVM`.</span><span class="sxs-lookup"><span data-stu-id="c1209-122">We store the response in our `$myVM` variable.</span></span> <span data-ttu-id="c1209-123">Wir können den folgenden Befehl ausführen, um nur die hier angegebenen Eigenschaften anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="c1209-123">We can run the following command to just show us the properties we specify here.</span></span>

```powershell
$myVM | select-object -property ResourceGroupName, Name, Type, Location
```

<span data-ttu-id="c1209-124">Wie im folgenden Screenshot zu sehen ist, ist dies der gewünschte virtuelle Computer.</span><span class="sxs-lookup"><span data-stu-id="c1209-124">As the following screenshot shows, this VM is indeed the VM we're after.</span></span> <span data-ttu-id="c1209-125">Wir fahren also fort.</span><span class="sxs-lookup"><span data-stu-id="c1209-125">So, let's move on.</span></span> 

![In der PowerShell-Konsole werden die letzten vier Befehle angezeigt, die wir ausgeführt haben.](../media-draft/ps-commands-1.PNG)

### <a name="view-os-disk-cache-status"></a><span data-ttu-id="c1209-127">Anzeigen des Cachestatus für den Betriebssystemdatenträger</span><span class="sxs-lookup"><span data-stu-id="c1209-127">View OS disk cache status</span></span>

<span data-ttu-id="c1209-128">Wir können die Cacheeinstellung wie folgt über das `StorageProfile`-Objekt überprüfen.</span><span class="sxs-lookup"><span data-stu-id="c1209-128">We can check the caching  setting through  the `StorageProfile` object as follows.</span></span>

```powershell
$myVM.StorageProfile.OsDisk.Caching
```
<span data-ttu-id="c1209-129">In diesem Beispiel lautet der aktuelle Wert **None** (Keine).</span><span class="sxs-lookup"><span data-stu-id="c1209-129">In this example, the current value is **None**.</span></span> <span data-ttu-id="c1209-130">Wir ändern ihn wieder in die Standardeinstellung für einen Betriebssystemdatenträger.</span><span class="sxs-lookup"><span data-stu-id="c1209-130">Let's change it back to the default for an OS disk.</span></span>

![PowerShell-Konsole mit dem Cachewert „None“ (Keine) für den Betriebssystemdatenträger](../media-draft/ps-oscaching-none.PNG)

### <a name="change-the-cache-settings-of-the-os-disk"></a><span data-ttu-id="c1209-132">Ändern der Cacheeinstellungen des Betriebssystemdatenträgers</span><span class="sxs-lookup"><span data-stu-id="c1209-132">Change the cache settings of the OS disk</span></span>

<span data-ttu-id="c1209-133">Wir können den Wert für den Cachetyp festlegen, indem wir wie folgt dasselbe StorageProfile-Objekt verwenden.</span><span class="sxs-lookup"><span data-stu-id="c1209-133">We can set the value for the cache type using the same StorageProfile\` object as follows.</span></span>
 
```powershell
$myVM.StorageProfile.OsDisk.Caching = "ReadWrite"
```

<span data-ttu-id="c1209-134">Dieser Befehl wird schneller ausgeführt. Dies deutet darauf hin, dass der Vorgang lokal erfolgt.</span><span class="sxs-lookup"><span data-stu-id="c1209-134">This command runs fast, which should tell you it's doing something locally.</span></span> <span data-ttu-id="c1209-135">Mit dem Befehl wird nur die Eigenschaft für das myVM-Objekt geändert.</span><span class="sxs-lookup"><span data-stu-id="c1209-135">The command just changes the property on the myVM object.</span></span> <span data-ttu-id="c1209-136">Wie im folgenden Screenshot zu sehen ist, gilt Folgendes: Wenn Sie die Variable `$myVM` aktualisieren, hat sich der Cachewert für den virtuellen Computer nicht geändert.</span><span class="sxs-lookup"><span data-stu-id="c1209-136">As the following screenshot shows, if you refresh the `$myVM` variable,  the caching value won't have changed on the VM.</span></span>

![PowerShell-Konsole: Durch die Aktualisierung des „myVM“-Objekts wird die Zwischenspeicherung auf „None“ zurückgesetzt, da der virtuelle Computer nicht aktualisiert wurde.](../media-draft/ps-commands-2.PNG)

<span data-ttu-id="c1209-138">Rufen Sie `Update-AzureRmVM` wie folgt auf, um die Änderung auf dem virtuellen Computer durchzuführen.</span><span class="sxs-lookup"><span data-stu-id="c1209-138">To  make the change on the VM itself, call `Update-AzureRmVM` as follows.</span></span>

```powershell
Update-AzureRmVM -ResourceGroupName $myRGName -VM $myVM
```

<span data-ttu-id="c1209-139">Beachten Sie, dass es eine Weile dauert, bis dieser Aufruf abgeschlossen wurde.</span><span class="sxs-lookup"><span data-stu-id="c1209-139">Notice that this call takes a while to complete.</span></span> <span data-ttu-id="c1209-140">Dies liegt daran, dass wir den eigentlichen virtuellen Computer aktualisieren und Azure den virtuellen Computer neu startet, um die Änderung vorzunehmen.</span><span class="sxs-lookup"><span data-stu-id="c1209-140">That's because we're updating the actual VM and Azure restarts the VM  to make the change.</span></span>

![PowerShell-Konsole mit dem Cachewert „None“ (Keine) für den Betriebssystemdatenträger](../media-draft/ps-oscaching-rw.PNG)

<span data-ttu-id="c1209-142">Wenn Sie die Variable `$myVM` erneut aktualisieren, sehen Sie die Änderung für das Objekt.</span><span class="sxs-lookup"><span data-stu-id="c1209-142">If you refresh the `$myVM` variable again, you'll see the change on the object.</span></span> <span data-ttu-id="c1209-143">Wenn Sie sich den Datenträger im Portal ansehen, können Sie die Änderung dort auch erkennen.</span><span class="sxs-lookup"><span data-stu-id="c1209-143">Looking at the disk in the portal, you'd also see the change there.</span></span> <span data-ttu-id="c1209-144">Wir fahren nun mit dem Erstellen eines neuen Datenträgers fort.</span><span class="sxs-lookup"><span data-stu-id="c1209-144">Ok, let's move on to creating a new data disk.</span></span>  

### <a name="list-data-disk-info"></a><span data-ttu-id="c1209-145">Auflisten von Datenträgerinformationen</span><span class="sxs-lookup"><span data-stu-id="c1209-145">List data disk info</span></span>

<span data-ttu-id="c1209-146">Führen Sie den folgenden Befehl aus, um anzuzeigen, welche für Daten bestimmte Datenträger auf unserem virtuellen Computer vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="c1209-146">To see what data disks we have on our VM, run the following command.</span></span> 

```powershell
$myVM.StorageProfile.DataDisks
```

<span data-ttu-id="c1209-147">Derzeit wird nur ein Datenträger verwendet.</span><span class="sxs-lookup"><span data-stu-id="c1209-147">We've only one data disk at the moment.</span></span> <span data-ttu-id="c1209-148">Das Feld `Lun` ist wichtig.</span><span class="sxs-lookup"><span data-stu-id="c1209-148">The `Lun` field is important.</span></span> <span data-ttu-id="c1209-149">„Lun“ steht für die eindeutige „**L**ogical **U**nit **N**umber“ (Logische Gerätenummer).</span><span class="sxs-lookup"><span data-stu-id="c1209-149">It's the unique **L**ogical **U**nit **N**umber.</span></span> <span data-ttu-id="c1209-150">Wenn wir einen weiteren Datenträger hinzufügen, vergeben wir dafür einen eindeutigen `Lun`-Wert.</span><span class="sxs-lookup"><span data-stu-id="c1209-150">When we add another data disk, we'll give it a unique `Lun` value.</span></span> 

### <a name="add-a-new-data-disk-to-our-vm"></a><span data-ttu-id="c1209-151">Hinzufügen eines neuen Datenträgers zum virtuellen Computer</span><span class="sxs-lookup"><span data-stu-id="c1209-151">Add a new data disk to our VM</span></span> 

<span data-ttu-id="c1209-152">Der Einfachheit halber speichern wir den Namen des neuen Datenträgers.</span><span class="sxs-lookup"><span data-stu-id="c1209-152">For convenience, we'll store our new disk name.</span></span>

```powershell
$newDiskName = "fotoshareVM-data2"
```

<span data-ttu-id="c1209-153">Führen Sie den folgenden Befehl `Add-AzureRmVMDataDisk` aus, um einen neuen Datenträger zu definieren.</span><span class="sxs-lookup"><span data-stu-id="c1209-153">Run the following `Add-AzureRmVMDataDisk` command to define a new disk.</span></span> 

```powershell
Add-AzureRmVMDataDisk -VM $myVM -Name $newDiskName  -LUN 1  -DiskSizeinGB 1 -CreateOption Empty
```

<span data-ttu-id="c1209-154">Wir haben für diesen Datenträger den Lun-Wert „1“ vergeben, da er noch frei ist.</span><span class="sxs-lookup"><span data-stu-id="c1209-154">We've given this disk a Lun value of 1, since that's not taken.</span></span> <span data-ttu-id="c1209-155">Wir haben jetzt den Datenträger definiert, der erstellt werden soll. Es ist also an der Zeit `Update-AzureRmVM` auszuführen, um die eigentliche Änderung vorzunehmen.</span><span class="sxs-lookup"><span data-stu-id="c1209-155">We defined the disk we want to create, so it's time to run `Update-AzureRmVM` to make the actual change.</span></span> 

```powershell
Update-AzureRmVM -ResourceGroupName $myRGName -VM $myVM
```

<span data-ttu-id="c1209-156">Wir sehen uns nun erneut die Datenträgerinformationen an.</span><span class="sxs-lookup"><span data-stu-id="c1209-156">Let's look at our data disk info again.</span></span>

```powershell
$myVM.StorageProfile.DataDisks
```

![PowerShell-Konsole mit zwei Datenträgern für Daten](../media-draft/2-data-disks-part1.png)

<span data-ttu-id="c1209-158">Wir verfügen jetzt über zwei Datenträger.</span><span class="sxs-lookup"><span data-stu-id="c1209-158">We now have two disks.</span></span> <span data-ttu-id="c1209-159">Der neue Datenträger hat den **Lun**-Wert „1“, und der Standardwert für **Caching** lautet **None** (Keine).</span><span class="sxs-lookup"><span data-stu-id="c1209-159">Our new disk has a **Lun** of 1 and the default value for **Caching** is **None**.</span></span> <span data-ttu-id="c1209-160">Wir ändern diesen Wert.</span><span class="sxs-lookup"><span data-stu-id="c1209-160">Let's change that value.</span></span>

### <a name="change-cache-settings-of-new-data-disk"></a><span data-ttu-id="c1209-161">Ändern der Cacheeinstellungen des neuen Datenträgers</span><span class="sxs-lookup"><span data-stu-id="c1209-161">Change cache settings of new data disk</span></span>

<span data-ttu-id="c1209-162">Wir ändern die Eigenschaften eines VM-Datenträgers wie folgt mit dem Cmdlet `Set-AzureRmVMDataDisk`.</span><span class="sxs-lookup"><span data-stu-id="c1209-162">We modify properties of a virtual machine data disk with the `Set-AzureRmVMDataDisk` cmdlet as follows.</span></span>

```powershell
Set-AzureRmVMDataDisk -Lun "1" -Caching ReadWrite
```

<span data-ttu-id="c1209-163">Die Änderungen committen wir wie immer mit `Update-AzureRmVM`.</span><span class="sxs-lookup"><span data-stu-id="c1209-163">As always, commit the changes with `Update-AzureRmVM`.</span></span>

```powershell
Update-AzureRmVM -ResourceGroupName $myRGName -VM $myVM
```

<span data-ttu-id="c1209-164">Hier ist eine Ansicht aus dem Portal angegeben, die verdeutlicht, was wir in dieser Übung erreicht haben.</span><span class="sxs-lookup"><span data-stu-id="c1209-164">Here's a view from the portal of what we've accomplished in this exercise.</span></span> <span data-ttu-id="c1209-165">Der virtuelle Computer verfügt nun über zwei Datenträger für Daten, und wir haben die Einstellungen für **Hostzwischenspeicherung** angepasst.</span><span class="sxs-lookup"><span data-stu-id="c1209-165">Our VM now has two data disks and we've adjust all **HOST Caching** settings.</span></span> <span data-ttu-id="c1209-166">Hierfür haben wir nur wenige Befehle benötigt.</span><span class="sxs-lookup"><span data-stu-id="c1209-166">We did all of that with just a few commands.</span></span> <span data-ttu-id="c1209-167">Dies liegt an der hohen Leistungsfähigkeit von Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1209-167">That's the power of Azure PowerShell.</span></span>

![PowerShell-Konsole mit zwei Datenträgern für Daten](../media-draft/disks-final-config-portal2.png)
