Container sind eine moderne Möglichkeit für die Bereitstellung von Anwendungs- und Computeprozessen. Wenn Sie Container verwenden, werden Anwendungen und alle Abhängigkeiten in das sogenannte *Containerimage* gepackt. Containerimages sind sehr portierbar, da sie eine Containerimageregistrierung verwenden. Sie können ein Containerimage auf Ihrem Entwicklungssystem erstellen und dann ohne zusätzliche Änderung eine Instanz dieses Images in einem Azure-Rechenzentrum ausführen.

## <a name="container-efficiencies"></a>Containereffizienz

Container und Containerimages werden so erstellt, dass sie Hostressourcen, wie z.B. Speicherplatz, Arbeitsspeicher und CPU effizient verwenden. Aufgrund dieser Effizienz starten Container schnell. In manchen Fällen erfolgt das Starten einer Containerinstanz fast unmittelbar. Dies ermöglicht nicht nur ein schnelles Bereitstellen von Anwendungen, sondern auch ein neues Modell für die bedarfsgesteuerte Verarbeitung und Skalierungsvorgänge.

Szenario: Sie führen einen Batchverarbeitungsdienst aus, bei dem gelegentlich große Bedarfsspitzen angezeigt werden. Durch die Verwendung von Containern können Sie ein System erstellen, das auf höheren Bedarf reagiert, indem schnell neue Containerinstanzen bereitgestellt werden, um die höheren Anforderungen zu erfüllen. Dies bedarf einer leistungsfähigen Methode und ist mit herkömmlichen virtuellen Computern nicht einfach zu erreichen.

Zusätzlich zum schnellen Starten können Sie mit Containern „extreme Kompaktheit“ erzielen. Dies bedeutet, dass Sie weitere Anwendungen und Prozesse mit geringeren virtuellen oder physischen Ressourcen ausführen können.

## <a name="use-cases"></a>Anwendungsfälle

Container sind eine hervorragende Plattform für herkömmliche Workloads (z.B. Webserver) und bieten darüber hinaus noch weitere Möglichkeiten wie etwa burstfähige Batchverarbeitung, Anwendungen mit moderner und verteilter Architektur und alles andere, was eine bedarfsgesteuerte Skalierung erfordert.

## <a name="learning-objectives"></a>Lernziele

In diesem Modul lernen Sie Folgendes:

- Vorbereiten einer lokalen Containerentwicklungsumgebung
- Grundlegende Docker-Vorgänge
- Ausführen, Auflisten und Löschen von Containern
- Erstellen eines benutzerdefinierten Containerimages
- Übertragen Sie Containerimages per Push an eine öffentliche Containerregistrierung, und führen Sie Container über diese Images aus.
