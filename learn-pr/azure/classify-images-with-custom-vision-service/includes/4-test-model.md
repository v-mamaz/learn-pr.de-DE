Später erstellen Sie in diesem Modul eine Node.js-App, die das Modell verwendet, um den Künstler von Bildern zu identifizieren, die ihr vorgeführt werden. Sie müssen jedoch keine App schreiben, um das Modell zu testen. Sie können Ihre Tests im Portal ausführen und das Modell mithilfe der Bilder, die Sie zum Testen verwenden, weiter optimieren. In dieser Einheit testen Sie mithilfe für Sie bereitgestellter Bilder die Fähigkeit des Modells, den Künstler eines Gemäldes zu identifizieren.

1. Klicken Sie ganz oben auf der Seite auf **Quick Test** (Schnelltest).

    ![Testen des Modells](../media-draft/4-portal-click-quick-test.png)

1. Klicken Sie auf **Lokale Dateien durchsuchen**, und navigieren Sie dann in den Modulressourcen zum Ordner „Quick Tests“. Wählen Sie **PicassoTest_01.jpg** aus, und klicken Sie auf **Öffnen**.

    ![Auswählen eines Picasso-Testbilds](../media-draft/4-portal-select-test-01.png)

1. Überprüfen Sie die Ergebnisse des Tests im Dialogfeld „Quick Test“. Mit welcher Wahrscheinlichkeit ist das Gemälde von Picasso? Mit welcher Wahrscheinlichkeit ist es von Rembrandt oder Pollock?

1. Schließen Sie das Dialogfeld „Quick Test“. Klicken Sie dann am oberen Rand der Seite auf **Vorhersagen**.

    ![Anzeigen der Tests, die durchgeführt wurden](../media-draft/4-portal-select-predictions.png)

1. Klicken Sie auf das Testbild, das Sie hochgeladen haben, um eine Detailansicht anzuzeigen. Markieren Sie das Bild dann als ein „Picasso“, indem Sie in der Dropdownliste **Picasso** auswählen und auf **Speichern und schließen** klicken.

    > Indem Sie die Testbilder auf diese Weise markieren, können Sie das Modell optimieren, ohne zusätzliche Trainingsbilder hochzuladen.
 
    ![Markieren des Testbilds](../media-draft/4-tag-test-image.png)

1. Führen Sie einen weiteren Schnelltest mit der Datei **FlowersTest.jpg** im Ordner „Quick Test“ durch. Vergewissern Sie sich, dass diesem Bild eine niedrige Wahrscheinlichkeit zugeordnet ist, von Picasso, Rembrandt oder Pollock zu stammen.

Das Modell wurde trainiert und ist einsatzbereit, es scheint erfahren im Identifizieren von Gemälden gewisser Künstler zu sein. Gehen Sie nun einen Schritt weiter, und integrieren Sie die Intelligenz des Modells in eine App.