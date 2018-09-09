### <a name="exercise-3-train-the-model"></a>Übung 3: Trainieren des Modells

In dieser Übung trainieren Sie das Modell mithilfe der Bilder, die Sie in der vorherigen Übung hochgeladen und markiert haben. Das Training kann durch einen einfachen Klick auf eine Schaltfläche im Portal durchgeführt werden oder indem Sie die Methode [TrainProject](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d9a10a4a5f8549599f1ecafc435119fa/operations/58d5835bc8cb231380095bed) in der [Custom Vision-Schulungs-API](https://southcentralus.dev.cognitive.microsoft.com/docs/services/d9a10a4a5f8549599f1ecafc435119fa/operations/58d5835bc8cb231380095be3) aufrufen. Nach dem Training können Sie ein Modell optimieren, indem Sie weitere markierte Bilder hochladen und das Training erneut durchführen.
 
1. Klicken Sie oben auf der Seite auf die Schaltfläche **Trainieren**, um das Modell zu trainieren. Jedes Mal, wenn Sie das Modell trainieren, wird eine neue Iteration erstellt. Custom Vision Service verwaltet mehrere Iterationen, was Ihnen ermöglicht, Ihren Fortschritt im Laufe der Zeit zu vergleichen.

    ![Trainieren des Modells](../images/portal-click-train.png)

    _Trainieren des Modells_

1. Warten Sie darauf, dass der Trainingsprozess abgeschlossen wird. (Dies sollte nur wenige Sekunden in Anspruch nehmen.) Überprüfen Sie anschließend die angezeigten Trainingsstatistiken für die erste Iteration. **Genauigkeit** und **Trefferquote** werden zwar separat aufgeführt, jedoch stellen sie zusammenhängende Messwerte für die Genauigkeit des Modells dar. Angenommen, dem Modell werden jeweils drei Werke von Picasso und Van Gogh vorgeführt, und das Modell identifiziert zwei Bilder von Picasso als „Picasso-Bilder“, aber identifiziert zwei der Bilder von Van Gogh fälschlicherweise als Bilder von Picasso. Dann würde die Genauigkeit 50 % betragen (zwei der vier Bilder, die als Bilder von Picasso identifiziert wurden, sind tatsächlich Picasso-Bilder), während die Trefferquote 67 % beträgt (zwei der drei Bilder von Picasso wurden richtig identifiziert). Weitere Informationen zur Genauigkeit und Trefferquote finden Sie unter https://en.wikipedia.org/wiki/Precision_and_recall.

    ![Ergebnisse des Trainings des Modells](../images/portal-train-complete.png)

    _Ergebnisse des Trainings des Modells_ 

Jetzt testen Sie das Modell mithilfe des Features „Quick Test“ (Schnelltest), mit dem Sie Bilder an das Modell übermitteln und sehen können, wie diese aufgrund der durch die Trainingsbilder gesammelten Daten klassifiziert werden.