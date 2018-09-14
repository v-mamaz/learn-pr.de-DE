Das Einrichten einer CI/CD-Pipeline hat immer eine Herausforderung Aktionen schnell ausführen müssen. Jetzt ist es unglaublich einfach, die von NULL überhaupt zu einem vollständigen End-to-End-Azure DevOps-Projekt zu gelangen. Und in das Azure DevOps-Projekt, erhalten Sie Folgendes:

1. Die Infrastruktur in Azure für Sie bereitgestellt.

2. Ein Teamprojekt in einem VSTS-Instanz.

3. Der Quellcode für eine Beispiel-app in der Sprache, die Sie in das Repository Ihrer VSTS-Instanz ausgewählt.

4. Build und Release Pipeline, die sinnvoll für die Technologien, die ausgewählt ist.

Und wenn die ist fertig, das Azure DevOps Projekt ist die Beispielapp, erstellt und freigegeben wird über die Pipelines in die Infrastruktur, die sie die Bereitstellung für Sie Sie in Azure. Und Sie erhalten all dies mit nur wenigen Klicks.

## <a name="create-an-azure-devops-project"></a>Erstellen eines Azure DevOps-Projekts

Sie können ein Azure DevOps-Projekt erstellen, über das Azure-Portal.

1. Besuchen Sie die die [Azure-Portal](https://portal.azure.com) , und klicken Sie auf `Create a resource`  
![Azure-Portal](../media-drafts/1-azureportal.png)

2. Klicken Sie auf `DevOps Project`.  
![Wählen Sie DevOps-Projekt](../media-drafts/1-pickdevopsproject.png)

3. Der nächste Bildschirm lautet, erhalten Sie, welche Sprache auszuwählen, Sie verwenden möchten. Beachten Sie, wie Sie .NET (natürlich) auswählen können, Java, Knoten, Php, Python, Ruby und Go. Sie können sogar Ihren eigenen Code aus einem Git-Repository importieren. Für diese Einheit wir jetzt, und erstellen Sie eine Node.js-app. Klicken Sie auf Node.js, und klicken Sie auf Weiter  
![Node.js für Sprache auswählen](../media-drafts/1-picknodejsforlang.png)

4. Als Nächstes wird es Sie welches node.js-Framework bitten, Sie verwenden möchten. Wählen Sie für diese Einheit einfache Node.js-app aus, und klicken Sie auf Weiter  
![Wählen Sie den einfachen Knoten](../media-drafts/1-picksimplenode.png)

5. Als Nächstes wird aufgefordert, welche Infrastruktur Sie bereitstellen möchten, und führen Sie die app im jetzt? Stellen Sie für diese Einheit lassen Sie uns und in einem Kubernetes-Cluster mithilfe von Azure Kubernetes Service bereitstellen. Wählen Sie die Kubernetes Service aus, und klicken Sie auf Weiter  
![Auswählen von Kubernetes](../media-drafts/1-pickkubernetes.png)

6. Und nun Sie können eine neue Instanz von VSTS erstellen oder ein vorhandenes Zertifikat. Sie können auch ausgeführt, wo und wie Sie Ihren Kubernetes-Cluster möchten einrichten. Fahren Sie für diese Unit fort, und erstellen Sie eine neue VSTS-Instanz durch Auswahl von "Neu" auswählen, und geben Sie Ihre VSTS-Instanz einen eindeutigen Namen. Geben Sie Informationen für den Projektnamen, wählen Sie Ihr Azure-Abonnement, benennen Sie den Cluster Name LearnCluster, wählen Sie den Speicherort, und klicken Sie auf Fertig USA, Osten  
![](../media-drafts/1-finalconfirmation2.png)

Und das ist wirklich alles! Dies dauert eine Weile, also starten wieder, entspannen und überlassen Sie Azure, die die Sache einfach. In den meisten Fällen werden ausgegeben werden, bereitstellen und Konfigurieren von Ihrer Azure-Infrastruktur. Für dieses Modul wird dies auf Ihre Azure Kubernetes Service und Azure Container Registry-Instanz sein.

## <a name="a-lap-around-the-finished-azure-devops-project"></a>Eine runde um das fertige Azure DevOps-Projekt

Wenn Azure abgeschlossen ist, werden Sie in den Warnungen benachrichtigt werden

1. Klicken Sie auf die Warnung, und klicken Sie dann zu Ressource wechseln  
![Warnung zu Ressource wechseln](../media-drafts/1-gotoresourcefromalert.png)

2. Dadurch gelangen Sie zu einem Portal-Blatt, das alles, was bereitgestellt anzeigt. Ist Sie auf der linken Seite Ihre CI/CD-Pipeline ein. Sie haben Ihr coderepository, die Builddefinition, und auch Ihrer releasedefinition. Alle Verknüpfungen sind deep-Links, mit denen Sie direkt in die Ressource in VSTS. Und auf der rechten Seite sehen Sie die gesamte Infrastruktur, die Sie in Azure bereitgestellt. Sie haben Ihre Kubernetes-Cluster mit der Beispielapp, die bereits bereitgestellt und auch Application Insights. Auch hier sind alle diese Links deep-Links zu Ressourcen in Azure.  
![Portal DevOps Proj](../media-drafts/1-portaldevopsproj.png)

3. Klicken Sie auf den Link für Ihren Quellcode  
![Link zur Quelle](../media-drafts/1-linktosource.png)

4. Dadurch gelangen Sie auf das Git-Repository im Azure-Code. Beachten Sie, dass dies nur eines normalen Git-Repositorys, die mit der Beispiel-node.js-app mit Helm-Diagrammen ist.  
![Azure Repo](../media-drafts/1-azurerepo.png)

5. Wechseln Sie in den builds  
![Verknüpfen mit builds](../media-drafts/1-linktobuild.png)

6. Bearbeiten Sie die erstellten Build durch Klicken auf den Build, und klicken Sie dann auf Bearbeiten  
![Build bearbeiten](../media-drafts/1-editbuildlink2.png)

7. Sie sehen eine Buildpipeline, die sinnvoll für die Technologien, die ausgewählt ist. Da wir eine node.js-app in einem Kubernetes-Cluster ausgewählt haben, erhalten wir eine Buildpipeline, die Docker-Aufgaben für die Node.js-app erstellen, erstellen das Image-Container-Abbild und Helm dann Aufgaben zum Erstellen eines Helm-Pakets verwendet.  
![Erstellen der Pipeline](../media-drafts/1-buildpipeline2.png)

8. Wechseln Sie zu der releasepipeline, indem Sie auf `Releases`  
![Releaselink](../media-drafts/1-gotoreleaselink.png)

9. Sie sehen, dass die releasepipeline erstellt. Bearbeiten Sie, indem Sie auf der Version klicken und auswählen `Edit pipeline`  
![Release bearbeiten](../media-drafts/1-editrelease2.png)

10. Azure hat eine releasepipeline erstellt, die sinnvoll für die Technologien, die ausgewählt ist. Eine Node-app in einem Container in einem Kubernetes-Cluster gehostet wird.
![Releasepipeline](../media-drafts/1-releasepipeline2.png)  
![Release-Pipeline-Schritte](../media-drafts/1-pipelinesteps.png)

11. Wechseln Sie zurück zum Azure-Portal, und klicken Sie auf den externen Endpunkt für den Kubernetes-Dienst  
![](../media-drafts/1-clickonendpoint.png)

12. Sie sehen, dass die Beispiel-app erstellen und in Ihrem AKS-Cluster bereitgestellt  
![Ausgeführte App](../media-drafts/1-apprunning.png)

## <a name="summary"></a>Zusammenfassung

In dieser Einheit erstellt Sie ein Azure DevOps-Projekt, das besteht aus:

1. Infrastruktur für Ihre app – Azure Kubernetes Service und Application Insights

2. Ein Teamprojekt in einem VSTS-Instanz.

3. Der Quellcode für eine Node.js-Beispiel-app in einem Container in das Repository Ihrer VSTS-Instanz ausgeführt wird.

4. Build und Release Pipeline für eine Node.js-Container-app in Ihrem Azure Kubernetes Service-Instanz ausgeführt wird.

Als Nächstes erfahren Sie, wie Sie die Beispiel-app mit tatsächlichen app ersetzen.