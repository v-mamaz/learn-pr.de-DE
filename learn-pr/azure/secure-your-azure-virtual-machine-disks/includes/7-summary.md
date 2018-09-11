Azure stellt zum Schutz von Azure VM-Datenträgern Speicherdienstverschlüsselung (Storage Service Encryption, SSE) und Azure Disk Encryption (ADE) bereit. Diese Technologien arbeiten zusammen, um starke 256-Bit-Verschlüsselung im Rahmen eines tiefgreifenden Verteidigungsansatzes für den Schutz von Azure VM-Datenträgern zu bieten. Es ist erforderlich, dass Sie Azure Disk Encryption – Voraussetzungen abschließen, um Datenträgerverschlüsselung zu aktivieren. Dieser Vorgang kann mit dem Konfigurationsskript für die Azure Disk Encryption-Voraussetzungen automatisiert werden. Beim Aktivieren von Verschlüsselung für neue VMs können Sie eine ARM-Vorlage verwenden, wodurch sichergestellt wird, dass Ihre Daten am Bereitstellungspunkt verschlüsselt werden, so dass alle Sicherheitsrisiken abgedeckt sind.

## <a name="cleanup"></a>Bereinigen
<!---TODO: Do we need to include cleanup for the free education tier?--->

Das Ausführen von Azure VMs und der zugeordnete Speicher verursachten Kosten im Rahmen Ihres Abonnements. Es ist daher sinnvoll, nicht benötigte Ressourcen zu entfernen, um unnötige Gebühren zu vermeiden. Die einfachste Möglichkeit, Ihr Azure-Abonnement zu bereinigen, ist das Entfernen der Ressourcengruppe. Dabei werden auch alle Ressourcen in der Gruppe gelöscht. Wenn Sie mit diesem Modul fertig sind, führen Sie das folgende Azure PowerShell-Cmdlet aus:

   ```powershell
   Remove-AzureRmResourceGroup -Name moneyapprg
   ```

Wenn Sie aufgefordert werden, den Löschvorgang zu bestätigen, klicken Sie auf **Ja**. Der Befehl zum Löschen der Ressourcen kann mehrere Minuten in Anspruch nehmen. 

Wenn eine Nachricht über einen Löschfehler angezeigt wird, müssen Sie möglicherweise Sperren am Schlüsseltresor entfernen, bevor Sie die Ressourcengruppe löschen.
