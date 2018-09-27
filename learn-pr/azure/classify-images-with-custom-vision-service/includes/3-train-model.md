In dieser Einheit trainieren Sie das Modell mithilfe der Bilder, die Sie in der vorherigen Übung hochgeladen und markiert haben. Nach dem Trainieren können Sie ein Modell optimieren, indem Sie weitere markierte Bilder hochladen und das Training erneut durchführen.

1. Klicken Sie oben auf der Seite auf die Schaltfläche **Trainieren**, um das Modell zu trainieren. Jedes Mal, wenn Sie das Modell trainieren, wird eine neue Iteration erstellt. Custom Vision Service verwaltet mehrere Iterationen, was Ihnen ermöglicht, Ihren Fortschritt im Laufe der Zeit zu vergleichen.

    ![Trainieren des Modells](../media/2-portal-click-train.png)

1. Warten Sie darauf, dass der Trainingsprozess abgeschlossen wird. (Dies sollte nur wenige Sekunden in Anspruch nehmen.) Überprüfen Sie anschließend die angezeigten Trainingsstatistiken für die erste Iteration. 

    In den Ergebnissen werden zwei Kennzahlen für die Genauigkeit eines Modells angezeigt: **Genauigkeit** und **Trefferquote**. Angenommen, das Modell wurde mit drei Bildern von Picasso und drei Bildern von Van Gogh konfrontiert. Wir nehmen weiter an, dass zwei der Bilder von Picasso korrekt „Picasso“ zugeordnet wurden, aber dass auch zwei der Bilder von Van Gogh als „Picasso“ identifiziert wurden. In diesem Fall beträgt die **Genauigkeit** 50%, da zwei von vier Bildern richtig identifiziert wurden. Der Wert für die **Trefferquote** beträgt 67%, da zwei der drei Bilder von Picasso richtig identifiziert wurden.

    ![Ergebnisse des Modelltrainings](../media/2-portal-train-complete.png)

In der nächsten Übung testen Sie das Modell mithilfe des Features „Quick Test“ (Schnelltest), mit dem Sie Bilder an das Modell übermitteln und sehen können, wie diese aufgrund der durch die Trainingsbilder gesammelten Daten klassifiziert werden.

> [!TIP]
> Zusätzlich zum Trainieren des Modells mit der Benutzeroberfläche im Custom Vision-Portal können Sie es auch trainieren, indem Sie die [TrainProject](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d9a10a4a5f8549599f1ecafc435119fa/operations/58d5835bc8cb231380095bed)-Methode in der [Trainings-API für Custom Vision](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d9a10a4a5f8549599f1ecafc435119fa/operations/58d5835bc8cb231380095be3) aufrufen.