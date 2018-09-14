Sie haben erfolgreich eine CI/CD-Pipeline für Ihre benutzerdefinierte Anwendung, die mit Azure DevOps-Projekten erstellt. 

## <a name="clean-up-resources"></a>Bereinigen von Ressourcen

Wenn Sie fertig sind arbeiten mit diesem CI/CD-Pipeline, können Sie alle während des Tutorials erstellte Ressourcen löschen.

1. Navigieren Sie im Azure-Portal zu `Resource Groups` und klicken Sie auf `VstsResourceGroup-LearnCluster-xxxx` Xxx ist, in dem zufälligen Gruppen von Buchstaben und Zahlen  
![LearnClusterRG](../media-drafts/4-learnclusterrg.png)

2. Klicken Sie auf das DevOps-Projekt mit dem Namen `Learn`  
![Link "Details"](../media-drafts/4-learnlink.png)

3. Klicken Sie auf `Delete`.  
![Löschen](../media-drafts/4-deleteproj.png)

4. Klicken Sie auf `Yes`.  
![Ja](../media-drafts/4-yes.png)

Hierdurch werden alle Ressourcen in Azure erstellt wurde gelöscht.

## <a name="summary"></a>Zusammenfassung

In diesem Tutorial haben Sie Folgendes gelernt:
> [!div class="checklist"]
> * Erstellen eines Azure DevOps-Projekts
> * Ersetzen Sie die Beispiel-app in das Azure DevOps-Projekt durch Ihre eigenen
> * Passen Sie den Build und Release-pipelines
