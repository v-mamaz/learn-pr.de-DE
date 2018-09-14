Azure stellt zum Schutz von Azure VM-Datenträgern Speicherdienstverschlüsselung (Storage Service Encryption, SSE) und Azure Disk Encryption (ADE) bereit. Diese Technologien wirken zusammen, um starke 256-Bit-Verschlüsselung im Rahmen eines Defense-in-Depth-Ansatzes für den Schutz von Azure-VM-Datenträgern zu ermöglichen. Es ist erforderlich, dass Sie die Azure Disk Encryption-Voraussetzungen zum Aktivieren der datenträgerverschlüsselung zu erfüllen. Die Azure Disk Encryption erforderliche Konfigurationsskript kann diesen Prozess automatisieren. Bei der Verschlüsselung auf neuen Computern zu aktivieren, können Sie eine Azure Resource Manager-Vorlage verwenden. Dadurch wird sichergestellt, dass Ihre Daten zum Zeitpunkt der Bereitstellung, sodass keine Sicherheitsrisiken verschlüsselt werden.

## <a name="clean-up"></a>Bereinigen
<!---TODO: Update for sandbox?---> Ausführen von virtuellen Azure-Computern und der zugeordnete Speicher, fallen Kosten für Ihr Abonnement an. Es ist daher sinnvoll, nicht benötigte Ressourcen zu entfernen, um unnötige Gebühren zu vermeiden. Die einfachste Möglichkeit, Ihr Azure-Abonnement zu bereinigen, ist das Entfernen der Ressourcengruppe. Dabei werden auch alle Ressourcen in der Gruppe gelöscht. Wenn Sie mit diesem Modul fertig sind, führen Sie das folgende Azure PowerShell-Cmdlet aus:

   ```powershell
   Remove-AzureRmResourceGroup -Name moneyapprg
   ```

Wenn Sie gefragt werden, um den Löschvorgang zu bestätigen, beantworten **Ja**. Der Befehl zum Löschen der Ressourcen kann mehrere Minuten in Anspruch nehmen. 

Wenn Sie eine Fehler beim Löschen der Nachricht erhalten, müssen Sie Sperren für die Key Vault-Instanz zu entfernen, bevor Sie die Ressourcengruppe löschen können.
