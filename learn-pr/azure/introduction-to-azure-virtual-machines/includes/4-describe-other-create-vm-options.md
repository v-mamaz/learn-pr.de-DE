Das Azure-Portal ist der einfachste Weg, um anfangs Ressourcen wie VMs zu erstellen. Allerdings stellt Azure nicht unbedingt die effizienteste oder schnellste Möglichkeit dar, insbesondere wenn Sie mehrere Ressourcen gleichzeitig erstellen möchten. In unserem Fall werden wir Dutzende von VMs erstellen, um verschiedene Aufgaben zu verarbeiten. Es wäre umständlich und lästig, sie manuell im Azure-Portal zu erstellen.

Betrachten wir einige andere Methoden, um Ressourcen in Azure zu erstellen und zu verwalten:

- [Azure Resource Manager](#Azure_RM)
- [Azure PowerShell](#Azure_PowerShell)
- [Azure CLI](#Azure_CLI)
- [Azure-REST-API](#Azure_REST_API)
- [Azure-Client SDK](#Azure_Client_SDK)
- [Azure-VM-Erweiterungen](#Azure_VMExtensions)
- [Azure Automation-Dienste](#Azure_Automation)

<a name="Azure_RM" />

## <a name="azure-resource-manager"></a>Azure Resource Manager

Angenommen Sie wollen eine Kopie einer VM mit den gleichen Einstellungen erstellen. Dafür könnten Sie ein VM-Image erstellen, es in Azure hochladen und als Grundlage für Ihre neue VM verwenden. Dieses Vorgehen ist jedoch ineffizient und zeitaufwändig. Azure bietet Ihnen die Möglichkeit, eine Vorlage zu erstellen, aus der Sie eine genaue Kopie einer VM erstellen können.

In der Regel enthält Ihre Azure-Infrastruktur viele Ressourcen, von denen viele in irgendeiner Weise miteinander verbunden sind. Beispielsweise verfügt die von uns erstellte VM über den virtuellen Computer selbst, Speicher, Netzwerkschnittstelle, Webserver und eine Datenbank – allesamt erstellt, um die WordPress-Website auszuführen. Der **Azure Resource Manager** macht die Arbeit mit diesen verknüpften Ressourcen effizienter. Er fasst Ressourcen in benannten **Ressourcengruppen** zusammen, über die Sie alle Ressourcen gleichzeitig bereitstellen, aktualisieren oder löschen können. Beim Erstellen der WordPress-Website wurde die Ressourcengruppe als Teil der VM-Erstellung identifiziert, und der Resource Manager hat die zugehörigen Ressourcen in derselben Gruppe platziert.

Mithilfe des Resource Managers können Sie auch _Vorlagen_ zum Erstellen und Bereitstellen bestimmter Konfigurationen erstellen.

### <a name="what-are-resource-manager-templates"></a>Was sind Resource Manager-Vorlagen?

**Resource Manager-Vorlagen** sind JSON-Dateien, mit denen die Ressourcen definiert werden, die Sie für Ihre Lösung bereitstellen müssen.

Sie können diese Vorlagen im Abschnitt **Einstellungen** für eine bestimmte VM erstellen, indem Sie die Option „Automatisierungsskript“ auswählen.

![Automatisierungsskript für die VM](../media-draft/4-automation-script.png)

Sie haben die Möglichkeit, die Resource Manager-Vorlage für die spätere Verwendung zu speichern oder direkt eine neue VM auf Basis dieser Vorlage bereitzustellen. Wenn Sie beispielsweise eine VM aus einer Vorlage in einer Testumgebung erstellen und feststellen, dass sie Ihren lokalen Computer nicht ganz ersetzt, können Sie wie folgt vorgehen: Löschen Sie die Ressourcengruppe, wodurch alle Ressourcen gelöscht werden, optimieren Sie die Vorlage, und versuchen Sie es dann erneut. Wenn Sie nur Änderungen an den vorhandenen bereitgestellten Ressourcen vornehmen möchten, können Sie die Vorlage, mit der sie erstellt wurden, ändern und erneut bereitstellen. Resource Manager ändert die Ressourcen entsprechend der neuen Vorlage.

Sobald alles Ihren Vorstellungen entspricht, können Sie mit dieser Vorlage mehrere Versionen Ihrer Infrastruktur erstellen, z.B. für das Staging und die Produktion. Sie können Felder wie „VM-Name“, „Netzwerkname“ und „Speicherkontoname“ parametrisieren und die Vorlage mit verschiedenen Parametern wiederholt laden, um die jeweilige Umgebung anzupassen.

Mithilfe von Tools zur automatischen Skripterstellung, z.B. die Azure CLI, Azure PowerShell oder sogar Azure-REST-APIs, können Sie Resource Manager-Vorlagen mit der von Ihnen bevorzugten Programmiersprache verarbeiten und auf diese Weise schnell eine Infrastruktur erstellen.

<a name="Azure_PowerShell" />

## <a name="azure-powershell"></a>Azure PowerShell

Verwaltungsskripts stellen eine ausgezeichnete Möglichkeit dar, Ihren Workflow zu optimieren. Sie können alltägliche, sich wiederholende Aufgaben automatisieren, und nachdem ein Skript überprüft wurde, wird es konsistent ausgeführt, sodass weniger Fehler auftreten sollten. **Azure PowerShell** eignet sich ideal für einmalige interaktive Aufgaben und bzw. oder für das Automatisieren von sich wiederholenden Aufgaben.

> [!NOTE]
> PowerShell ist eine plattformübergreifende Shell, die Dienste wie Shellfenster und Befehlsanalysen bereitstellt. Azure PowerShell ist ein optionales Add-On-Paket, das Azure-spezifische Befehle (die sogenannten **Cmdlets**) hinzufügt. Weitere Informationen zur Installation und Verwendung von Azure PowerShell erhalten Sie in einem separaten Schulungsmodul.

Beispielsweise können Sie mit dem `New-AzureRmVM`-Cmdlet eine neue Azure-VM erstellen.

```powershell
New-AzureRmVm `
    -ResourceGroupName "TestResourceGroup" `
    -Name "test-wp1-eus-vm" `
    -Location "East US" `
    -VirtualNetworkName "test-wp1-eus-network" `
    -SubnetName "default" `
    -SecurityGroupName "test-wp1-eus-nsg" `
    -PublicIpAddressName "test-wp1-eus-pubip" `
    -OpenPorts 80,3389
```

Geben Sie wie hier gezeigt verschiedene Parameter an, damit die zahlreichen verfügbaren VM-Konfigurationseinstellungen verarbeitet werden können. Die meisten Parameter haben sinnvolle Werte – Sie müssen nur die erforderlichen Parameter angeben. Weitere Informationen zum Erstellen und Verwalten von VMs mit Azure PowerShell finden Sie im Modul **Automatisieren von Azure-Aufgaben mithilfe von Skripts mit PowerShell**.
<a name="Azure_CLI" />

## <a name="azure-cli"></a>Azure CLI

Eine weitere Option für das Erstellen von Skripts und Verwenden von Befehlszeilen in Azure ist die **Azure CLI**.

Die Azure CLI ist das plattformübergreifende Befehlszeilentool von Microsoft zum Verwalten von Azure-Ressourcen wie VMs und Dateiträgern über die Befehlszeile. Sie steht für macOS, Linux und Windows sowie unter Verwendung von Cloud Shell im Browser zur Verfügung. Wie Azure PowerShell ist auch die Azure CLI eine leistungsstarke Option, Ihren Verwaltungsworkflow zu optimieren. Im Gegensatz zu Azure PowerShell benötigt die Azure CLI PowerShell nicht.

Sie können beispielsweise eine Azure-VM mit dem Befehl `az vm create` erstellen.

```bash
az vm create \
    --resource-group TestResourceGroup \
    --name test-wp1-eus-vm \
    --image win2016datacenter \
    --admin-username jonc \
    --admin-password aReallyGoodPasswordHere
```

Die Azure CLI kann mit anderen Skriptsprachen verwendet werden, z.B. mit Ruby und Python. Beide Sprachen werden häufig auf Computern verwendet, die nicht auf Windows basieren. Außerdem sind nicht alle Entwickler mit PowerShell vertraut.

Weitere Informationen zum Erstellen und Verwalten von VMs finden Sie im Modul **Verwalten von VMs mit der Azure CLI**.

## <a name="programmatic-apis"></a>Programmgesteuert (APIs)

Im Allgemeinen eignet sich sowohl Azure PowerShell als auch die Azure CLI, wenn Sie einfache Skripts ausführen und Befehlszeilentools verwenden möchten. Bei komplexeren Szenarios, in denen das Erstellen und Verwalten von VMs Teil einer größeren Anwendung mit komplexer Logik ist, ist ein anderer Ansatz erforderlich.

Sie können mit jeder Art von Ressource in Azure programmgesteuert interagieren.

<a name="Azure_REST_API" />

### <a name="azure-rest-api"></a>Die Azure-REST-API

Die Azure-REST-API bietet Entwicklern nach Ressourcen geordnete Vorgänge und die Möglichkeit, VMs zu erstellen und zu verwalten. Vorgänge werden als URIs mit entsprechenden HTTP-Methoden (`GET`, `PUT`, `POST`, `DELETE` und `PATCH`) und einer entsprechenden Antwort verfügbar gemacht.

Die Azure Compute-APIs ermöglichen Ihnen den programmgesteuerten Zugriff auf virtuelle Computer und die zugehörigen unterstützenden Ressourcen. Diese API unterstützt die folgenden Vorgänge:

- Erstellen und Verwalten von Verfügbarkeitsgruppen
- Hinzufügen und Verwalten von VM-Erweiterungen
- Erstellen und Verwalten von verwalteten Datenträgern, Momentaufnahmen und Images
- Zugreifen auf die in Azure verfügbaren Plattformimages
- Abrufen von Nutzungsinformationen von Ressourcen
- Erstellen und Verwalten von VMs
- Erstellen und Verwalten von VM-Skalierungsgruppen

<a name="Azure_Client_SDK" />

### <a name="azure-client-sdk"></a>Das Azure-Client SDK

Obwohl die REST-API plattform- und sprachunabhängig ist, achten Entwickler meist auf eine höhere Abstraktionsebene. Das Azure-Client SDK kapselt die Azure-REST-API und erleichtert Entwicklern die Interaktion mit Azure erheblich.

Die Azure-Client SDKs sind für zahlreiche Sprachen und Frameworks verfügbar, einschließlich .NET-basierter Sprachen wie C#, Java, Node.js, PHP, Python, Ruby und Go.

Nachfolgend wird ein Beispielausschnitt aus einem C#-Code dargestellt, über den eine Azure-VM mit dem `Microsoft.Azure.Management.Fluent`-NuGet-Paket erstellt werden kann:

```csharp
var azure = Azure
    .Configure()
    .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
    .Authenticate(credentials)
    .WithDefaultSubscription();
// ...
var vmName = "test-wp1-eus-vm";

azure.VirtualMachines.Define(vmName)
    .WithRegion(Region.USEast)
    .WithExistingResourceGroup("TestResourceGroup")
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .WithAdminUsername("jonc")
    .WithAdminPassword("aReallyGoodPasswordHere")
    .WithComputerName(vmName)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

Hier ist der gleiche Ausschnitt in Java unter Verwendung von **Azure-Java SDK**:

```java
String vmName = "test-wp1-eus-vm";
// ...
VirtualMachine virtualMachine = azure.virtualMachines()
    .define(vmName)
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("TestResourceGroup")
    .withExistingPrimaryNetworkInterface(networkInterface)
    .withLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .withAdminUsername("jonc")
    .withAdminPassword("aReallyGoodPasswordHere")
    .withComputerName(vmName)
    .withSize("Standard_DS1")
    .create();
```

<a name="Azure_VMExtensions" />

## <a name="azure-vm-extensions"></a>Azure-VM-Erweiterungen

Angenommen, Sie möchten nach der ersten Bereitstellung zusätzliche Software auf Ihrer VM konfigurieren und installieren. Sie möchten, dass diese Aufgabe eine bestimmte Konfiguration verwendet, die automatisch überwacht und ausgeführt wird.

**Azure-VM-Erweiterungen** sind kleine Anwendungen, mit denen Sie Aufgaben auf Azure-VMs nach der erstmaligen Bereitstellung konfigurieren und automatisieren können. **Azure-VM-Erweiterungen** können über die Azure CLI, PowerShell, Azure Resource Manager-Vorlagen und das Azure-Portal ausgeführt werden.

Sie bündeln Erweiterungen mit einer neuen VM-Bereitstellung oder führen sie für ein bestehendes System aus.

<a name="Azure_Automation" />

## <a name="azure-automation-services"></a>Azure Automation-Dienste

Zeitersparnis, Fehlerreduktion und Effizienzsteigerung sind einige der größten Herausforderungen beim Verwalten von Remoteinfrastrukturen. Wenn Sie über mehrere Infrastrukturdienste verfügen, sollten Sie in Betracht ziehen, Azure-Dienste auf einer höheren Ebene für die Ausführung auf einer höheren Ebene zu verwenden.

Mit **Azure Automation** können Sie Dienste integrieren, um so häufige, zeitaufwändige und fehleranfälliger Verwaltungsaufgaben ganz leicht zu automatisieren. Dies umfasst die **Prozessautomatisierung**, **Konfigurationsverwaltung** und **Updateverwaltung**.

- **Prozessverwaltung**. Angenommen, Sie haben eine VM, die auf ein bestimmtes Fehlerereignis überwacht wird. Sie möchten Maßnahmen ergreifen und das Problem beheben, sobald es gemeldet wird. Mit der Prozessautomatisierung können Sie Watchertasks einrichten, die auf Ereignisse reagieren, die ggf. in Ihrem Rechenzentrum auftreten.

- **Konfigurationsverwaltung**.  Möglicherweise möchten Sie Softwareupdates nachverfolgen, die für das Betriebssystem verfügbar sind, das auf Ihrer VM ausgeführt wird. Vielleicht möchten Sie bestimmte Updates ein- oder ausschließen. Mit der Konfigurationsverwaltung können Sie diese Updates nachverfolgen und bei Bedarf Maßnahmen ergreifen. Mit dem **System Center Configuration Manager** lassen sich die PCs Ihres Unternehmens sowie Server und mobile Geräte verwalten. Mit dem Configuration Manager können Sie diese Unterstützung auf Ihre Azure-VMs erweitern.

- **Updateverwaltung**. Mit der Updateverwaltung können Sie Updates und Patches für Ihre VMs verwalten. Mit diesem Dienst haben Sie die Möglichkeit, den Status verfügbarer Updates zu bewerten, Installationen zu planen und Bereitstellungsergebnisse zu überprüfen, um sicherzustellen, dass Updates erfolgreich angewendet wurden. Die Updateverwaltung umfasst Dienste, die Prozess- und Konfigurationsverwaltung bieten. Sie aktivieren die Updateverwaltung für eine VM direkt über Ihr **Azure Automation**-Konto. Sie können die Updateverwaltung auch für eine einzelne VM im Portal über das Blatt „Virtueller Computer“ aktivieren.

Wie Sie sehen können, bietet Azure zahlreiche Tools zum Erstellen und Verwalten von Ressourcen. So können Sie Verwaltungsvorgänge in Prozesse integrieren, um _Ihre Workflows zu optimieren_. Nachfolgend werden nun einige andere Azure-Dienste betrachtet, damit Sie dafür sorgen können, dass Ihre Infrastrukturressourcen optimal ausgeführt werden.
