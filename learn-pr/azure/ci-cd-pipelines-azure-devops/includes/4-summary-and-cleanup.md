Sie haben erfolgreich mit Azure DevOps-Projekten eine CI/CD-Pipeline für Ihre benutzerdefinierte Anwendung erstellt. 

## <a name="clean-up-resources"></a>Bereinigen von Ressourcen

Nachdem Sie die Arbeit an dieser CI/CD-Pipeline abgeschlossen haben, können Sie alle Ressourcen löschen, die während des Tutorials erstellt wurden.

1. Navigieren Sie im Azure-Portal zu `Resource Groups`, und klicken Sie auf `VstsResourceGroup-LearnCluster-xxxx`, wobei xxx eine zufällige Gruppen von Buchstaben und Zahlen ist.  
![LearnClusterRG](/media-draft/4-learnclusterrg.png)

2. Klicken Sie auf das DevOps-Projekt mit dem Namen `Learn`.  
![Link „Learn“](/media-draft/4-learnlink.png)

3. Klicken Sie auf `Delete`.  
![Löschen](/media-draft/4-deleteproj.png)

4. Klicken Sie auf `Yes`.  
![Ja](/media-draft/4-yes.png)

Hierdurch werden alle Ressourcen gelöscht, die in Azure erstellt wurden.

## <a name="summary"></a>Zusammenfassung

In diesem Tutorial haben Sie Folgendes gelernt:
> [!div class="checklist"]
> * Erstellen eines Azure DevOps-Projekts
> * Ersetzen der Beispiel-App im Azure DevOps-Projekt durch Ihre eigene
> * Anpassen der Build- und Releasepipelines
