Da Ihre Data Science Virtual Machine jetzt betriebsbereit ist und ausgeführt wird, entscheiden Sie sich, Ihr erstes Deep Learning-Modell zu trainieren. Sie möchten Ihre Experimente isoliert von allen anderen Prozessen auf Ihrem Server ausführen. Zu diesem Zweck führen Sie sie in einem Docker-Container aus.

## <a name="connect-to-the-vm-with-ssh"></a>Herstellen einer Verbindung mit dem virtuellen Computer mit ssh

Stellen Sie sicher, dass Sie noch immer mit Ihrem virtuellen Computer über ssh verbunden sind. Wenn dies nicht der Fall ist, führen Sie diesen Befehl einfach erneut aus, um die Remoteverbindung mit dem virtuellen Computer wiederherzustellen.

1. Führen Sie in Azure Cloud Shell den folgenden Befehl aus, um sich beim virtuellen Computer anzumelden.

    ```azurecli 
    ssh <USERNAME>@<IP>
    ``` 
    
    Ersetzen Sie `<USERNAME>` durch den Administratorkontonamen, den Sie beim Erstellen des virtuellen Computers definiert haben. Ersetzen Sie `<IP>` durch die IP-Adresse des virtuellen Computers, die Sie in der vorherigen Übung gespeichert haben.  

1. Wenn Sie dazu aufgefordert werden, geben Sie Ihr Kennwort für das Administratorkonto ein, um den Anmeldevorgang abzuschließen.

## <a name="run-a-jupyter-notebook-server-in-a-docker-container-in-the-vm"></a>Ausführen eines Jupyter Notebook-Servers in einem Docker-Container auf dem virtuellen Computer

> [!NOTE]
> Da wir nur über ein Administrator- oder Stammkonto auf dem virtuellen Computer verfügen, müssen wir alle Docker-Befehle als root mit `sudo` ausführen.

1. Um zu ermitteln, welche Docker-Container auf dem virtuellen Computer vorhanden sind, führen Sie den folgenden Befehl an der Eingabeaufforderung aus.

    ```azurecli 
    sudo docker ps
    ```

1. Führen Sie den folgenden Befehl an der Eingabeaufforderung aus, um einen neuen Container für unsere Experimente zu erstellen.

    ```azurecli 
    sudo docker run --rm -it --entrypoint '/bin/sh' -p 8888:8888 pytorch/pytorch -c \
    'conda install jupyter matplotlib -y &&\
    curl https://pytorch.org/tutorials/_downloads/cifar10_tutorial.ipynb > first_pytorch_classifier.ipynb &&\
    jupyter notebook --ip=0.0.0.0 --no-browser --allow-root'
    ``` 

    Die Ausführung dieses Befehls dauert eine ganze Weile. Während wir also etwas Zeit haben, können wir erörtern, was der Befehl bewirkt. 
    - `docker run` führt einen Befehl in einem neuen Container aus. Das Docker-Image, das verwendet wird, ist pytorch/pytorch. Es erstellt zunächst eine schreibbare Containerschicht über dem angegebenen Image und startet sie dann mit dem angegebenen Befehl.
    - `--rm` entfernt den Container, sobald dieser vorhanden ist. Wenn Sie den Container beibehalten möchten, löschen Sie dieses Argument. 
    - `--entrypoint 'bin/sh'` überschreibt den Standardeinstiegspunkt des Images durch die Angabe der Bash-Shell.
    - `-c` definiert, welcher Befehl ausgeführt werden soll, wenn der Container gestartet wird. In diesem Fall werden drei Befehle ausgeführt:
        - Installiert Jupyter und matplotlib.
        - Kopiert ein Notebook („cifar10_tutorial.ipynb“) aus pytorch.org in eine Datei im Container namens `first_pytorch_classifier.ipynb`.
        - Startet den Notebook-Server im Container auf die gleiche Weise wie in der vorherigen Übung.  Es wird kein Browser gestartet, auf das Notebook kann über root zugegriffen werden, und es wird an allen Ports gelauscht. 
    
    Der Notebook-Server lauscht an allen Ports für den betreffenden Container. Aber wie erfolgt Datenverkehr von außerhalb des Containers? Das `-p 8888:8888`-Argument bindet Port `8888` des Containers an TCP-Port 8888 auf dem Hostcomputer. Daher wird Datenverkehr, der vom virtuellen Computer stammt, über Port 8888 vom Container aufgenommen. 

## <a name="connect-to-the-jupyter-notebook-server-from-a-remote-browser"></a>Herstellen einer Verbindung mit dem Jupyter Notebook-Server über einen Remotebrowser 

Sobald das Jupyter Notebook im Container ausgeführt wird, wird eine Meldung ähnlich der folgenden angezeigt. 

> *Kopieren Sie bei der ersten Verbindungsherstellung die folgende URL, und fügen Sie sie in Ihren Browser ein, um sich mit einem Token anzumelden: http://(5b8783e7911d oder 127.0.0.1):8888/?token={Token}*

1. Ersetzen Sie den Teil **http://(5b8783e7911d oder 127.0.0.1)** der URL durch `<HOSTNAME>.<REGION>.cloudapp.azure.com` oder die IP-Adresse des virtuellen Computers, und navigieren Sie auf einer neuen Registerkarte in Ihrem Browser zu der Adresse.

    ![Screenshot des Jupyter Notebook-Dashboards ](../media/notebook-in-docker.png)
    
    Dieses Mal wird nur ein einzelnes Notebook angezeigt. Das liegt daran, dass wir uns in einem Container befinden und nur dieses Notebook kopiert haben. In der nächsten Übung experimentieren wir mit diesem Notebook. 
    
    > [!TIP]
    > Fahren Sie den Notebook-Server also noch nicht herunter. Wir untersuchen das Notebook `first_pytorch_classifier.ipynb` in der nächsten Übung.