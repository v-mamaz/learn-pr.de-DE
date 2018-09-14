Die Out-of der Box-Experience mit einem Azure DevOps-Projekt erstellt, Build und Release-pipelines, die sinnvoll für die Technologien ausgewählt. Für dieses Modul erstellt Sie eine Build und Release-Pipeline, die sinnvoll für eine node.js-app, die in einem Container in einem Kubernetes-Cluster gehostet ist. 

Oft müssen wir passen Sie die Build- und Pipelines für bestimmte Aufgaben für unser Projekt. Die Build- und Release-Pipelines in VSTS sind zu 100 % angepasst. Sie können die Pipelines auszuführen, was auch immer Sie sie zu machen.

In dieser Einheit die Informationen Sie, zum Anpassen der Build- und releasepipelines.

## <a name="customize-the-build-pipeline"></a>Anpassen der Buildpipeline

Die Build-Engine in VSTS ist nur eine aufgabenausführung, die eine Aufgabe, nach dem anderen ausführen. Informationen zum Anpassen des Builds Sie nur hinzufügen oder entfernen Aufgaben und füllen Sie die richtigen Parameter für den Task.

Standardmäßig ist VSTS mit mehr als 100 Aufgaben, die Sie verwenden können. Wenn bestimmte Aktionen ausführen müssen, die nicht standardmäßig vorhanden, überprüfen Sie im Marketplace vorhanden sind, wird mehr als 700 erstellen und Veröffentlichen von Aufgaben, die heruntergeladen und verwendet werden können. Sie haben auch die Möglichkeit, eigene benutzerdefinierte Tasks erstellen.

Für diese Unit passen Sie die Buildpipeline durch die Installation von WhiteSource Bolt tun, Security-Überprüfung des Codes die Marketplace-Aufgaben.

1. Navigieren Sie zum Azure DevOps-Projekt im Azure-Portal, und klicken Sie auf den Link der Build-definition  
![Link erstellen](../media-drafts/3-buildlink.png)

2. Dadurch gelangen Sie auf der Seite "Erstellen von Pipelines". Klicken Sie auf der Build, und wählen Sie `Edit`  
![Edit Build](../media-drafts/3-editbuild2.png)

3. Dadurch gelangen Sie an der Builddefinition. Klicken Sie auf die `+` 1 der-Agent-Auftrag eine Aufgabe hinzu  
![Aufgabe hinzufügen](../media-drafts/3-addtask2.png)

4. Geben Sie im Textfeld `bolt` , und klicken Sie auf `Get it free`  
![Abrufen von weißen Quelle Bolt](../media-drafts/3-getwhitesourcebolt.png)

5. Dadurch gelangen Sie auf der WhiteSource Bolt-Marketplace-Seite. Klicken Sie auf `Get it free`.  
![WhiteSource Bolt kostenlos erhalten](../media-drafts/3-getwhitesourceboltfree2.png)

6. Wählen Sie Ihre Organisation Azure DevOps, und klicken Sie dann auf `Install`  
![Installieren](../media-drafts/3-installwsb.png)

7. WhiteSource Bolt zu aktivieren, indem Sie die Anweisungen hier befolgen <https://www.whitesourcesoftware.com/whitesource_bolt_visualstudio_2017/#activate>

8. Wechseln Sie zurück zu Ihrem Azure-Portal mit der DevOps-Projekt geladen, und klicken Sie auf der Build-Pipeline-link  
![Erstellen der Pipelinelink](../media-drafts/3-buildpipelinelink.png)

9. Wählen Sie den Build aus, und klicken Sie auf `Edit`  
![Edit Build](../media-drafts/3-editbuild2.png)

10. Klicken Sie auf die `+` Agentauftrag 1 eine Aufgabe hinzufügen, geben Sie im `bolt` in das Suchfeld ein, und klicken Sie auf `Add`  
![Hinzufügen von Bolts](../media-drafts/3-addwsbolt.png)

11. Dadurch wird die WhiteSource Bolt-Aufgabe zum unteren Rand der Liste hinzugefügt, ziehen Sie es an den Anfang  
![Bolt nach oben verschieben](../media-drafts/3-moveboltototopoftasklist.png)

12. Klicken Sie auf `Save & queue` , und wählen Sie `Save & queue`  
![Speichern und Warteschlange](../media-drafts/3-saveandqueue2.png)

13. Klicken Sie auf `Save & queue`.  
![Speichern und in die Warteschlange Schaltfläche](../media-drafts/3-saveandqueuebutton.png)

Dies speichert die geänderte Buildpipeline und fügt den Build. Nachdem der Build abgeschlossen ist, betrachten Sie den Build `WhiteSource Bolt Build Report`, sehen Sie der Quellcode von WhiteSource Bolt-Suche nach Sicherheitsrisiken überprüft wurde.

![Weiß Quellbericht](../media-drafts/3-whitesourcereport.png)

## <a name="customize-the-release-pipeline"></a>Anpassen der releasepipeline

Wie der Build die releasepipeline ist Task Runner und kann die gleiche Weise angepasst werden. Für diese Unit fügen Sie am Ende der Veröffentlichung ein Webleistungstests. Überprüfen, dass Ihre app bereitgestellt wird und erfolgreich im Kubernetes-Cluster ausgeführt wird.

1. Navigieren Sie zu den DevOps-Projekt im Azure-Portal, und klicken Sie auf den Link, um die releasepipeline  
![Releaselink](../media-drafts/3-releaselink.png)

2. Dadurch gelangen Sie auf der Seite der Release-Pipeline. Klicken Sie auf Ihre releasepipeline, und klicken Sie auf `Edit`  
![Release bearbeiten](../media-drafts/3-editreleasebutton.png)

3. Klicken Sie auf die Aufgaben in Ihrer Version `Dev` Phase  
![Freigabestufe](../media-drafts/3-releasestage2.png)

4. Klicken Sie auf die `+` Hinzufügen einer Aufgabe zu Phase 1, Typ `web test` in das Suchfeld ein, und klicken Sie auf `Add` für die Cloud-basierten Web Performance Test-Aufgabe  
![Fügen Sie Webtests hinzu.](../media-drafts/3-addwebtest2.png)

5. Bearbeiten Sie die schnellen Webleistungstest-Aufgabe, indem Sie darauf klicken und Hinzufügen der Url zu Ihrer app in der Website-URL (um die Url finden, wechseln zu Azure DevOps-Projekt-Portalseite und auf der rechten Seite mit der rechten Maustaste Beispiel externe Endpunkt und die Kopie-Link Ihrer app), und klicken Sie dann für die geplante tName, geben Sie im `Ping Test` und dann auf `Save`  
![URL kopieren](../media-drafts/3-copyurl.png)  
![Speichern Sie Webtest](../media-drafts/3-savewebtest.png)

Beim Ausführen einer Version, nach der Bereitstellung des neuen Pakets Helm ist ein Webtest führen Sie nun drücken die Url der app erfolgreich.

![Web-Testlauf](../media-drafts/3-webtestrun.png)

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie gelernt, wie Sie das Anpassen der Build- und releasepipelines. Sie haben zudem das Installieren und verwenden Aufgaben aus dem Marketplace.