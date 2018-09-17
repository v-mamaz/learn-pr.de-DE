Nach der Erstellung eines Azure DevOps-Projekts stellt sich natürlich die Frage, wie sich die Beispiel-App durch eine eigene App ersetzen lässt. In dieser Einheit lernen Sie zwei einfache Methoden dafür kennen.

1. Ersetzen des Codes im VSTS-Git-Repository durch Ihren eigenen Code

2. Verweisen Ihrer Buildpipeline auf ein externes Git-Repository mit Ihrem eigenen Code

## <a name="replacing-code-in-vsts-git-repository"></a>Ersetzen des Codes im VSTS-Git-Repository

Eine Möglichkeit besteht darin, einfach das Git-Repository in VSTS auf Ihrer Festplatte zu klonen, alles durch Ihren eigenen Code zu ersetzen und es anschließend wieder in VSTS hochzuladen. Daraufhin wird Ihr Code über die CI/CD-Pipeline erstellt und bereitgestellt.

In dieser Einheit laden Sie zunächst den Quellcode der Node.js-App herunter und speichern ihn auf Ihrer Festplatte.

1. Herunterladen des Quellcodes von <https://abelsharedblob.blob.core.windows.net/microsoftlearn/MicrosoftLearnDevOps.zip>

2. Extrahieren Sie den Inhalt von „MicrosoftLearnDevOps.zip“ an einem beliebigen Ort auf Ihrer Festplatte. In diesem Beispiel wurde `C:\users\abel\Downloads\MicrosoftLearnDevOps` verwendet.  
![Entzipptes Verzeichnis](/media-draft/2-unzippedfolder.png)

Als Nächstes müssen Sie das Repository auf Ihrer Festplatte klonen und die Beispiel-App durch Ihre eigene Node.js-App ersetzen. In dieser Einheit wird davon ausgegangen, dass Git bereits auf Ihrem Computer installiert ist.

1. Navigieren Sie im Azure-Portal zu Ihrem Azure DevOps-Projekt, und klicken Sie auf den Link zum Coderepository.  
![](/media-draft/2-browsetorepolink.png)

2. Klicken Sie auf „Klonen“, und kopieren Sie die URL für das Git-Repository (in der rechten oberen Ecke).  
![Kopieren der Klon-URL](/media-draft/2-copycloneurl.png)  
Daraufhin wird die Repository-URL in die Zwischenablage kopiert.

3. Klonen des Repositorys auf Ihrer Festplatte  
![Git Clone](/media-draft/2-gitclone.png)  
In diesem Beispiel wurde das Repository in „C:\Users\abel\Source\TripleCrown\DevOps“ geklont.

4. Löschen Sie alles aus Ihrem lokalen Repository (mit Ausnahme des Verzeichnisses `.git`).  
![Löschen aller Inhalte aus dem Repository](/media-draft/2-deleterepoofeverything.png)

5. Kopieren Sie den Quellcode für die heruntergeladene Node.js-App in den Repositoryordner.  
![Ersetzter Code](/media-draft/2-replacedeverything.png)

6. Fügen Sie Ihrem lokalen Repository sämtliche Änderungen hinzu, indem Sie `git add *` über die Befehlszeile eingeben.  
![Git: Alles hinzufügen](/media-draft/2-gitaddall.png)

7. Geben Sie `git commit -m "replace sample app with real code"` ein, um die Änderungen an Ihrem lokalen Repository zu committen.  
![Git: Committen](/media-draft/2-gitcommit.png)

8. Pushen Sie Änderungen mithilfe von `git push` wieder an das Git-Repository in VSTS.  
![Git: Pushen](/media-draft/2-gitpush.png)

9. Nach dem Pushen der Änderungen an VSTS sollte der Code Ihrer eigenen App den Buildvorgang durchlaufen.  
![Buildvorgang gestartet](/media-draft/2-buildkickedoff.png)  
![Buildvorgang in Aktion](/media-draft/2-buildinaction.png) und Releasepipeline bis Azure  
 ![Releasevorgang](/media-draft/2-releaserunning.png)

 Nach Abschluss der Bereitstellung können Sie sich im Azure-Portal vergewissern, dass Ihre eigene App bereitgestellt wurde.

 1. Navigieren Sie im Azure-Portal zu Ihrem Azure DevOps-Projekt, und klicken Sie auf der rechten Seite auf Ihre bereitgestellte App.  
 ![Link zum Starten der Beispiel-App](/media-draft/2-launchapp.png)

 2. Daraufhin wird die ausgeführte App in Ihrem Browser gestartet.  
 ![Ausgeführte App](/media-draft/2-apprunning.png)

## <a name="using-external-git-repo"></a>Verwenden eines externen Git-Repositorys

Eine weitere Möglichkeit, die Beispiel-App durch Ihren eigenen App-Code zu ersetzen, besteht darin, die Buildpipeline auf ein externes Git-Repository mit Ihrem App-Code zu verweisen. In diesem Beispiel laden Sie Ihren eigenen App-Code in ein GitHub-Repository hoch.

Gehen Sie anschließend wie folgt vor, um die Buildpipeline auf dieses GitHub-Repository zu verweisen:

1. Navigieren Sie im Azure-Portal zu Ihrem Azure DevOps-Projekt, und klicken Sie auf den Build-Link.  
![Build-Link](/media-draft/2-buildlink.png)

2. Dadurch gelangen Sie zu den Buildpipelines. Klicken Sie dort auf Ihre Buildpipeline und anschließend auf `Edit`.  
![Klicken auf „Build bearbeiten“](/media-draft/2-clickeditbuildlink.png)

3. Dadurch gelangen Sie zum Build-Editor. Klicken Sie auf `Get sources`.  
![Klicken auf „Get sources“ (Quellen abrufen)](/media-draft/2-clickgetsource.png)

4. Dadurch gelangen Sie zur Seite zum Auswählen einer Quelle. Beachten Sie, dass Sie für die Buildpipeline nicht nur VSTS-Git, sondern auch GitHub, GitHub Enterprise, Subversion, Bitbucket Cloud sowie jedes andere externe Repository auf Git-Basis verwenden können. Wählen Sie für diese Übung „GitHub“ aus.  
![Auswählen von GitHub](/media-draft/2-selectgithub.png)

5. Dadurch gelangen Sie zur GitHub-Verbindungsseite. Verwenden Sie entweder OAuth oder ein persönliches Zugriffstoken, um eine Verbindung mit Ihrem GitHub-Konto herzustellen.

6. Wählen Sie das GitHub-Repository mit Ihrem eigenen App-Code aus, und klicken Sie auf `Save & queue`.  
![Speichern und in Warteschlange einreihen](/media-draft/2-saveandqueue.png)

7. Klicken Sie auf die Schaltfläche `Save & queue`.  
![](/media-draft/2-saveandqueuedialog.png)

8. Daraufhin wird ein Speichervorgang ausgeführt und der Buildvorgang gestartet, sodass Ihr eigener, in GitHub gehosteter App-Code unsere Build- und Releasepipelines bis Azure durchläuft.  
![Ausgeführter Buildvorgang](/media-draft/2-buildrunning.png)

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie zwei Möglichkeiten kennengelernt, um den Beispielcode des DevOps-Projekts durch eigenen App-Code zu ersetzen: Sie können entweder den Code im VSTS-Git-Repository ersetzen oder die Buildpipeline mit einem anderen externen Repository verknüpfen, in dem sich Ihr App-Code befindet.

Als Nächstes erfahren Sie, wie Sie die Build- und Releasepipelines anpassen.