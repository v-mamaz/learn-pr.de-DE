Die Einrichtung einer CI/CD-Pipeline war bislang immer etwas zeitaufwendig. Ab sofort können Sie jedoch ganz einfach ein vollständiges Azure DevOps-Projekt erstellen. Dieses Azure DevOps-Projekt bietet Folgendes:

1. Eine für Sie in Azure bereitgestellte Infrastruktur.

2. Ein Teamprojekt in einer VSTS-Instanz.

3. Quellcode für eine Beispiel-App in der Sprache, die Sie im Repository Ihrer VSTS-Instanz ausgewählt haben.

4. Eine geeignete Build- und Releasepipeline für die gewählten Technologien.

Das fertige Azure DevOps-Projekt verwendet die Beispiel-App und erstellt/veröffentlicht sie über die Pipelines in der Infrastruktur, die für Sie in Azure bereitgestellt wird. Für all das sind nur wenige Klicks erforderlich.

## <a name="create-an-azure-devops-project"></a>Erstellen eines Azure DevOps-Projekts

Sie erstellen ein Azure DevOps-Projekt über das Azure-Portal.

1. Klicken Sie im [Azure-Portal](https://portal.azure.com) auf `Create a resource`.  
![](/media-draft/1-azureportal.png)

2. Klicken Sie auf `DevOps Project`.  
![Auswählen von „DevOps-Projekt“](/media-draft/1-pickdevopsproject.png)

3. Auf dem nächsten Bildschirm können Sie die gewünschte Sprache auswählen. Sie haben die Wahl zwischen .NET, Java, Node.js, PHP, Python, Ruby und Go. Sie können sogar eigenen Code aus einem Git-Repository verwenden. In dieser Einheit erstellen wir eine Node.js-App. Klicken Sie auf „Node.js“ und anschließend auf „Weiter“.  
![Auswählen von „Node.js“ als Sprache](/media-draft/1-picknodejsforlang.png)

4. Als Nächstes werden Sie gefragt, welches Node.js-Framework Sie verwenden möchten. Wählen Sie für diese Einheit die Option „Einfache Node.js-App“ aus, und klicken Sie auf „Weiter“.  
![Auswählen von „Einfache Node.js-App“](/media-draft/1-picksimplenode.png)

5. Als Nächstes werden Sie gefragt, in welcher Infrastruktur Sie Ihre App bereitstellen und ausführen möchten. In dieser Einheit verwenden wir als Bereitstellungsziel einen Kubernetes-Cluster mit Azure Kubernetes Service. Wählen Sie „Kubernetes-Dienst“ aus, und klicken Sie auf „Weiter“.  
![Auswählen von „Kubernetes“](/media-draft/1-pickkubernetes.png)

6. Nun können Sie entweder eine ganz neue VSTS-Instanz erstellen oder eine bereits vorhandene Instanz auswählen. Außerdem können Sie festlegen, wo und wie Ihr Kubernetes-Cluster ausgeführt werden soll. Erstellen Sie im Rahmen dieser Einheit eine neue VSTS-Instanz. Klicken Sie dazu auf „Neu auswählen“, und geben Sie Ihrer VSTS-Instanz einen eindeutigen Namen. Geben Sie „Learn“ als Projektname ein, wählen Sie Ihr Azure-Abonnement aus, nennen Sie den Cluster „LearnCluster“, wählen Sie den Standort „USA, Osten“ aus, und klicken Sie anschließend auf „Fertig“.  
![Abschließender Bestätigungsbildschirm](/media-draft/1-finalconfirmation.png)

Und das war's auch schon! Die Einrichtung dauert zwar eine Weile, läuft aber vollständig automatisch ab. Die meiste Zeit wird für die Bereitstellung und Konfiguration Ihrer Azure-Infrastruktur benötigt. In diesem Modul sind das die Instanzen von Azure Kubernetes Service und Azure Container Registry.

## <a name="a-lap-around-the-finished-azure-devops-project"></a>Übersicht über das fertige Azure DevOps-Projekt

Nach Abschluss des Vorgangs erhalten Sie eine Benachrichtigung.

1. Klicken Sie auf die Benachrichtigung, und navigieren Sie zur Ressource.  
![Navigieren zur Ressource über die Benachrichtigung](/media-draft/1-gotoresourcefromalert.png)

2. Dadurch gelangen Sie zu einem Portal-Blatt, auf dem alle bereitgestellten Elemente angezeigt werden. Auf der linken Seite befindet sich Ihre CI/CD-Pipeline. Sie haben Ihr Coderepository, Ihre Builddefinition und auch Ihre Releasedefinition. Alle Links sind Deep-Links, über die Sie direkt zur Ressource in VSTS gelangen. Auf der rechten Seite sehen Sie die gesamte Infrastruktur, die für Sie in Azure bereitgestellt wurde. Sie haben Ihren Kubernetes-Cluster mit bereits bereitgestellter Beispiel-App sowie Application Insights. Auch diese Links sind Deep-Links, die direkt zu den Ressourcen in Azure führen.  
![DevOps-Projekt im Portal](/media-draft/1-pickdevopsproject.png)

3. Klicken Sie auf den Link für Ihren Quellcode.  
![Link zum Quellcode](/media-draft/1-linktosource.png)

4. Dadurch gelangen Sie zum Git-Repository in Ihrem VSTS-Projekt. Wie Sie sehen, handelt es sich hierbei um ein ganz normales Git-Repository, das die Node.js-Beispiel-App mit Helm-Diagrammen enthält.  
![VSTS-Repository](/media-draft/1-vstsrepo.png)

5. Navigieren Sie zu den Builds.  
![Link zu Builds](/media-draft/1-navtobuild.png)

6. Bearbeiten Sie den erstellten Build, indem Sie auf den Build und anschließend auf „Bearbeiten“ klicken.  
![](/media-draft/1-editbuildlink.png)

7. Daraufhin wird eine geeignete Buildpipeline für die gewählten Technologien angezeigt. Da wir uns für eine Node.js-App in einem Kubernetes-Cluster entschieden haben, erhalten wir eine Buildpipeline, die mithilfe von Docker-Aufgaben die Node.js-App erstellt, das Containerimage erstellt und anschließend mithilfe von Helm-Aufgaben ein Helm-Paket erstellt.  
![Buildpipeline](/media-draft/1-buildpipeline.png)

8. Klicken Sie auf `Releases`, um zur Releasepipeline zu gelangen.  
![Navigieren zu „Releases“](/media-draft/1-gotoreleases.png)

9. Die erstellte Releasepipeline wird angezeigt. Klicken Sie zur Bearbeitung auf das Release und anschließend auf `Edit pipeline`.  
![Bearbeiten des Release](/media-draft/1-editrelease.png)

10. Azure hat eine geeignete Releasepipeline für die gewählten Technologien erstellt. Eine Node-App, die in einem Container ausgeführt wird, der wiederum in einem Kubernetes-Cluster gehostet wird.
![Releasepipeline](/media-draft/1-releasepipeline.png)

11. Kehren Sie zum Azure-Portal zurück, und klicken Sie auf den externen Endpunkt für den Kubernetes-Dienst.  
![](/media-draft/1-clickonendpoint.png)

12. Daraufhin sollte die Beispiel-App angezeigt werden, die in Ihrem AKS-Cluster erstellt und bereitgestellt wurde.  
![Ausgeführte App](/media-draft/1-apprunning.png)

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie ein Azure DevOps-Projekt mit Folgendem erstellt:

1. Infrastruktur für Ihre App (Azure Kubernetes Service und Application Insights)

2. Ein Teamprojekt in einer VSTS-Instanz.

3. Quellcode für eine Node.js-Beispiel-App, die in einem Container im Repository Ihrer VSTS-Instanz ausgeführt wird.

4. Eine Build- und Releasepipeline für eine Node.js-Container-App, die in Ihrer Azure Kubernetes Service-Instanz ausgeführt wird.

Als Nächstes erfahren Sie, wie Sie die Beispiel-App durch Ihre eigene App ersetzen.