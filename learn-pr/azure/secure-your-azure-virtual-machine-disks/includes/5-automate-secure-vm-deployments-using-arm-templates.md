Angenommen, Ihr Unternehmen stellt im Rahmen ihrer Cloudmigration mehrere Server bereit. VM-Datenträger müssen bei der Bereitstellung verschlüsselt werden, damit sie zu keinem Zeitpunkt angreifbar sind. Sie möchten diesen Prozess automatisieren und müssen die Azure Resource Manager-Vorlagen ändern, damit die Verschlüsselung automatisch aktiviert wird.

Im Folgenden verwenden Sie eine Azure Resource Manager-Vorlage, um die Verschlüsselung für neue virtuelle Windows-Computer automatisch zu aktivieren.

## <a name="what-are-azure-resource-manager-templates"></a>Was sind Azure Resource Manager-Vorlagen?

Resource Manager-Vorlagen sind JSON-Dateien zum Definieren einer Gruppe von Ressourcen, die in Azure bereitgestellt werden soll. Sie können von Grund auf neu erstellt werden. Bei einigen Ressourcen (unter anderem bei virtuellen Computern) besteht allerdings auch die Möglichkeit, sie über das Azure-Portal zu generieren. Sie geben die erforderlichen Informationen für die manuelle Bereitstellung eines virtuellen Computers an, stellen den virtuellen Computer aber nicht in Azure bereit, sondern speichern die Vorlage. Anschließend können Sie die Vorlage _wiederverwenden_, um diese spezifische VM-Konfiguration zu erstellen.

In der Dokumentation stehen [Beispielvorlagen](https://azure.microsoft.com/resources/templates) zur Automatisierung verschiedenster administrativer Aufgaben zur Verfügung. Zur Verschlüsselung des virtuellen Computers hätten Sie anstelle der manuellen Vorgehensweise auch eine dieser Vorlagen verwenden können.

![Screenshot mit Azure-Vorlagen](../media/5-browse-templates.png)

## <a name="using-github-templates"></a>Verwenden von GitHub-Vorlagen

Die Quelldateien der Vorlage sind in GitHub gespeichert. Sie können in GitHub zur Vorlage navigieren und direkt über die Seite die Bereitstellung in Azure durchführen.

![Screenshot mit GitHub-Vorlage und hervorgehobener Schaltfläche „Deploy to Azure“ (In Azure bereitstellen)](../media/5-deploy-from-github.png)

Bei der Bereitstellung der Vorlage wird in Azure eine Liste der Pflichteingabefelder angezeigt.

![Screenshot mit Vorlage im Azure-Portal](../media/5-fill-in-template.png)

Anschließend können Sie die Vorlage ausführen, um Ressourcen zu erstellen, anzupassen oder zu entfernen.

### <a name="running-templates-in-the-azure-portal"></a>Ausführen von Vorlagen im Azure-Portal

Wenn Sie bereits wissen, welche Vorlage Sie verwenden möchten, oder Vorlagen in Ihrem Azure-Konto gespeichert haben, können Sie über **Ressource erstellen** > **Vorlagenbereitstellung** nach definierten Vorlagen im Portal suchen und diese ausführen. Sie können anhand des Namens nach Vorlagen suchen, eine Vorlage bearbeiten, um die Parameter oder das Verhalten zu ändern, und die Vorlage direkt über die grafische Benutzeroberfläche ausführen.

### <a name="running-templates-from-the-command-line"></a>Ausführen von Vorlagen über die Befehlszeile

Mit einer Vorlagen-URL können Sie die Vorlage in Azure PowerShell ausführen. Beispielsweise könnten Sie die Verschlüsselungsvorlage für Datenträger mit dem folgenden PowerShell-Befehl ausführen:

```powershell
New-AzureRmResourceGroupDeployment `
    -Name encrypt-disk `
    -ResourceGroupName <resource-group-name> `
    -TemplateUri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-encrypt-running-windows-vm-without-aad/azuredeploy.json
```

Alternativ können Sie auch die Azure CLI und den Befehl `group deployment create` verwenden.

```azurecli
azure config mode arm
azure group deployment create <my-resource-group> <my-deployment-name> \ 
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-encrypt-running-windows-vm-without-aad/azuredeploy.json
```

