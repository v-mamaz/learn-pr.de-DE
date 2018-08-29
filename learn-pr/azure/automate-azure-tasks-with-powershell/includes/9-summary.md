In diesem Modul haben wir ein Skript zum Automatisieren der Erstellung mehrerer VMs geschrieben. Auch wenn das Skript relativ kurz war, konnten Sie das Potenzial erkennen, wenn Sie Schleifen, Variablen und Funktionen aus PowerShell mit Azure PowerShell-Cmdlets kombinieren.

Azure PowerShell ist für Administratoren mit PowerShell-Erfahrung eine gute Wahl bei der Automatisierung. Durch die Kombination von übersichtlicher Syntax und leistungsfähiger Skriptsprache ist das Tool auch dann interessant, wenn Sie mit PowerShell noch nicht vertraut sind. Dieses Maß an Automatisierung für zeitintensive und fehleranfällige Aufgaben sollte Ihnen helfen, die Zeit für die Verwaltung zu reduzieren und die Qualität zu erhöhen.

## <a name="cleanup"></a>Cleanup
Für bereitgestellte und aktive VMs fallen Kosten in Ihrem Abonnement an. Entfernen Sie nicht benötigte VMs, um unnötige Gebühren zu vermeiden. Die einfachste Möglichkeit, Ihr Azure-Abonnement zu bereinigen, ist das Entfernen der zugehörigen Ressourcengruppe. Dabei werden auch alle VMs in der Gruppe gelöscht. Hierfür können Sie PowerShell verwenden. Wenn Sie fertig sind, führen Sie das folgende Azure PowerShell-Cmdlet aus:

```powershell
Remove-AzureRmResourceGroup -Name TrialsResourceGroup
```

Sie werden aufgefordert, den Löschvorgang zu bestätigen. Wählen Sie **Ja** aus. Der Befehl kann mehrere Minuten in Anspruch nehmen.