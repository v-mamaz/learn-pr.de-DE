In diesem Modul haben wir ein Skript zum Automatisieren der Erstellung mehrerer VMs geschrieben. Auch wenn das Skript relativ kurz war, konnten Sie das Potenzial erkennen, wenn Sie Schleifen, Variablen und Funktionen aus PowerShell mit Azure PowerShell-Cmdlets kombinieren.

Azure PowerShell ist für Administratoren mit PowerShell-Erfahrung eine gute Wahl bei der Automatisierung. Durch die Kombination von übersichtlicher Syntax und leistungsfähiger Skriptsprache ist das Tool auch dann interessant, wenn Sie mit PowerShell noch nicht vertraut sind. Dieses Maß an Automatisierung für zeitintensive und fehleranfällige Aufgaben sollte Ihnen helfen, die Zeit für die Verwaltung zu reduzieren und die Qualität zu erhöhen.

<!-- Cleanup sandbox -->
[!include[](../../../includes/azure-sandbox-cleanup.md)]

In Ihrem eigenen Abonnement können Sie folgendes PowerShell-Cmdlet verwenden, um die Ressourcengruppe und alle zugehörigen Ressourcen zu löschen.

```powershell
Remove-AzureRmResourceGroup -Name MyResourceGroupName
```

Wenn Sie dazu aufgefordert werden, den Löschvorgang zu bestätigen, antworten Sie mit **Yes** (Ja). Alternativ können Sie den `-Force`-Parameter hinzufügen, um die Eingabeaufforderung zu überspringen. Der Befehl kann mehrere Minuten in Anspruch nehmen.