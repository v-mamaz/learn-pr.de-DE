In diesem Modul haben Sie Informationen zum Azure-Datenträgerzwischenspeichern erhalten und erfahren, wie es möglicherweise die Leistung verbessert. Wir haben mithilfe von Azure-Portal und Azure PowerShell das Datenträgerzwischenspeichern für den virtuellen Computer verwaltet. 

Nachdem Sie die Strategie für das Azure-VM-Datenträgerzwischenspeichern eingerichtet haben, können Sie mithilfe von Skripts und Vorlagen schnell und einfach neue VMs und Datenträger mit den optimalen Datenträgercacheeinstellungen bereitstellen.

## <a name="further-reading"></a>Weitere nützliche Informationen

- [Azure Storage Premium: Entwurf für hohe Leistung](https://docs.microsoft.com/azure/virtual-machines/windows/premium-storage-performance)
- [Erste Schritte mit Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps?view=azurermps-6.8.1)
- [Referenz zu Azure-Computer-Cmdlets](https://docs.microsoft.com/powershell/module/azurerm.compute/?view=azurermps-6.8.1#vm_disks)


## <a name="cleanup"></a>Bereinigen
<!---TODO: Update for sandbox?--->

Für die Ausführung von Azure-VMs fallen Kosten in Ihrem Abonnement an. Entfernen Sie nicht benötigte Ressourcen, um unnötige Gebühren zu vermeiden. Am einfachsten bereinigen Sie Ihr Azure-Abonnement, indem Sie die Ressourcengruppe entfernen. Durch das Löschen einer Ressourcengruppe werden alle Ressourcen in dieser Ressourcengruppe gelöscht. Wenn Sie mit diesem Modul fertig sind, führen Sie das folgende Azure PowerShell-Cmdlet aus:

    ```powershell
    Remove-AzureRmResourceGroup -Name "fotoshare-rg"
    ```

Wenn Sie aufgefordert werden, den Löschvorgang zu bestätigen, antworten Sie mit **Ja**. Der Befehl zum Löschen der Ressourcen kann mehrere Minuten in Anspruch nehmen.
