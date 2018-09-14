Nach dem Erstellen eines Azure DevOps-Projekts, ist als erstes Fragen Sie alle Benutzer an, wie Sie die Beispiel-app mit Ihrer eigenen app ersetzt werden? Es ist ziemlich einfach, und in diesem Kapitel lernen Sie zwei Methoden zur Auswahl.

1. Ersetzen den Code im VSTS-Git-Repository mit Ihrem tatsächlichen code

2. Zeigen Ihre Buildpipeline zu einem externen Git-Repository mit den tatsächlichen code

## <a name="replacing-code-in-vsts-git-repository"></a>Ersetzen Code in VSTS-Git-repository

Eine einfache Möglichkeit ist durch Klonen des Git-Repositorys in VSTS auf Ihrer Festplatte, und Ersetzen alles, was mit Ihrem eigenen Code, der an VSTS und tataa hochzuladen. Code wird nun erstellt und bereitgestellt, über die CI/CD-Pipeline.

Für diese Einheit werden Sie zunächst herunterladen und speichern den Quellcode der node.js-App auf Ihrer Festplatte.

1. Herunterladen des Quellcodes aus <https://abelsharedblob.blob.core.windows.net/microsoftlearn/MicrosoftLearnDevOps.zip>

2. Extrahieren Sie den Inhalt der MicrosoftLearnDevOps.zip an einer beliebigen Stelle auf der Festplatte freigeben. In diesem Beispiel `C:\users\abel\Downloads\MicrosoftLearnDevOps` verwendet wurde  
![Verpackten Verzeichnis der](../media-drafts/2-unzippedfolder.png)

Als Nächstes müssen Sie zum Klonen des Repositorys auf Ihrer Festplatte, und ersetzen die Beispiel-app mit der echten node.js-app. Diese Einheit wird davon ausgegangen, dass Sie bereits über Git auf Ihrem Computer installiert haben.

1. Klicken Sie im Azure-Portal navigieren Sie zu Ihrer Azure DevOps-Projekt, und klicken Sie auf den Code-Repository-Link.  
![](../media-drafts/2-browsetorepolink.png)

2. Klicken Sie auf klonen, und kopieren Sie die Url für das Git-Repository in der oberen rechten Ecke.  
![Repository Klonen](../media-drafts/2-clonerepo2.png) wird dadurch die Repository-Url in die Zwischenablage kopieren

3. Klonen Sie das Repository auf Ihre Festplatte  
![Git-Klon](../media-drafts/2-gitclone.png)  
In diesem Beispiel wurde auf C:\Users\abel\Source\TripleCrown\DevOps das Repository geklont haben.

4. Löschen Sie alles aus Ihrem lokalen Repository mit Ausnahme der `.git` Verzeichnis  
![Alles, was-Repository löschen](..//media-drafts/2-deleterepoofeverything.png)

5. Kopieren Sie den Quellcode für die heruntergeladenen node.js-app in den Ordner "Repo"  
![Ersetzte Code](../media-drafts/2-replacedeverything.png)

6. Alle Änderungen in Ihrem lokalen Repository hinzufügen, indem Sie eingeben `git add *` über die Befehlszeile  
![Fügen Sie alle Git hinzu](../media-drafts/2-gitaddall.png)

7. Änderungen Sie in Ihrem lokalen Repository eingeben `git commit -m "replace sample app with real code"`  
![Git-Commit](../media-drafts/2-gitcommit.png)

8. Änderungen per Push zurück in das Git-Repository in VSTS mit `git push`  
![Git-Push](../media-drafts/2-gitpush.png)

9. Dies sollte den tatsächlichen app-Code durch den Build senden, nach rückübertragung von Änderungen in VSTS,  
![Nutzen Sie initiiert die](../media-drafts/2-buildkickedoff2.png)
![Build ausgeführten](../media-drafts/2-buildrunning2.png) und der releasepipeline bis hin zu Azure  
 ![Version ausgeführt wird](../media-drafts/2-releaserunning2.png)

 Nachdem die Bereitstellung abgeschlossen ist, können Sie überprüfen, ob die tatsächliche app bereitgestellt wurde, dazu wieder auf das Azure-portal

 1. Wechseln Sie zum Azure-Portal, navigieren Sie zu Ihrem Azure DevOps-Projekt, und klicken Sie auf Ihrer bereitgestellten app in der rechten Seite  
 ![Starten Sie die Beispiel-App-Link](../media-drafts/2-launchapp.png)

 2. Dadurch wird die ausgeführte app in Ihrem browser  
 ![Ausgeführte App](../media-drafts/2-apprunning.png)

## <a name="using-external-git-repo"></a>Verwenden von externen Git-Repository

Eine weitere Möglichkeit zum Auslagern der Beispiel-app mit echten app-Code ist, zeigen Sie die Buildpipeline mit einem externen Git-Repository, die Ihrem app-Code enthält. In diesem Beispiel laden Sie den tatsächlichen app-Code in einem Github-Repository hoch.

Gehen Sie nach dem tatsächlichen Code in Github hochladen zum Buildpipeline auf diesem Github-Repository zu verweisen.

1. Klicken Sie im Azure-Portal navigieren Sie zu Ihrem Azure DevOps-Projekt, und klicken Sie auf den Build-link  
![Link erstellen](../media-drafts/2-buildlink.png)

2. Dadurch gelangen Sie auf die Erstellung von Pipelines, klicken Sie auf der Buildpipeline und klicken Sie dann `Edit`  
![Klicken Sie auf Bearbeiten-Buildpipeline](../media-drafts/2-editbuildpipelinelink.png)

3. Dadurch gelangen Sie auf dem Build-Editor, klicken Sie auf `Get sources`  
![Klicken Sie auf Get-Source-Aufgabe](../media-drafts/2-clickgetsourcetask.png)

4. Dadurch gelangen Sie zum Auswählen einer Seite "Quelle". Beachten Sie, wie Sie nicht nur VSTS-Git verwenden können, aber auch GitHub, GitHub Enterprise, Subversion, Bitbucket-Cloud und einem beliebigen externen Git-Repository für die Buildpipeline basieren. Wählen Sie für diese Übung GitHub  
![Wählen Sie GitHub](../media-drafts/2-selectgithub2.png)

5. Dadurch gelangen Sie auf der GitHub-Seite "Verbindung". Verwenden Sie OAuth oder ein persönliches Zugriffstoken für die Verbindung mit Ihrem GitHub-Konto

6. Wählen Sie das Github-Repository mit den tatsächlichen app-Code aus, und klicken Sie auf `Save & queue`  
![Speichern und Warteschlange](../media-drafts/2-saveandqueue2.png)

7. Klicken Sie auf die `Save & queue` Schaltfläche  
![Speichern und in die Warteschlange Schaltfläche](../media-drafts/2-saveandqueuebutton.png)

8. Dadurch speichert und definierten sicherheitsschwellwerte der Build, und Senden der echten app code gehosteten in GitHub über unser Build und releasepipelines bis hin zu Azure  
![Der Build wird ausgeführt](../media-drafts/2-buildpipelinerunning.png)

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie zwei Möglichkeiten, dem Beispielcode in die DevOps-Projekt mit einer echten app-Code zu ersetzen. Dies kann entweder durch den Code im VSTS-Git-Repository oder durch das Verknüpfen von der Buildpipeline mit einer anderen externes Repository mit Ihrem app-Code erfolgen.

Als Nächstes erfahren Sie, wie zum Anpassen von die Build- und releasepipelines.