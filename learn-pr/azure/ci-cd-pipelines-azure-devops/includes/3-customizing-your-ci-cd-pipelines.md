Über die bereitgestellte Benutzeroberfläche für ein Azure DevOps-Projekt werden Build- und Releasepipelines erstellt, die für die gewählten Technologiekomponenten sinnvoll sind. Für dieses Modul haben Sie eine Build- und Releasepipeline erstellt, die für eine Node.js-App geeignet ist, bei der die Ausführung in einem per Kubernetes-Cluster gehosteten Container erfolgt. 

Es ist häufig der Fall, dass wir die Build- und Releasepipelines anpassen müssen, um für ein Projekt bestimmte Anforderungen zu erfüllen. Die Build- und Releasepipelines in VSTS sind zu 100% anpassbar. Sie können die Pipelines so festlegen, wie Sie dies benötigen.

In dieser Einheit wird beschrieben, wie Sie Ihre Build- und Releasepipelines anpassen.

## <a name="customize-the-build-pipeline"></a>Anpassen der Buildpipeline

Die Build-Engine in VSTS ist lediglich eine Aufgabenausführung, über die eine Aufgabe nach der anderen ausgeführt wird. Zum Anpassen des Builds können Sie einfach Aufgaben hinzufügen und entfernen und die richtigen Parameter für die Aufgabe einfügen.

Standardmäßig verfügt VSTS über ca. 100 Aufgaben, die Sie verwenden können. Falls Sie eine Aufgabe durchführen müssen, die nicht standardmäßig vorhanden ist, werden Sie ggf. auf dem Marketplace fündig. Er enthält über 700 Build- und Releaseaufgaben, die heruntergeladen und genutzt werden können. Außerdem haben Sie die Möglichkeit, eigene benutzerdefinierte Aufgaben zu schreiben.

Für diese Einheit passen Sie die Buildpipeline an, indem Sie die Marketplace-Aufgaben installieren (WhiteSource-Bolt), um für den Code einen Sicherheitsscan durchzuführen.

1. Navigieren Sie im Azure-Portal zum Azure DevOps-Projekt, und klicken Sie auf den Link für die Builddefinition.  
![Build-Link](/media-draft/3-buildlink.png)

2. Sie gelangen zur Seite mit den Buildpipelines. Klicken Sie auf den Build, und wählen Sie `Edit`.  
![Bearbeiten des Builds](/media-draft/3-editbuild.png)

3. Sie gelangen zur Builddefinition. Klicken Sie auf das Pluszeichen (`+`), um Agent-Auftrag 1 eine Aufgabe hinzuzufügen.  
![Hinzufügen der Aufgabe](/media-draft/3-addtask.png)

4. Geben Sie im Textfeld `bolt` ein, und klicken Sie auf `Get it free`.  
![Get it free (Kostenlos)](/media-draft/3-getitfree.png)

5. Sie gelangen zur Marketplace-Seite für „WhiteSource-Bolt“. Klicken Sie auf `Get it free`.  
![White Source-Bolt – Kostenlos](/media-draft/3-getwhitesourceboltfree.png)

6. Wählen Sie Ihre VSTS-Organisation aus, und klicken Sie dann auf `Install`.  
![Installieren](/media-draft/3-install.png)

7. Aktivieren Sie den WhiteSource-Bolt, indem Sie die hier angegebene Anleitung verwenden: <https://www.whitesourcesoftware.com/whitesource_bolt_visualstudio_2017/#activate>.

8. Wechseln Sie zurück zu Ihrem Azure-Portal mit dem geladenen DevOps-Projekt, und klicken Sie auf den Link für die Buildpipeline.  
![Buildpipeline-Link](/media-draft/3-buildpipelinelink.png)

9. Wählen Sie Ihren Build aus, und klicken Sie auf `Edit`.  
![Bearbeiten des Builds](/media-draft/3-editbuild.png)

10. Klicken Sie auf „`+` Add a task to Agent job 1“, geben Sie `bolt` in das Suchfeld ein, und klicken Sie auf `Add`.  
![Hinzufügen des Bolts](/media-draft/3-addbolt.png)

11. Die WhiteSource-Boltaufgabe wird unten in der Aufgabenliste hinzugefügt. Ziehen Sie sie an den Anfang.  
![Bolt am Anfang der Liste](/media-draft/3-boltattop.png)

12. Klicken Sie auf `Save & queue`, und wählen Sie `Save & queue`.  
![Speichern und Einreihen in Warteschlange](/media-draft/3-saveandqueue.png)

13. Klicken Sie auf `Save & queue`.  
![Dialogfeld für Speichern und Einreihen in die Warteschlange](/media-draft/3-saveandqueuedialog.png)

Die geänderte Buildpipeline wird gespeichert, und der Build wird in die Warteschlange eingereiht. Wenn Sie sich nach Abschluss des Buildvorgangs den Build `WhiteSource Bolt Build Report` ansehen, erkennen Sie, dass der Quellcode vom WhiteSource-Bolt gescannt wurde, um nach Sicherheitsrisiken zu suchen.

![Buildbericht](/media-draft/3-buildreport.png)

## <a name="customize-the-release-pipeline"></a>Anpassen der Releasepipeline

Wie der Build auch, ist die Releasepipeline eine Aufgabenausführung, die auf die gleiche Weise angepasst werden kann. Für diese Einheit fügen Sie am Ende des Release einen Webleistungstest hinzu. Hiermit wird überprüft, ob Ihre App bereitgestellt und im Kubernetes-Cluster erfolgreich ausgeführt wird.

1. Navigieren Sie im Azure-Portal zum DevOps-Projekt, und klicken Sie auf den Link für die Releasepipeline.  
![Link für Release](/media-draft/3-releaselink.png)

2. Sie gelangen auf die Seite für Releasepipelines. Klicken Sie auf Ihre Releasepipeline und dann auf `Edit`.  
![Bearbeiten der Releasepipeline](/media-draft/3-editreleasepipeline.png)

3. Klicken Sie in der Releasestufe `Dev` auf die Aufgaben.  
![Releasestufe](/media-draft/3-releasestage.png)

4. Klicken Sie auf `+` (Add a task to Phase1), geben Sie im Suchfeld `web test` ein, und klicken Sie für die Aufgabe „Cloud-based Web Performance Test“ auf `Add`.  
![Hinzufügen eines Webtests](/media-draft/3-addwebtest.png)

5. Bearbeiten Sie die Aufgabe „Quick Web Performance Test“, indem Sie darauf klicken und die URL Ihrer App in der Website-URL hinzufügen. (Ermitteln Sie die URL, indem Sie im Azure-Portal rechts auf der Seite mit dem DevOps-Projekt mit der rechten Maustaste auf Ihren externen Endpunkt der Beispiel-App klicken und den Link kopieren.) Geben Sie als „TestName“ dann `Ping Test` ein.  
![Kopieren der URL](/media-draft/3-copyurl.png)  
![Bearbeiten der Webtestaufgabe](/media-draft/3-editwebtesttask.png)

6. Klicken Sie auf `Save`.  
![Speichern des Release](/media-draft/3-saverelease.png)

Wenn Sie jetzt einen Release ausführen, wird nach dem Bereitstellen des neuen Helm-Pakets ein Webtest durchgeführt, um zu überprüfen, ob die App-URL korrekt ist.

![Webtest](/media-draft/3-webtest.png)


## <a name="summary"></a>Zusammenfassung

In dieser Einheit wurde beschrieben, wie Sie Ihre Build- und Releasepipelines anpassen. Außerdem haben Sie erfahren, wie Sie Aufgaben auf dem Marketplace installieren und verwenden.