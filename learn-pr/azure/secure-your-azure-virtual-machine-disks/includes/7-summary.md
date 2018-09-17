Azure stellt zum Schutz von Azure-VM-Datenträgern Speicherdienstverschlüsselung (SSE) und Azure Disk Encryption (ADE) bereit. Diese Technologien arbeiten zusammen, um eine starke 256-Bit-Verschlüsselung im Rahmen eines mehrschichtigen Sicherheitsansatzes für den Schutz von Azure-VM-Datenträgern zu bieten. Es ist erforderlich, dass Sie die Einrichtung der notwendigen Komponenten für Azure Disk Encryption abschließen, um die Datenträgerverschlüsselung zu aktivieren. Dieser Vorgang kann mit dem Konfigurationsskript für die erforderlichen Azure Disk Encryption-Komponenten automatisiert werden. Wenn Sie die Verschlüsselung auf neuen VMs aktivieren, können Sie eine Azure Resource Manager-Vorlage verwenden. Dadurch wird sichergestellt, dass Ihre Daten zum Zeitpunkt der Bereitstellung verschlüsselt werden, sodass keine Sicherheitsrisiken entstehen.

## <a name="clean-up"></a>Bereinigen
<!---TODO: Update for sandbox?---> Das Ausführen von Azure-VMs und der zugeordnete Speicher verursachen Kosten im Rahmen Ihres Abonnements. Es ist daher sinnvoll, nicht benötigte Ressourcen zu entfernen, um unnötige Gebühren zu vermeiden. Die einfachste Möglichkeit, Ihr Azure-Abonnement zu bereinigen, ist das Entfernen der Ressourcengruppe. Dabei werden auch alle Ressourcen in der Gruppe gelöscht. Wenn Sie mit diesem Modul fertig sind, führen Sie das folgende Azure PowerShell-Cmdlet aus:

   ```powershell
   Remove-AzureRmResourceGroup -Name moneyapprg
   ```

Sie werden aufgefordert, den Löschvorgang zu bestätigen. Wählen Sie **Ja** aus. Die Ausführung des Befehls zum Löschen der Ressourcen kann mehrere Minuten in Anspruch nehmen. 

Wenn eine Meldung angezeigt wird, in der auf einen Löschfehler hingewiesen wird, müssen Sie möglicherweise Schlüsseltresorsperren entfernen, bevor Sie die Ressourcengruppe löschen.
