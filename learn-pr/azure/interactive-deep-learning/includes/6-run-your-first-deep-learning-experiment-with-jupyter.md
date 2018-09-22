![PyTorch-Logo](../media/5-image1.png) 

Im Normalfall implementieren Deep Learning-Entwickler Matrixalgebraoperationen nicht durchgängig manuell. Stattdessen verwenden sie Frameworks, etwa PyTorch oder TensorFlow.  

PyTorch ist ein Python-basiertes Framework, das Flexibilität als Entwicklungsplattform für Deep Learning bietet. PyTorch baut auf der wissenschaftlichen Computingbibliothek NumPy von Python auf. 

Sie fragen sich jetzt vielleicht, warum wir PyTorch zum Erstellen von Deep Learning-Modellen verwenden?  

- Einfach zu verwendende API: Wenn Sie Python kennen, können Sie schnell einsteigen.
- Python-Unterstützung: PyTorch integriert sich reibungslos in den wissenschaftlichen Computingstapel.
- Dynamische Computergraphen: Anstelle vordefinierter Graphen mit bestimmter Funktionalität erstellt PyTorch Computergraphen dynamisch, die zur Laufzeit verändert werden können. Dynamische Computergraphen sind für die geschachtelte Batchverarbeitung und in Fällen nützlich, in denen der Speicherplatzbedarf zum Erstellen eines bestimmten Netzwerks unbekannt ist.

Weitere Informationen zu PyTorch finden Sie in der [offiziellen Dokumentation von PyTorch.org](https://pytorch.org/about/).

## <a name="run-your-first-pytorch-model"></a>Ausführen Ihres ersten PyTorch-Modells

Da Sie nun einen Docker-Container aus einem PyTorch-Image bereitgestellt haben, ist es an der Zeit zu experimentieren. Wenn Sie sich erinnern, haben wir ein Notebook von [python.org](https://python.org) heruntergeladen. Dieses Beispiel-Notebook führt Sie schrittweise durch das Trainieren eines Netzwerks zum Klassifizieren von Bildern in verschiedene Kategorien. Es definiert ein Deep Convolutional Neural Network (CNN).

1. Navigieren Sie in Ihrem lokalen Browser zum Jupyter Notebook-Server, den Sie in der letzten Übung eingerichtet haben. Die URL weist das folgende Format auf:

    `<HOSTNAME>.<REGION>.cloudapp.azure.com:8888/?token={sometoken}`

1. Wählen Sie das Notebook `first_pytorch_classifier.ipynb` im Dashboard aus.

    ![Auswählen von „first_pytorch_classifier.ipynb“](../media/5-image2.PNG)

    Befolgen Sie die Anweisungen im Notebook, um Ihren ersten PyTorch-Klassifizierer zu trainieren.

    ![Screenshot des „Training eines Klassifizierers-Notebooks“](../media/5-image3.PNG)

2. Starten Sie an der obersten Position des Notebooks, und führen Sie jede Zelle in der entsprechenden Reihenfolge aus. Beachten Sie Folgendes:

    - Die Ausführung einiger Zellen dauert sehr lange. Beobachten Sie den kleinen Punkt oben rechts im Notebook neben der Angabe „Python 3“. Wenn der Kernel mit einem Vorgang ausgelastet ist, wird der Punkt zu einem ausgefüllten dunkleren Kreis. Dies bleibt so, bis der Vorgang abgeschlossen ist. 
    - Sie trainieren ein CNN, um Bilder zu klassifizieren. Nachdem das Netzwerk trainiert wurde, testet das Notebook beschriftete Bilder anhand des Modells. Es zeichnet die vorgenommene Vorhersage für jedes Bild auf und berechnet die Genauigkeit des Modells. Die Ergebnisse werden im folgenden Format angezeigt.

    ![Trainingsergebnisse, die die Genauigkeit des Modells anzeigen](../media/accuracy.png)
    
    - Mehr über das Notebook erfahren Sie in der [Dokumentation zu den PyTorch-Tutorials](https://pytorch.org/tutorials/beginner/blitz/cifar10_tutorial.html) online.
    
    - Gegen Ende des Notebooks behandeln die Notizen das Training für eine GPU. Wenn Sie die Übungen in diesem Modul ausgeführt haben, haben Sie einen CPU-basierten virtuellen Computer eingerichtet. Dies ist für ein Modell dieser Größe in Ordnung, und Sie sehen möglicherweise keine signifikanten Verbesserungen in der Trainingszeit mit einer GPU. Wenn Sie das Modul mit einem virtuellen Computer mit GPUs testen möchten, müssen Sie zwei Änderungen vornehmen:
    - Bereitstellen von DSVM für eine GPU-aktivierte VM-Größe der N-Serie.
    - Erstellen eines Containers mit `nvidia-docker` anstelle von `docker` in der vorherigen Übung.