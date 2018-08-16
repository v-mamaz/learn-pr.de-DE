## <a name="module-summary"></a>Modul-Zusammenfassung
In diesem Modul haben wir ein Skript zum Automatisieren der Erstellung mehrerer VMs geschrieben. Auch wenn das Skript relativ kurzen war, sehen Sie die potenzielle Leistung beim Kombinieren von Schleifen, Variablen und Funktionen von PowerShell mit Azure PowerShell-Cmdlets.

Azure PowerShell ist eine gute Automation-Wahl für Administratoren mit PowerShell-Oberfläche. Die Kombination von saubere Syntax und eine leistungsfähige Skriptsprache können Sie auch in Betracht ziehen, auch wenn Sie mit PowerShell vertraut sind. Dieses Maß an Automatisierung für zeitintensive und fehleranfällige Aufgaben tragen Sie reduzieren die Zeit bei der Verwaltung und erhöhen die Qualität.

## <a name="cleanup"></a>Cleanup
Bereitgestellt und die ausgeführten virtuellen Computer fallen Kosten für Ihr Abonnement. Entfernen Sie nicht benötigte virtuelle Computer, um unnötige Gebühren zu vermeiden. Die einfachste Möglichkeit, um Ihr Azure-Abonnement zu bereinigen ist die zugeordnete Ressourcengruppe zu entfernen. Dabei werden auch alle virtuellen Computer in der Gruppe gelöscht. Und Sie können dazu PowerShell! Wenn Sie fertig sind, führen Sie das folgende Azure PowerShell-Cmdlet:

   ```powershell
   Remove-AzureRmResourceGroup -Name TrialsResourceGroup
   ```

Wenn Sie gefragt werden, um den Löschvorgang zu bestätigen, beantworten **Ja**. Der Befehl dauert mehrere Minuten in Anspruch.