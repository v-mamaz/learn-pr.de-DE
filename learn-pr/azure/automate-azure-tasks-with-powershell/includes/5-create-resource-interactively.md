Mit PowerShell können Sie Befehle schreiben und diese sofort ausführen. Wird als **interaktiver Modus** bezeichnet.

Denken Sie daran, dass das Ziel im CRM-Beispiel (Customer Relationship Management) darin besteht, drei Testumgebungen zu erstellen, die virtuelle Computer enthalten. Sie verwenden Ressourcengruppen, um sicherzustellen, dass die virtuellen Computer in separaten Umgebungen organisiert sind: einer für Komponententests, einer für Integrationstests und einer für Benutzerakzeptanztests. Da Sie die Ressourcengruppen nur einmal erstellen müssen, ist der interaktive Modus von PowerShell daher eine gute Wahl.

Wenn Sie einen Befehl in PowerShell eingeben, wird er einem _Cmdlet_ zugeordnet, mit dem dann die gewünschte Aktion durchgeführt wird. Wir sehen uns einige allgemeine Befehle an, die Sie verwenden können, und anschließend wird die Installation der Azure-Unterstützung für PowerShell beschrieben.

## <a name="what-are-powershell-cmdlets"></a>Was sind PowerShell-Cmdlets?
Ein PowerShell-Befehl wird als **Cmdlet** (ausgesprochen: „Command-let“) bezeichnet. Ein Cmdlet ist ein Befehl, der ein einzelnes Feature bearbeitet. Der Begriff **Cmdlet** soll „kleiner Befehl“ heißen. Gemäß der Konvention wird Cmdlet-Autoren empfohlen, Cmdlets einfach zu halten und nur für einen einzigen Zweck zu erstellen.

Im PowerShell-Basisprodukt sind Cmdlets enthalten, die mit Features wie Sitzungen und Hintergrundaufträgen funktionieren. Fügen Sie Module zu Ihrer PowerShell-Installation hinzu, damit Cmdlets andere Features ändern können. Es gibt z.B. Drittanbietermodule für die Arbeit mit FTP, das Verwalten Ihres Betriebssystems oder das Zugreifen auf das Dateisystem.

Die Namenskonvention bei Cmdlets ist „Verb-Substantiv“, z.B. **Get-Process**, **Format-Table**, and **Start-Service**. Es gibt ebenfalls eine Konvention für die Auswahl des Verbs, z.B. „get“ zum Abrufen von Daten, „set“ zum Einfügen oder Aktualisieren von Daten, „format“ zum Formatieren von Daten oder „out“, um die Ausgabe einem Ziel zuzuweisen.

Cmdlet-Autoren wird empfohlen, eine Hilfedatei für jedes Cmdlet einzufügen. Das Cmdlet **Get-Help** zeigt jeweils die Hilfedatei für ein Cmdlet an. Beispielsweise können wir mit der folgenden Anweisung die Hilfe zum Cmdlet `Get-ChildItem` anzeigen:

```powershell
Get-Help Get-ChildItem -detailed
```

## <a name="what-is-a-powershell-module"></a>Was ist ein PowerShell-Modul?

Cmdlets werden als Teile von _Modulen_ bereitgestellt. Ein PowerShell-Modul ist eine DLL, die den Code zum Verarbeiten der einzelnen verfügbaren Cmdlets enthält. Sie können Cmdlets in PowerShell laden, indem Sie das Modul laden, in dem diese enthalten sind. Eine Liste mit den geladenen Modulen können Sie mit dem Befehl `Get-Module` anzeigen:

```powershell
Get-Module
```

Die Ausgabe sieht in etwa wie folgt aus:

