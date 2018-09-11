### <a name="exercise-1-create-an-ubuntu-data-science-vm"></a>Übung 1: Erstellen einer Data Science Virtual Machine für Ubuntu

Die Data Science Virtual Machine für Linux ist das Image eines virtuellen Computers, das Ihnen den Einstieg in Data Science erleichtert. Dabei sind zahlreiche Tools bereits erstellt, installiert und konfiguriert, damit Sie so schnell wie möglich beginnen können. Der NVIDIA-GPU-Treiber, [NVIDIA CUDA](https://developer.nvidia.com/cuda-downloads), und die [NVIDIA CUDA Deep Neural Network](https://developer.nvidia.com/cudnn)-Bibliothek (cuDNN) sind ebenso enthalten wie [Jupyter](http://jupyter.org/), einige Jupyter-Beispielnotebooks und [TensorFlow](https://www.tensorflow.org/). Alle vorinstallierten Frameworks sind sowohl GPU- als auch CPU-fähig. In dieser Übung erstellen Sie eine Instanz der Data Science Virtual Machine für Linux in Azure.

1. Öffnen Sie das [Azure-Portal](https://portal.azure.com) in Ihrem Browser. Wenn Sie gefragt werden, ob Sie sich anmelden möchten, melden Sie sich mit Ihrem Microsoft-Konto an.

1. Klicken Sie im Menü auf der linken Seite des Portals auf **+ Ressource erstellen**, und geben Sie dann „data science“ (ohne Anführungszeichen) in das Suchfeld ein. Wählen Sie **Data Science Virtual Machine for Linux (Ubuntu)** in der Ergebnisliste aus.

    ![Suchen einer Data Science Virtual Machine für Ubuntu](../images/new-data-science-vm.png)

    _Suchen einer Data Science Virtual Machine für Ubuntu_

1. Nehmen Sie sich die Zeit, um die Liste der Tools zu lesen, die der virtuelle Computer enthält. Klicken Sie dann unten auf dem Blatt auf **Erstellen**.

1. Füllen Sie das Blatt „Grundlagen“ wie unten dargestellt aus. Geben Sie ein mindestens 12 Zeichen langes Kennwort ein, das eine Mischung aus Großbuchstaben, Kleinbuchstaben, Zahlen und Sonderzeichen enthält. *Merken Sie sich unbedingt den Benutzernamen und das Kennwort, die Sie eingeben, da Sie sie im weiteren Verlauf der Aufgabe benötigen.*

    ![Eingeben grundlegender Informationen zur VM](../images/create-data-science-vm-1.png)

    _Eingeben grundlegender Einstellungen_

1. Wählen Sie auf dem Blatt „Größe auswählen“ die Option **DS1_V2 Standard** aus, die eine kostengünstige Möglichkeit zum Experimentieren mit Data Science Virtual Machine-Instanzen bereitstellt. Klicken Sie dann unten auf dem Blatt auf die Schaltfläche **Auswählen**.

    ![Auswählen einer VM-Größe](../images/create-data-science-vm-2.png)

    _Auswählen einer VM-Größe_

1. Aktivieren Sie auf dem Blatt „Einstellungen“ in der Liste der eingehenden Ports **SSH (22)**, damit Clients über das [Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell)-Protokoll (SSH) auf Port 22 eine Verbindung mit dem virtuellen Computer herstellen können. Klicken Sie dann auf **OK**.

    ![Erstellen des virtuellen Computers](../images/create-data-science-vm-3.png)

    _Erstellen des virtuellen Computers_

1. Überprüfen Sie auf dem Blatt „Erstellen“ die Optionen, die Sie für den virtuellen Computer ausgewählt haben, und klicken Sie auf **Erstellen**, um den Prozess der Erstellung des virtuellen Computers zu starten.

    ![Erstellen des virtuellen Computers](../images/create-data-science-vm-4.png)

    _Erstellen des virtuellen Computers_

1. Klicken Sie im Menü auf der linken Seite des Portals auf **Ressourcengruppen**. Klicken Sie dann auf die Ressourcengruppe „data-science-rg“.

    ![Öffnen der Ressourcengruppe](../images/open-resource-group.png)

    _Öffnen der Ressourcengruppe_

1. Warten Sie, bis „Wird bereitgestellt“ sich in „Erfolgreich“ ändert, um anzugeben, dass DSVM-Instanz und unterstützende Azure-Ressourcen erstellt wurden. Die Bereitstellung dauert in der Regel höchstens 5 Minuten. Klicken Sie zum Aktualisieren des Bereitstellungsstatus regelmäßig am oberen Rand des Blatts auf **Aktualisieren**.

    ![Überwachen des Bereitstellungsstatus](../images/deployment-succeeded.png)

    _Überwachen des Bereitstellungsstatus_

Sobald die Bereitstellung abgeschlossen ist, fahren Sie mit der nächsten Übung fort.