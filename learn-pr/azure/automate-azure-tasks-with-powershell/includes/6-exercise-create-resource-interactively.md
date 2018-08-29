Nehmen Sie an, Sie arbeiten in einem Unternehmen, das eine Sammlung von Linux-Verwaltungstools entwickelt. Ihre Aufgabe ist es, potenziellen Kunden vor dem Kauf Ihrer Software bei der Testphase zu unterstützen. Da die Software Änderungen auf der Stammebene für das Betriebssystem vornimmt, haben Sie sich dazu entschlossen, für jeden Testkunden eine Linux-VM zu erstellen. Sie erstellen je nach Bedarf die VMs und löschen sie nach Ablauf des Testabonnements. Auf diese Weise führt jeder Kunde seine ersten Schritte mit einer bereinigten Betriebssystemversion durch. 

Damit diese VMs für interne Tests separat von den VMs Ihres Unternehmen verwaltet werden, erstellen Sie eine dedizierte Ressourcengruppe, um diese zu hosten. Sie benötigen nur eine Ressourcengruppe. Daher ist die Verwendung von Azure PowerShell im interaktiven Modus die naheliegende Wahl für diese Aufgabe.

## <a name="steps-to-create-a-resource-group"></a>Schritte zum Erstellen einer Ressourcengruppe

1. Starten Sie PowerShell.

1. Importieren Sie das Modul in die aktuelle Sitzung, damit Sie Zugriff auf die Azure-Cmdlets haben.

   ```powershell
   Import-Module AzureRM
   ```

1. Stellen Sie über den folgenden Befehl eine Verbindung mit Azure her: Authentifizieren Sie sich nach der Eingabe des Befehls durch die Angabe Ihrer Azure-Anmeldeinformationen.

   ```powershell
   Connect-AzureRmAccount
   ```

1. Erstellen Sie eine Ressourcengruppe.

    ```powershell
    New-AzureRmResourceGroup -Name "TrialsResourceGroup" -Location "East US"
    ```

1. Stellen Sie sicher, dass die Ressourcengruppe erfolgreich erstellt wurde.

    ```powershell
    Get-AzureRmResource | Format-Table
    ```
Eine weitere Möglichkeit zur Überprüfung, ob die Ressourcengruppe erfolgreich erstellt wurde, ist das Azure-Portal. Melden Sie sich hierfür beim Portal an, und navigieren zum Abschnitt **Ressourcengruppen** (siehe unten). Die neue Ressourcengruppe sollte in der Liste angezeigt werden.

![Auflisten von Ressourcengruppen über das Portal](../media-drafts/6-listing-resource-groups.png)

## <a name="summary"></a>Zusammenfassung
In dieser Übung wird ein allgemeines Muster für eine interaktive PowerShell-Sitzung veranschaulicht. Sie haben ein Standard-Cmdlet verwendet, um für die Durchführung einer bestimmten Aufgabe das AzureRM-Modul und dann die Azure PowerShell-Cmdlets zu importieren. Nun haben Sie eine Ressourcengruppe in Ihrem Abonnement erstellt und können nun VMs erstellen.