```output
ModuleType Version    Name                                ExportedCommands
---------- -------    ----                                ----------------
Manifest   3.1.0.0    Microsoft.PowerShell.Management     {Add-Computer, Add-Content, Checkpoint-Computer, Clear-Con...
Manifest   3.1.0.0    Microsoft.PowerShell.Utility        {Add-Member, Add-Type, Clear-Variable, Compare-Object...}
Binary     1.0.0.1    PackageManagement                   {Find-Package, Find-PackageProvider, Get-Package, Get-Pack...
Script     1.0.0.1    PowerShellGet                       {Find-Command, Find-DscResource, Find-Module, Find-RoleCap...
Script     2.0.0      PSReadline                          {Get-PSReadLineKeyHandler, Get-PSReadLineOption, Remove-PS...
```

## <a name="what-is-azurerm"></a>Was ist AzureRM?
**AzureRM** ist der formelle Name des Azure PowerShell-Moduls, das die Cmdlets enthält, die mit den Azure-Features zusammenarbeiten sollen (das **RM** im Namen steht für **Resource Manager**). Es enthält hunderte Cmdlets, mit denen Sie nahezu jeden Aspekt jeder Azure-Ressource regulieren können. Sie können mit Ressourcengruppen, Speicher, virtuellen Computern, Azure Active Directory, Containern, Machine Learning usw. arbeiten. Dieses Modul ist eine Open-Source-Komponente, die [auf GitHub verfügbar](https://github.com/Azure/azure-powershell) ist.

> [!NOTE]
> Das Azure PowerShell-Modul kann optional installiert werden. Die Cmdlets stehen erst zur Verfügung, nachdem Sie das Modul importiert haben.

### <a name="install-the-azurerm-module"></a>Installieren des AzureRM-Moduls

Das AzureRM-Modul ist über ein globales Repository mit dem Namen „PowerShell-Katalog“ verfügbar. Sie können das Modul mit dem Befehl `Install-Module` auf Ihrem lokalen Computer installieren. Sie benötigen eine PowerShell-Instanz mit erhöhten Rechten, um Module aus dem PowerShell-Katalog zu installieren. 

::: zone pivot="windows"

Führen Sie die folgenden Befehle aus, um das aktuelle Azure PowerShell-Modul zu installieren:

1. Öffnen Sie das **Startmenü**, und geben Sie **Windows PowerShell** ein.

1. Klicken Sie mit der rechten Maustaste auf das Symbol **Windows PowerShell**, und wählen Sie **Als Administrator ausführen** aus.

1. Klicken Sie im Dialogfeld **Benutzerkontensteuerung** auf **Ja**.

1. Geben Sie den folgenden Befehl ein, und drücken Sie die Eingabetaste:

    ```powershell
    Install-Module -Name AzureRM
    ```

Das Modul wird standardmäßig für alle Benutzer installiert (über den Bereichsparameter gesteuert). 

Der Befehl nutzt NuGet zum Abrufen von Komponenten. Je nach der bei Ihnen installierten NuGet-Version wird ggf. ein Dialogfeld angezeigt, über das Sie die aktuelle Version von NuGet herunterladen und installieren können.

```output
NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The NuGet
 provider must be available in 'C:\Program Files (x86)\PackageManagement\ProviderAssemblies' or
'C:\Users\<username>\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider by running
'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and import
 the NuGet provider now?
```

Standardmäßig ist der PowerShell-Katalog nicht als vertrauenswürdiges Repository für PowerShellGet konfiguriert. Bei der ersten Verwendung des PowerShell-Katalogs wird die folgende Meldung angezeigt:

```output
You are installing the modules from an untrusted repository. If you trust this repository, change its
InstallationPolicy value by running the Set-PSRepository cmdlet. Are you sure you want to install the modules from
'PSGallery'?
```

#### <a name="script-execution-failed"></a>Fehler bei der Skriptausführung
Je nach Ihrer Sicherheitskonfiguration tritt für `Import-Module` unter Umständen ein Fehler der folgenden Art auf.

```output
import-module : File C:\Program Files (x86)\WindowsPowerShell\Modules\azurerm\6.8.1\AzureRM.psm1 cannot be loaded
because running scripts is disabled on this system. For more information, see about_Execution_Policies at
https:/go.microsoft.com/fwlink/?LinkID=135170.
At line:1 char:1
+ import-module azurerm
+ ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : SecurityError: (:) [Import-Module], PSSecurityException
    + FullyQualifiedErrorId : UnauthorizedAccess,Microsoft.PowerShell.Commands.ImportModuleCommand
```

Hiermit wird normalerweise angegeben, dass die Ausführungsrichtlinie „eingeschränkt“ ist. Dies bedeutet, dass Sie keine Module ausführen können, die Sie von einer externen Quelle herunterladen, einschließlich des PowerShell-Katalogs. Sie können überprüfen, ob dies der Fall ist, indem Sie den Befehl `Get-ExecutionPolicy` ausführen. Gehen Sie wie folgt vor, falls „Eingeschränkt“ zurückgegeben wird:

1. Öffnen Sie eine PowerShell-Eingabeaufforderung mit erhöhten Rechten.
1. Verwenden Sie das Cmdlet `SetExecutionPolicy`, um die Richtlinie in „RemoteSigned“ zu ändern:

```powershell
Set-ExecutionPolicy RemoteSigned
```

Ihre Berechtigung wird abgefragt:

```output
The execution policy helps protect you from scripts that you do not trust. Changing the execution policy might expose
you to the security risks described in the about_Execution_Policies help topic at
https:/go.microsoft.com/fwlink/?LinkID=135170. Do you want to change the execution policy?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): Y
```

Sie sollten dann `Import-Module` verwenden können, um die Cmdlets zu laden.

:::zone-end

::: zone pivot="linux,macos"

Zum Installieren von Azure PowerShell unter Linux oder macOS verwenden wir die gleichen Befehle.

1. Geben Sie auf einem Terminal den folgenden Befehl ein, um PowerShell Core mit erhöhten Rechten zu starten.

    ```bash
    sudo pwsh
    ```

1. Um Azure PowerShell zu installieren, führen Sie an der PowerShell Core-Eingabeaufforderung den folgenden Befehl aus.

    ```powershell
    Install-Module AzureRM.NetCore
    ```

1. Wenn Sie gefragt werden, ob Sie Modulen von **PSGallery** vertrauen, antworten Sie **Ja** oder **Ja, alle**.

:::zone-end

### <a name="update-a-module"></a>Aktualisieren eines Moduls

Wenn Sie in einer Warnung oder Fehlermeldung darauf hingewiesen werden, dass bereits eine Version des Azure PowerShell-Moduls installiert ist, können Sie diese mit dem folgenden Befehl auf die _neueste_ Version aktualisieren:

:::zone pivot="windows"

```powershell
Update-Module -Name AzureRM
```

:::zone-end

::: zone pivot="linux,macos"

```powershell
Update-Module -Name AzureRM.NetCore
```

:::zone-end

Antworten Sie ebenso wie beim Befehl `Install-Module` auf die Frage, ob Sie dem Modul vertrauen, mit **Ja** oder **Ja, alle**. Sie können auch den Befehl `Update-Module` verwenden, um ein Modul neu zu installieren, falls dafür Probleme auftreten.

## <a name="example-how-to-create-a-resource-group-with-azure-powershell"></a>Beispiel: Erstellen einer Ressourcengruppe mit Azure PowerShell
Nachdem Sie das Azure-Modul geladen haben, können Sie mit der Verwendung von Azure beginnen. Wir führen eine häufige Aufgabe durch: das Erstellen einer Ressourcengruppe. Wie Sie wissen, verwenden wir Ressourcengruppen, um zusammengehörige Ressourcen gemeinsam zu verwalten. Die Erstellung einer neuen Ressourcengruppe ist eine der ersten Aufgaben, die Sie beim Starten einer neuen Azure-Lösung durchführen.

Es müssen vier Schritte ausgeführt werden:

1. Importieren Sie die Azure-Cmdlets.

1. Stellen Sie eine Verbindung mit Ihrem Azure-Abonnement her.

1. Erstellen Sie die Ressourcengruppe.

1. Stellen Sie sicher, dass das Erstellen erfolgreich war.

Die folgende Abbildung zeigt eine Übersicht dieser Schritte.

![Eine Abbildung, die die Schritte zum Erstellen einer Ressourcengruppe zeigt.](../media/5-create-resource-overview.png)

Jeder Schritt entspricht einem anderen Cmdlet.

### <a name="import-the-azure-cmdlets"></a>Importieren der Azure-Cmdlets
PowerShell lädt beim Start standardmäßig nur die wichtigsten Cmdlets. Das bedeutet, dass das Cmdlet, dass mit Azure arbeiten muss, nicht geladen wird. Die zuverlässigste Option zum Laden der benötigten Cmdlets besteht darin, diese manuell zu Beginn der PowerShell-Sitzung zu importieren.

Sie verwenden das Cmdlet **Import-Module** zum Laden von Modulen. Dieses Cmdlet verfügt über viele Parameter, die für unterschiedliche Situationen geeignet sind. Beispielsweise kann es mehrere Module, eine bestimmte Modulversion, Teile eines Moduls usw. laden.

Beispielsweise können wir alle Cmdlets für AzureRM mit dem folgenden Befehl **in einer PowerShell-Sitzung mit erhöhten Rechten** laden:

:::zone pivot="windows"

```powershell
Import-Module AzureRM
```

:::zone-end

::: zone pivot="linux,macos"

```powershell
Import-Module AzureRM.NetCore
```

:::zone-end

> [!TIP]
> Wenn Sie häufig mit Azure PowerShell arbeiten, haben Sie zwei Möglichkeiten, um den Modulladeprozess zu automatisieren. Sie können Ihrem PowerShell-Profil einen Eintrag hinzufügen, um das Azure-Modul beim Start zu importieren, oder die aktuellste Versionen von PowerShell verwenden, die das enthaltende Modul automatisch lädt, wenn Sie das Cmdlet verwenden.

### <a name="connect"></a>Verbinden
Wenn Sie mit einer lokalen Installation von Azure PowerShell arbeiten, müssen Sie sich zunächst authentifizieren, um Azure-Befehle ausführen zu können. Das Cmdlet **Connect-AzureRmAccount** ruft Ihre Azure-Anmeldeinformationen ab und stellt dann eine Verbindung mit Ihrem Azure-Abonnement her. Es hat viele optionale Parameter. Aber wenn Sie nur eine interaktive Eingabeaufforderung benötigen, sind keine Parameter erforderlich:

```powershell
Connect-AzureRmAccount
```

Sie müssen diese Schritte für jede neue PowerShell-Sitzung wiederholen, die Sie starten, da dieses Modul nicht Teil des Kernsatzes ist.


### <a name="working-with-subscriptions"></a>Arbeiten mit Abonnements
Falls Sie noch keine Erfahrung mit Azure haben, verfügen Sie wahrscheinlich nur über ein einzelnes Abonnement. Wenn Sie Azure hingegen schon eine Weile verwenden, haben Sie unter Umständen bereits mehrere Azure-Abonnements erstellt. Sie können Azure PowerShell so konfigurieren, dass Befehle für ein bestimmtes Abonnement ausgeführt werden.

Hierfür kann nur jeweils ein Abonnement verwendet werden. Verwenden Sie das Cmdlet `Get-AzureRmContext`, um zu ermitteln, welches Abonnement aktiv ist. Falls es nicht das richtige Abonnement ist, können Sie es ändern.

1. Rufen Sie mit dem Befehl `Get-AzureRmSubscription` eine Liste mit allen Abonnementnamen Ihres Kontos ab. 

2. Ändern Sie das Abonnement, indem Sie den Namen des gewünschten Abonnements übergeben.

```powershell
Select-AzureRmSubscription -Subscription "Visual Studio Enterprise"
```

### <a name="get-a-list-of-all-resource-groups"></a>Abrufen einer Liste mit allen Ressourcengruppen

Sie können eine Liste mit allen Ressourcengruppen des aktiven Abonnements abrufen:

```powershell
Get-AzureRmResourceGroup
```

Wenn Sie eine kürzere Übersicht erhalten möchten, können Sie die Ausgabe von `Get-AzureRmResourceGroup` per Pipezeichen („|“) an das Cmdlet `Format-Table` senden.

```powershell
Get-AzureRmResourceGroup | Format-Table
```

Die Ausgabe sieht in etwa wie folgt aus:

```output
ResourceGroupName                  Location       ProvisioningState Tags TagsTable ResourceId
-----------------                  --------       ----------------- ---- --------- ----------
cloud-shell-storage-southcentralus southcentralus Succeeded                        /subscriptions/xxxxxxxx-d3ce-4172...
ExerciseResources                  eastus         Succeeded                        /subscriptions/xxxxxxxx-d3ce-4172...
```

### <a name="create-a-resource-group"></a>Erstellen einer Ressourcengruppe

Wie Sie wissen, ordnen Sie die Ressourcen bei ihrer Erstellung in Azure zu Verwaltungszwecken immer in einer Ressourcengruppe an. Eine Ressourcengruppe ist häufig eines der ersten Dinge, die Sie beim Starten einer neuen Anwendung erstellen.

Sie können Ressourcengruppen mit dem Cmdlet `New-AzureRmResourceGroup` erstellen. Sie müssen einen Namen und einen Standort angeben. Der Name muss innerhalb Ihres Abonnements eindeutig sein. Der Standort bestimmt, wo die Metadaten für Ihre Ressourcengruppe gespeichert werden (was für Sie aus Konformitätsgründen wichtig sein kann). Verwenden Sie Zeichenfolgen wie „USA, Westen“, „Europa, Norden“ oder „Indien, Westen“, um den Standort anzugeben. Wie die meisten Azure-Cmdlets verfügt auch `New-AzureRmResourceGroup` über viele optionale Parameter. Die grundlegende Syntax lautet:

```powershell
New-AzureRmResourceGroup -Name <name> -Location <location>
```

> [!NOTE]
> Zur Erinnerung: Wir arbeiten in der Azure-Sandbox, mit der die Ressourcengruppe für Sie erstellt wird. Der obige Befehl wird verwendet, wenn Sie in Ihrem eigenen Abonnement arbeiten.

### <a name="verify-the-resources"></a>Überprüfen der Ressourcen
Mit `Get-AzureRmResource` werden Ihre Azure-Ressourcen aufgelistet. So können wir hier überprüfen, ob die Ressourcengruppe erfolgreich erstellt wurde.

```powershell
Get-AzureRmResource
```

Wie beim Befehl `Get-AzureRmResourceGroup` auch, können Sie mit dem Cmdlet `Format-Table` eine kürzere Übersicht erhalten. Hier nutzen wir eine Kurzform von `ft`:

```powershell
Get-AzureRmResource | ft
```

Sie können auch nach bestimmten Ressourcengruppen filtern, um nur die Ressourcen aufzulisten, die dieser Gruppe zugeordnet sind:

```powershell
Get-AzureRmResource -ResourceGroup ExerciseResources
```

### <a name="creating-an-azure-virtual-machine"></a>Erstellen eines virtuellen Azure-Computers

Eine weitere häufige Aufgabe, die mit PowerShell durchgeführt werden kann, ist die Erstellung von VMs.

Azure PowerShell stellt das Cmdlet `New-AzureRmVm` bereit, um einen virtuellen Computer zu erstellen. Das Cmdlet hat viele Parameter, um die große Anzahl von Konfigurationseinstellungen für virtuelle Computer zu verarbeiten. Die meisten Parameter haben sinnvolle Standardwerte, deshalb müssen Sie nur fünf Werte angeben:

- **ResourceGroupName:** Die Ressourcengruppe, in der der neue virtuelle Computer platziert wird.
- **Name:** Der Name des virtuellen Computers in Azure.
- **Location:** Der geografische Standort, in dem der virtuelle Computer bereitgestellt wird.
- **Credential:** Ein Objekt, das den Benutzernamen und das Kennwort für das Administratorkonto des virtuellen Computers enthält. Wir verwenden das Cmdlet `Get-Credential`. Bei diesem Cmdlet werden ein Benutzername und ein Kennwort abgefragt und in einem Objekt für Anmeldeinformationen verpackt.
- **Image**: Das Betriebssystemimage, das für den virtuellen Computer verwendet werden soll. Dies ist häufig eine Linux-Distribution oder Windows Server.

```powershell
   New-AzureRmVm 
       -ResourceGroupName <resource group name> 
       -Name <machine name> 
       -Credential <credentials object> 
       -Location <location> 
       -Image <image name>
```

Sie können diese Parameter direkt für das obige Cmdlet bereitstellen. Alternativ hierzu können auch andere Cmdlets verwendet werden, um den virtuellen Computer zu konfigurieren, z.B. `Set-AzureRmVMOperatingSystem`, `Set-AzureRmVMSourceImage`, `Add-AzureRmVMNetworkInterface` und `Set-AzureRmVMOSDisk`.

Hier ist ein Beispiel angegeben, in dem das Cmdlet `Get-Credential` mit dem Parameter `-Credential` verknüpft wird:

```powershell
New-AzureRmVM -Name MyVm -ResourceGroupName ExerciseResources -Credential (Get-Credential) ...
```

Das Suffix `AzureRmVM` gilt speziell für VM-basierte Befehle in PowerShell. Es gibt noch mehrere andere, die Sie verwenden können:

| Befehl | Beschreibung |
|---------|-------------|
| `Remove-AzureRmVM` | Löscht eine Azure-VM. |
| `Start-AzureRmVM` | Startet eine angehaltene VM. |
| `Stop-AzureRmVM` | Beendet die Ausführung einer VM. |
| `Restart-AzureRmVM` | Startet eine VM neu. |
| `Update-AzureRmVM` | Aktualisiert die Konfiguration für eine VM. |

#### <a name="example-getting-the-information-for-a-vm"></a>Beispiel: Abrufen der Informationen für eine VM

Sie können die Liste mit den VMs in Ihrem Abonnement mit dem Befehl `Get-AzureRmVM -Status` auflisten. Hiermit kann auch eine VM mit der `-Name`-Eigenschaft angegeben werden. Hier erfolgt die Zuweisung zu einer PowerShell-Variablen:

```powershell
$vm = Get-AzureRmVM  -Name MyVM -ResourceGroupName ExerciseResources
```

Hierbei ist interessant, dass es sich um ein _Objekt_ handelt, mit dem Sie interagieren können. Beispielsweise können Sie dieses Objekt verwenden, Änderungen daran vornehmen und die Änderungen dann mit dem Befehl `Update-AzureRmVM` mithilfe eines Pushvorgangs zurück an Azure übertragen:

```powershell
$ResourceGroupName = "ExerciseResources"
$vm = Get-AzureRmVM  -Name MyVM -ResourceGroupName $ResourceGroupName
$vm.HardwareProfile.vmSize = "Standard_DS3_v2"

Update-AzureRmVM -ResourceGroupName $ResourceGroupName  -VM $vm
```

Der interaktive Modus von PowerShell eignet sich für einmalige Aufgaben. In unserem Beispiel verwenden wir voraussichtlich die gleiche Ressourcengruppe für das gesamte Projekt, weshalb es sinnvoll ist, sie als interaktive Ressourcengruppe zu erstellen. Der interaktive Modus erweist sich für diese Aufgabe oft als schneller und einfacher als das Schreiben eines Skripts, das Sie dann nur einmal ausführen.