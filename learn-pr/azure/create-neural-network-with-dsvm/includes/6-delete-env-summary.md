### <a name="exercise-6-delete-the-data-science-vm"></a>Übung 6: Löschen der Data Science-VM

In dieser Übung löschen Sie die Ressourcengruppe, die Sie in Übung 1 bei der Erstellung der Data Science-VM erstellt haben. Wenn Sie die Ressourcengruppe löschen, werden auch alle darin enthaltenen Elemente gelöscht. Dadurch wird sichergestellt, dass keine weiteren Kosten mehr anfallen. Gelöschte Ressourcengruppen können nicht wiederhergestellt werden. Achten Sie daher darauf, diese erst zu löschen, wenn Sie sie nicht mehr benötigen. Es ist jedoch **wichtig, diese Ressourcengruppe nicht länger als erforderlich bereitzustellen**, da Kosten für eine Data Science-VM anfallen.

1. Kehren Sie zum Blatt für die Ressourcengruppe zurück, die Sie in Übung 1 erstellt haben. Klicken Sie anschließend ganz oben auf dem Blatt auf **Ressourcengruppe löschen**.

    ![Löschen der Ressourcengruppe](../images/delete-resource-group.png)

    _Löschen der Ressourcengruppe_

1. Aus Sicherheitsgründen müssen Sie den Namen der Ressourcengruppe eingeben. Nach dem Löschen kann eine Ressourcengruppe nicht wiederhergestellt werden. Geben Sie den Namen der Ressourcengruppe ein. Klicken Sie anschließend auf **Löschen**, um alle Komponenten dieser Aufgabe aus dem Azure-Abonnement zu entfernen.

Nach einigen Minuten werden die Ressourcengruppe und alle zugehörigen Ressourcen gelöscht. Die Abrechnung endet mit dem Klick auf **Löschen**, sodass die erforderliche Zeit zum Löschen der Ressourcen nicht in Rechnung gestellt wird. Analog dazu beginnt die Abrechnung erst, nachdem die Ressourcen vollständig bereitgestellt wurden.

### <a name="summary"></a>Zusammenfassung

Die Schritte in dieser Aufgabe sind möglicherweise für das Ausführen anderer Arten von Bildklassifizierungsaufgaben generalisiert. Beispielsweise können Sie das gleiche TensorFlow-Modell zum Erkennen von Katzenbildern oder zum Identifizieren von defekten auf einem Fließband produzierten Einzelteilen trainieren. Die Bildklassifizierung gehört heute zu den häufigsten Verwendungszwecken des maschinellen Lernens, und ihre Zweckmäßigkeit wird sich im Laufe der Zeit nur erhöhen. Da Sie nun über eine Grundlage verfügen, auf der Sie aufbauen können, versuchen Sie, Ihre eigenen Modelle für die Bildklassifizierung zu erstellen. Man weiß nie, wie man davon profitieren kann.