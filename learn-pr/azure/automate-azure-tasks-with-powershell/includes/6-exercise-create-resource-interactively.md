
Angenommen Sie, Sie in einem Unternehmen arbeiten, mit der eine Sammlung von Linux-Verwaltungstools. Ihre Aufgabe ist, können Sie potenzielle Kunden, die vor dem Kauf es zum Testen Ihrer Software. Da die Software auf der Stammebene-Änderungen für das Betriebssystem vornimmt, haben Sie sich entschieden, zum Erstellen einer Linux-VM für jeden Kunden Testversion. Sie erstellen die virtuellen Computer aus, je nach Bedarf und am Ende des Test-Abonnements löschen. Auf diese Weise wird jeder Kunde mit einer sauberen Version des Betriebssystems gestartet. 

Damit diese virtuellen Computer getrennt von den virtuellen Computern bleibt Ihr Unternehmen für interne Tests verwendet, erstellen Sie eine dedizierte Ressourcengruppe, deren aufnehmen soll. Sie benötigen nur eine Ressourcengruppe, damit mithilfe von Azure PowerShell im interaktiven Modus eine vernünftige Wahl für diese Aufgabe ist.

## <a name="steps-to-create-a-resource-group"></a>Schritte zum Erstellen einer Ressourcengruppe

1. Starten Sie PowerShell.

1. Importieren Sie das Modul in die aktuelle Sitzung, damit Sie Zugriff auf den Azure-Cmdlets haben.

   ```powershell
   Import-Module AzureRM
   ```

1. Verbinden Sie mit Azure mit dem unten gezeigten Befehl. Nach Eingabe des Befehls, durch die Bereitstellung Ihrer Azure-Anmeldeinformationen zu authentifizieren.

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
Eine weitere Möglichkeit zum Überprüfen, ob die Ressourcengruppe erfolgreich erstellt wurde, ist im Azure-Portal verwenden. Hierfür Anmelden beim Portal, und navigieren zu der **Ressourcengruppen** Abschnitt (siehe unten). Die neue Ressourcengruppe sollte in der Liste angezeigt werden.

![Verwenden des Portals zum Auflisten von Ressourcengruppen](../images/6-listing-resource-groups.png)

## <a name="summary"></a>Zusammenfassung
Diese Übung zeigt ein allgemeines Muster für eine interaktive PowerShell-Sitzung. Sie verwendet ein standard-Cmdlet zum Importieren des AzureRM-Moduls, und klicken Sie dann Azure-PowerShell-Cmdlets für eine bestimmte Aufgabe durchzuführen. Klicken Sie jetzt haben eine Ressourcengruppe in Ihrem Abonnement und zum Erstellen von VMs bereit sind.