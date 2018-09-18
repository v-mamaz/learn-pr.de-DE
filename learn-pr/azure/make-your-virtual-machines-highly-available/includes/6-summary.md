Hier haben Sie gelernt, wie Sie einen Lastenausgleich als Teil einer Lösung verwenden, um die Hochverfügbarkeit in Azure gehosteter virtueller Computer zu ermöglichen. Dies beinhaltete den Lastenausgleich selbst, die zugeordneten virtuellen Netzwerke, die Regeln zum Steuern des Ausgleichsalgorithmus und Integritätstests, die identifizieren, welche virtuellen Computer ordnungsgemäß ausgeführt werden.

## <a name="clean-up"></a>Bereinigen
<!---TODO: Update for sandbox?--->

Beim Ausführen von virtuellen Computern und Skalierungsgruppen fallen Kosten für Ihr Abonnement an. Sie sollten nicht benötigte Ressourcen entfernen, um unnötige Gebühren zu vermeiden. Die einfachste Möglichkeit, Ihr Azure-Abonnement zu bereinigen, ist das Entfernen der Ressourcengruppe. Dabei werden auch alle Ressourcen in der Gruppe gelöscht. Wenn Sie mit diesem Modul fertig sind, führen Sie das folgende Azure PowerShell-Cmdlet aus:

```powershell
Remove-AzureRmResourceGroup -Name woodgrove-RG
```

Wenn Sie aufgefordert werden, den Löschvorgang zu bestätigen, klicken Sie auf **Ja**. Der Befehl zum Löschen der Ressourcen kann mehrere Minuten in Anspruch nehmen.