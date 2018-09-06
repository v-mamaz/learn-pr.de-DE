### <a name="exercise-6-use-the-app-to-classify-images"></a>Übung 6: Verwenden der App zum Klassifizieren von Bildern

In dieser Übung verwenden Sie die Artworks-App, um Bilder zur Klassifizierung an den Custom Vision Service zu senden. Die App nutzt JSON-Informationen, die von Aufrufen der [PredictImage](https://southcentralus.dev.cognitive.microsoft.com/docs/services/eb68250e4e954d9bae0c2650db79c653/operations/58acd3c1ef062f0344a42814)-Methode der Custom Vision-Vorhersage-API zurückgegeben wurden. Diese teilt mit, ob ein Bild ein Gemälde von Picasso, Rembrandt, Pollock oder von keinem der genannten Maler darstellt. Es wird auch die Wahrscheinlichkeit angegeben, dass die Klassifizierung, die dem Bild zugewiesen ist, richtig ist.

1. Klicken Sie auf die Schaltfläche **Browse (...)** (Durchsuchen) in der Artworks-App. 

    ![Suche nach lokalen Bildern in der Artworks-App](../images/app-click-browse.png)

    _Suche nach lokalen Bildern in der Artworks-App_ 

1. Navigieren Sie dann in den Ressourcen für die Aufgaben zum Ordner „Quick Tests“. Wählen Sie die Datei mit der Bezeichnung **PicassoTest_02.jpg** aus, und klicken Sie auf **Open** (Öffnen).

1. Klicken Sie auf die Schaltfläche **Predict** (Vorhersagen), um das Bild an den Custom Vision Service zu übermitteln.

    ![Übermitteln des Bilds an den Custom Vision Service](../images/app-click-predict.png)

    _Übermitteln des Bilds an den Custom Vision Service_ 

1. Bestätigen Sie, dass die App das Gemälde als einen Picasso erkennt.

    ![Klassifizieren des Bilds als einen Picasso](../images/app-prediction-01.png)

    _Klassifizieren des Bilds als einen Picasso_ 

1. Wiederholen Sie die Schritte 1 bis 3 für die Bilder **RembrandtTest_01.jpg** und **PollockTest_01.jpg**, und bestätigen Sie, dass die App Gemälde von Rembrandt und Pollock identifizieren kann.

    ![Klassifizieren des Bilds als einen Rembrandt](../images/app-prediction-02.png)

    _Klassifizieren des Bilds als einen Rembrandt_ 

1. Wiederholen Sie die Schritte 1 bis 3 für **VanGoghTest_01.png** und **VanGoghTest_02.png**, und bestätigen Sie, dass die App diese Meisterwerke von Van Gogh nicht als Gemälde von Picasso, Rembrandt oder Pollock identifiziert.

    ![Kein Picasso, Rembrandt oder Pollock](../images/app-prediction-03.png)

    _Kein Picasso, Rembrandt oder Pollock_ 

1. Wie Sie sehen können, ist die Verwendung einer Vorhersage-API einer App genauso verlässlich wie das Custom Vision Service-Portal, aber es macht noch viel mehr Spaß. Wenn Sie dann noch zu den Vorhersageseiten im Portal navigieren, finden Sie jedes Bild, das über die App hochgeladen wurde.
 
    ![Bild, das an den Custom Vision Service gesendet wurde](../images/portal-all-predictions.png)

    _Bild, das an den Custom Vision Service gesendet wurde_ 

Probieren Sie es einfach selbst mit eigenen Bildern aus, und beurteilen Sie die Erfahrenheit des Modells beim Identifizieren von Künstlern oder der Bestimmung, dass ein Bild keinen Picasso, Rembrandt oder Pollock darstellt. Wenn Sie das Modell trainieren möchten, sodass es auch Van Goghs erkennt, laden Sie einige Gemälde von Van Gogh hoch, markieren Sie diese mit „Van Gogh“, und trainieren Sie das Modell weiter. Der Intelligenz des Modells sind keine Grenzen gesetzt, wenn Sie bereit sind, es zu trainieren. Und denken Sie daran: je mehr Bilder Sie zum Trainieren zur Verfügung stellen, desto intelligenter wird das Modell.