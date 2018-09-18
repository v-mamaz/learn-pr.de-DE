### <a name="train-a-tensorflow-model"></a>Trainieren eines TensorFlow-Modells

In dieser Einheit trainieren Sie ein mit [TensorFlow](https://www.tensorflow.org/) erstelltes Bildklassifizierungsmodell zur Erkennung von Bildern, die Hotdogs enthalten. Statt ein Modell von Grund auf neu zu erstellen, was eine enorm große Rechenleistung und Unmengen von Bildern erfordern würde, passen Sie ein bereits vorhandenes Modell an. Dies ist ein Verfahren, das als [Transfer Learning](https://en.wikipedia.org/wiki/Transfer_learning) bezeichnet wird. Mit Transfer Learning erreichen Sie eine hohe Genauigkeit mit nur wenigen Minuten Trainingszeit auf einem typischen Laptop oder PC und nur einigen Dutzend Bildern.

Im Zusammenhang mit Deep Learning wird beim Transfer Learning mit einem tiefgreifenden neuronalen Netzwerk begonnen, das vorab trainiert wurde, Bilder zu erkennen. Diesem wird eine Ebene hinzugefügt, mit der das Netzwerk an Ihren Problembereich angepasst wird, beispielsweise Bilder in zwei Gruppen zu teilen, nämlich in Bilder mit Hotdogs und Bilder ohne Hotdogs. Unter <https://github.com/tensorflow/models/tree/master/research/slim#pre-trained-models.> sind mehr als 20 vorab trainierte TensorFlow-Bildklassifizierungsmodelle verfügbar. Die Modelle [Inception](https://arxiv.org/abs/1512.00567) und [ResNet](https://towardsdatascience.com/an-overview-of-resnet-and-its-variants-5281e2f56035) zeichnen sich durch eine höhere Genauigkeit und einen entsprechend höheren Ressourcenbedarf aus, während bei MobileNet-Modellen Genauigkeit gegen Kompaktheit und Energieeffizienz eingetauscht wird und diese Modelle für mobile Geräte entwickelt wurden. Alle diese Modelle sind in der Deep-Learning-Community bekannt und wurden in einer Reihe von Wettbewerben sowie in realen Anwendungen eingesetzt. Verwenden Sie eines der MobileNet-Modelle als Grundlage für Ihr neuronales Netzwerk, um ein vernünftiges Verhältnis zwischen Genauigkeit und Trainingszeit zu finden.

Zum Training des Modells gehört etwas mehr als nur die Ausführung eines Python-Skripts, welches das Basismodell herunterlädt und eine Ebene hinzufügt, die mit domänenspezifischen Bildern und Bezeichnungen trainiert wurde. Das Skript, das Sie benötigen, erhalten Sie unter GitHub, und die Bilder, die Sie verwenden, wurden aus Tausenden von öffentlich zugänglichen Bildern von Lebensmitteln zusammengestellt, die unter [Kaggle](https://www.kaggle.com) verfügbar sind.

1. Klicken Sie auf der Data Science Virtual Machine auf das Symbol „Terminal“ am unteren Bildschirmrand, um ein Terminalfenster zu öffnen.

    ![Aufrufen eines Terminalfensters](../media-draft/3-launch-terminal.png)

    _Aufrufen eines Terminalfensters_

1. Führen Sie im Terminalfenster den folgenden Befehl aus, um zum Ordner „notebooks“ zu navigieren:

    ```bash
    cd notebooks
    ```
    Dieser Ordner enthält bereits Jupyter-Beispielnotebooks, die für DSVM zusammengestellt wurden.

1. Verwenden Sie als Nächstes den folgenden Befehl, um das Repository „TensorFlow for Poets“ aus GitHub zu klonen:

    ```bash
    git clone https://github.com/googlecodelabs/tensorflow-for-poets-2
    ```
    > **Tipp**: Sie können diese Zeile in die Zwischenablage kopieren und anschließend mit der Tastenkombination **UMSCHALTTASTE+Einfg** in das Terminalfenster einfügen.

    Dieses Repository enthält Skripts zum Erstellen von Transfer-Learning-Modellen, zum Aufrufen eines trainierten Modells, um ein Bild zu klassifizieren, und vieles mehr. Es ist Teil von [Google Codelabs](https://codelabs.developers.google.com/), eine Plattform, die eine Vielzahl von Ressourcen und praktischen Übungen für Softwareentwickler enthält, die TensorFlow und andere Google-Tools und APIs kennenlernen möchten.

1. Nachdem der Klonvorgang abgeschlossen ist, navigieren Sie zu dem Ordner, der das geklonte Modell enthält:

    ```bash
    cd tensorflow-for-poets-2
    ```

1. Verwenden Sie den folgenden Befehl, um Bilder herunterzuladen, die zum Trainieren des Modells verwendet werden:

    ```bash
    wget https://topcs.blob.core.windows.net/public/tensorflow-resources.zip -O temp.zip; unzip temp.zip -d tf_files; rm temp.zip
    ```

    Mit diesem Befehl wird eine ZIP-Datei, die Hunderte von Bildern von Lebensmitteln enthält – die Hälfte davon mit Hotdogs, die andere Hälfte ohne – heruntergeladen und in das Unterverzeichnis „tf_files“ kopiert.

1. Klicken Sie auf das Symbol „Datei-Manager“ am unteren Bildschirmrand, um das Fenster „Datei-Manager“ zu öffnen.

    ![Aufrufen von Datei-Manager](../media-draft/3-launch-file-manager.png)

    _Aufrufen von Datei-Manager_

1. Navigieren Sie im Datei-Manager zum Ordner „notebooks/tensorflow-for-poets-2/tf_files“. Überprüfen Sie, ob der Ordner die Unterverzeichnisse „hot_dog“ und „not_hot_dog“ enthält. Ersteres enthält mehrere Hundert Bilder mit Hotdogs, während das Letztere dieselbe Anzahl von Bildern **ohne** Hotdogs enthält. Durchsuchen Sie die Bilder im Ordner „hot_dog“, um ein Gefühl dafür zu bekommen, wie die Bilder aussehen. Sehen Sie sich auch die Bilder im Ordner „not_hot_dog“ an.

    > Um ein neuronales Netzwerk so zu trainieren, dass es ermitteln kann, ob ein Bild einen Hotdog enthält, trainieren Sie es mit Bildern, die einen Hotdog enthalten, sowie mit Bildern, die keinen Hotdog enthalten.

    ![Bilder im Ordner „Hot_dog“](../media-draft/3-hot-dog-images.png)

    *Bilder im Ordner „Hot_dog“*

    Überprüfen Sie außerdem, ob der Ordner eine Textdatei mit dem Namen **retrained_labels_hotdog.txt** enthält. In dieser Datei sind die Unterverzeichnisse angegeben, in denen die Trainingsbilder enthalten sind. Sie wird von dem Python-Skript verwendet, mit dem das Modell trainiert wird. Vom Skript werden die Dateien in den jeweiligen in der Textdatei angegebenen Unterverzeichnissen einzeln benannt und zum Trainieren des Netzwerks verwendet (der Name der Textdatei ist ein Parameter, der an das Skript übergeben wird).

1. Öffnen Sie ein zweites Terminalfenster, und navigieren Sie zum Ordner „notebooks/tensorflow-for-poets-2“. Das ist derselbe Ordner, der bereits im ersten Terminalfenster geöffnet ist. Verwenden Sie anschließend den folgenden Befehl, um [TensorBoard](https://www.tensorflow.org/programmers_guide/summaries_and_tensorboard) aufzurufen – hierbei handelt es sich um eine Reihe von Tools, mit denen Sie TensorFlow-Modelle visualisieren und sich einen Überblick über den Transfer-Learning-Prozess verschaffen können:

     ```bash
     tensorboard --logdir tf_files/training_summaries
     ```

     > Dieser Befehl kann nicht ausgeführt werden, wenn bereits eine Instanz von TensorBoard ausgeführt wird. Wenn Sie benachrichtigt werden, dass Port 6006 bereits verwendet wird, verwenden Sie einen ```pkill -f "tensorboard"```-Befehl, um den vorhandenen Prozess zu beenden. Führen Sie anschließend den Befehl ```tensorboard``` erneut aus.

1. Wechseln Sie zurück zum ursprünglichen Terminalfenster, und führen Sie die folgenden Befehle aus:

    ```bash
    IMAGE_SIZE=224;
    ARCHITECTURE="mobilenet_0.50_${IMAGE_SIZE}";
    ```

    Mit diesen Befehlen werden Umgebungsvariablen initialisiert, die die Auflösung der Trainingsbilder und das Basismodell angeben, auf dem das neuronale Netzwerk aufgebaut ist. Gültige Werte für IMAGE_SIZE: 128, 160, 192 und 224. Höhere Werte verlängern die Trainingszeit, aber auch die Genauigkeit der Klassifizierung.

1. Führen Sie als Nächstes den folgenden Befehl aus, um den Transfer-Learning-Prozess zu starten, d.h. um das Modell mit den heruntergeladenen Bildern zu trainieren:

    ```bash
    python scripts/retrain.py \
    --bottleneck_dir=tf_files/bottlenecks \
    --how_many_training_steps=500 \
    --model_dir=tf_files/models/ \
    --summaries_dir=tf_files/training_summaries/"${ARCHITECTURE}" \
    --output_graph=tf_files/retrained_graph_hotdog.pb \
    --output_labels=tf_files/retrained_labels_hotdog.txt \
    --architecture="${ARCHITECTURE}" \
    --image_dir=tf_files \
    --testing_percentage=15 \
    --validation_percentage=15
    ```

    **retrain.py** ist eines der Skripts im Repository, das Sie heruntergeladen haben. Es ist ein komplexes Skript und umfasst mehr als 1.000 Codezeilen und Kommentare. Seine Aufgabe besteht darin, das mit dem Schalter ```--architecture``` angegebene Modell herunterzuladen und einer neuen Ebene hinzuzufügen, die mit den Bildern in Unterverzeichnissen des mit dem Schalter ```--image_dir``` angegebenen Verzeichnisses trainiert wurde. Jedes Bild ist mit dem Namen des Unterverzeichnisses beschriftet, in dem es sich befindet – in diesem Beispiel entweder mit „hot_dog“ oder mit „not_hot_dog“ – sodass das geänderte neuronale Netzwerk eingegebene Bilder als Bilder mit Hotdogs („hot_dog“) oder als Bilder ohne Hotdogs („not_hot_dog“) klassifizieren kann. Die Ausgabe der Trainingssitzung ist eine TensorFlow-Modelldatei mit dem Namen **retrained_graph_hotdog.pb**. Der Name und der Speicherort werden im Schalter ```--output_graph``` angegeben.

1. Warten Sie, bis das Training abgeschlossen ist. Das sollte keine fünf Minuten dauern. Überprüfen Sie dann die Ausgabe, um die Genauigkeit des Modells zu ermitteln. Ihr Ergebnis kann sich geringfügig vom folgenden unterscheiden, da zum Trainingsprozess ein gewisses Maß an zufälligen Schätzungen gehört.

      ![Beurteilen der Modellgenauigkeit](../media-draft/3-running-transfer-learning.png)

1. Klicken Sie auf das Browsersymbol am unteren Bildschirmrand, um den in Data Science Virtual Machine installierten Browser zu öffnen. Navigieren Sie zu <http://0.0.0.0:6006>, um eine Verbindung mit TensorBoard herzustellen.

    ![Aufrufen von Firefox](../media-draft/3-launch-firefox.png)

1. Überprüfen Sie das Diagramm mit der Bezeichnung „accuracy_1“. Die blaue Linie zeigt die Genauigkeit an, die im Laufe der Ausführung der mit dem Schalter ```how_many_training_steps``` angegebenen 500 Trainingsschritte erzielt wurde. Diese Metrik ist wichtig, weil sie zeigt, wie sich die Genauigkeit des Modells im Verlauf des Trainings entwickelt. Gleichermaßen wichtig ist der Abstand zwischen der blauen und der orangefarbenen Linie, der das Maß der aufgetretenen Überanpassung beziffert, die immer möglichst gering gehalten werden sollte. [Überanpassung](https://en.wikipedia.org/wiki/Overfitting) bedeutet, dass das Modell zwar die Bilder, mit denen es trainiert wurde, gut klassifizieren kann, bei der Klassifizierung von anderen Bildern jedoch Schwächen zeigt. Die Ergebnisse hier sind akzeptabel, da der Abstand zwischen der orangefarbenen Linie (für die mit den Trainingsbildern erzielte „Trainingsgenauigkeit“) und der blauen Linie (für die beim Testen mit anderen als den Trainingsbildern erzielte „Validierungsgenauigkeit“) weniger als 10 % beträgt.

    ![Anzeige der TensorBoard-Skalare](../media-draft/3-tensorboard-scalars.png)

1. Klicken Sie im TensorBoard-Menü auf **GRAPHS**, und überprüfen Sie die dort angezeigten Diagramme. Dieses Diagramms hat in erster Linie die Aufgabe, das neuronale Netzwerk und die Ebenen darzustellen, aus denen das Netzwerk besteht. In diesem Beispiel ist „input_1“ die Ebene, die mit Bildern von Lebensmitteln trainiert und dem Netzwerk hinzugefügt wurde. „MobilenetV1“ ist das neuronale Basisnetzwerk, mit dem Sie begonnen haben. Es enthält zahlreiche Ebenen, die nicht angezeigt werden. Wenn Sie ein neuronales Deep-Netzwerk von Grund auf neu erstellt hätten, würden hier alle Ebenen angezeigt werden. (Wenn Sie die Ebenen anzeigen möchten, aus denen das Netzwerk „MobileNet“ besteht, doppelklicken Sie im Diagramm auf den Block „MobilenetV1“.) Weitere Informationen zur Anzeige von Diagrammen sowie zu den dort angezeigten Informationen finden Sie unter [TensorBoard: Graph Visualization](https://www.tensorflow.org/programmers_guide/graph_viz).

    ![Anzeige der TensorBoard-Diagramme](../media-draft/3-tensorboard-graphs.png)

1. Wechseln Sie zurück zum Datei-Manager, und navigieren Sie zum Ordner „notebooks/tensorflow-for-poets-2/tf_files“. Überprüfen Sie, ob er eine Datei mit dem Namen **retrained_graph_hotdog.pb** enthält. *Diese Datei wurde während des Trainingsprozesses erstellt und enthält das trainierte TensorFlow-Modell*. Sie verwenden es in der nächsten Übung, um das Modell aus der NotHotDog-App aufzurufen.

Das Skript, das Sie in Schritt 10 ausgeführt haben, gibt 500 Trainingsschritte an, wodurch ein vernünftiges Verhältnis zwischen Genauigkeit und Trainingszeit gefunden wird. Wenn Sie möchten, trainieren Sie das Modell erneut mit einem höheren ```how_many_training_steps```-Wert wie etwa 1000 oder 2000. Eine höhere Schrittzahl führt in der Regel zu einer höheren Genauigkeit, jedoch auf Kosten einer längeren Trainingszeit. Achten Sie auf eine Überanpassung. Diese wird, wie Sie sich erinnern, durch den Abstand zwischen der orangefarbenen und der blauen Linie in der Anzeige der TensorBoards-Skalare dargestellt.