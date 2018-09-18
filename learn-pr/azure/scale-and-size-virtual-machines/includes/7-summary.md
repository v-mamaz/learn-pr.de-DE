Sie haben zwei Möglichkeiten kennengelernt, um den Bedarf mit VMs zu decken. Wenn Ihre Auslastung vorhersehbar ist, können Sie über das Portal oder mit Skripten die Größe Ihrer VMs manuell anpassen. Für nicht planbare Bedarfsmuster eignen sich besser Skalierungsgruppen mit Autoskalierung, um Instanzen automatisch hinzuzufügen und zu entfernen, wenn sich der Bedarf ändert. Mehrere VMs bieten den zusätzlichen Vorteil, dass sie die Verfügbarkeit Ihres Systems erhöhen – denn eine ausgefallene VM stört Ihren Dienst nicht mehr.

## <a name="cleanup"></a>Cleanup

Für das Bereitstellen und Ausführen einer VM fallen Kosten für Ihr Abonnement an. Da Sie sämtliche VMs in der gleichen Ressourcengruppe erstellen, lässt sich Ihr Azure-Abonnement am einfachsten bereinigen, indem Sie die Ressourcengruppe entfernen. Dadurch werden alle ihre Inhalte entfernt. Führen Sie das folgende PowerShell-Cmdlet aus, wenn Sie die Übung beendet haben:

   ```powershell
   Remove-AzureRmResourceGroup -Name ExerciseRG
   ```

Wenn Sie aufgefordert werden, den Löschvorgang zu bestätigen, klicken Sie auf **Ja**. Der Befehl zum Löschen der Ressourcen kann mehrere Minuten in Anspruch nehmen.