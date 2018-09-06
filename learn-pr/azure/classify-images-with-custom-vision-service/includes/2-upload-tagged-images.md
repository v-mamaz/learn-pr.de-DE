### <a name="exercise-2-upload-tagged-images"></a>Übung 2: Hochladen von markierten Bildern

In dieser Übung fügen Sie Bilder berühmter Originalwerke von Picasso, Pollock und Rembrandt dem Artworks-Projekt hinzu und markieren die Bilder, damit der Custom Vision Service lernen kann, die Künstler voneinander zu unterscheiden.
  
1. Klicken Sie auf **Bilder hinzufügen**, um dem Projekt Bilder hinzuzufügen.

    ![Hinzufügen von Bildern zum Artworks-Projekt](../images/portal-click-add-images.png)

    _Hinzufügen von Bildern zum Artworks-Projekt_ 
 
1. Klicken Sie auf **Lokale Dateien durchsuchen**.

    ![Suchen nach lokalen Bildern](../images/portal-click-browse-local-files.png)

    _Suchen nach lokalen Bildern_ 
 
1. Navigieren Sie in den [Ressourcen, die diese Übung begleiten](https://a4r.blob.core.windows.net/public/cvs-resources.zip), zum Ordner „Artists\Picasso“, wählen Sie alle Dateien im Ordner aus, und klicken Sie auf **Öffnen**.

    ![Auswahl eines Bildes](../images/fe-browse-picasso-01.png)

    _Auswahl eines Bildes_ 
 
1. Geben Sie „painting“ (Gemälde) (ohne Anführungszeichen) in das Feld **Ein paar Tags hinzufügen...** ein. Klicken Sie dann auf **+**, um das Tag den Bildern zuzuweisen.

    ![Hinzufügen eines „painting“-Tags zu den Bildern](../images/portal-add-tags-01.png)

    _Hinzufügen eines „painting“-Tags zu den Bildern_ 

1. Wiederholen Sie Schritt 4, um den Bildern ein „Picasso“-Tag hinzuzufügen.

1. Klicken Sie auf **7 Dateien hochladen**, um die Bilder hochzuladen. Nachdem der Upload abgeschlossen ist, klicken Sie auf **Fertig**.

    ![Hochladen von markierten Bildern](../images/upload-picasso-images.png)

    _Hochladen von markierten Bildern_ 

1. Vergewissern Sie sich, dass die Bilder, die Sie hochgeladen haben, zusammen mit den ihnen zugewiesenen Tags im Portal angezeigt werden.

    ![Die hochgeladenen Bildern](../images/portal-tagged-01.png)

    _Die hochgeladenen Bildern_ 

1. Mit sieben Bildern von Picasso kann der Custom Vision Service Originalwerke von Picasso einigermaßen zuverlässig identifizieren. Aber wenn Sie das Modell gerade jetzt trainiert haben, würde es nur verstehen, wie ein Picasso aussieht, und wäre nicht in der Lage, Originalwerke anderer Künstler zu identifizieren.

    Im nächsten Schritt werden einige Originalwerke eines anderen Künstlers hochgeladen. Klicken Sie auf **Bilder hinzufügen**, und wählen Sie alle Bilder im Ordner „Artists\Rembrandt“ in den Lab-Ressourcen aus. Markieren Sie sie mit den Bezeichnungen „painting“ und „Rembrandt“ (nicht „Picasso“), und laden Sie sie in das Projekt hoch.

    > Wenn Sie das Tag „painting“ hinzufügen, müssen Sie es nicht erneut eingeben. Sie können es aus der Dropdownliste auswählen, die dem Feld **Ein paar Tags hinzufügen...** angefügt ist, wie unten dargestellt. Sie **müssen** „Rembrandt“ eingeben und auf **+** klicken, um ein „Rembrandt“-Tag hinzuzufügen.

    ![Auswahl eines vorhandenen Tags](../images/select-painting-tag.png)

    _Auswahl eines vorhandenen Tags_ 

1. Vergewissern Sie sich, dass die Bilder Rembrandts zusammen mit den Bildern Picassos im Projekt angezeigt werden, und dass „Rembrandt“ in der Liste der Tags angezeigt wird.

    ![Bilder von Picasso und Rembrandt](../images/portal-tagged-02.png)

    _Bilder von Picasso und Rembrandt_ 

1. Fügen Sie nun Originalwerke des geheimnisvollen Künstlers Jackson Pollock hinzu, damit der Custom Vision Service Originalwerke Pollocks ebenfalls erkennen kann. Wählen Sie alle Bilder im Ordner „Artists\Pollock“ in den Lab-Ressourcen aus, markieren Sie sie mit den Begriffen „painting“ und „Pollock“, und laden Sie sie in das Projekt hoch.

Wenn die markierten Bilder hochgeladen sind, trainieren Sie im nächsten Schritt das Modell mit diesen Bildern, damit es sowohl zwischen Originalwerken von Picasso, Rembrandt und Pollock unterscheiden als auch bestimmen kann, ob ein Gemälde eine Arbeit eines dieser berühmten Künstler ist.