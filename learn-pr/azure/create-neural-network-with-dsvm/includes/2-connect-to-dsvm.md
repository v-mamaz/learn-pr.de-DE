### <a name="exercise-2-connect-to-the-data-science-vm"></a>Übung 2: Herstellen einer Verbindung mit der Data Science Virtual Machine

In dieser Übung stellen Sie per Remotezugriff eine Verbindung mit dem Ubuntu-Desktop auf dem virtuellen Computer her, den Sie in der vorherigen Übung erstellt haben. Zu diesem Zweck benötigen Sie einen Client, der [Xfce](https://xfce.org/) unterstützt, eine einfache Desktopumgebung für Linux. Hintergrundinformationen und eine Übersicht über die verschiedenen Möglichkeiten, eine Verbindung mit einer DSVM herzustellen, finden Sie unter [Zugreifen auf die Data Science Virtual Machine für Linux](https://docs.microsoft.com/en-us/azure/machine-learning/data-science-virtual-machine/dsvm-ubuntu-intro#how-to-access-the-data-science-virtual-machine-for-linux).

1. Wenn Sie nicht bereits einen Xfce-Client installiert haben, laden Sie den [X2Go-Client](https://wiki.x2go.org/doku.php/download:start) herunter, und installieren Sie ihn, bevor Sie mit dieser Übung fortfahren. X2Go ist eine kostenlose Open-Source-Xfce-Lösung, die mit einer Vielzahl von Betriebssystemen einschließlich Windows und OS X funktioniert. Die Anweisungen in dieser Übung setzen voraus, dass Sie X2Go verwenden, jedoch können Sie jeden Client verwenden, der Xfce unterstützt.

1. Kehren Sie zur Ressourcengruppe „data-science-rg“ im Azure-Portal zurück. Klicken Sie auf die Ressource „data-science-vm“, um sie im Portal zu öffnen.

    ![Öffnen der Data Science Virtual Machine](../images/open-data-science-vm.png)

    _Öffnen der Data Science Virtual Machine_

1. Setzen Sie den Mauszeiger auf die für den virtuellen Computer angezeigte IP-Adresse, und klicken Sie auf die Schaltfläche **Kopieren**, die zum Kopieren der IP-Adresse in die Zwischenablage angezeigt wird.

    ![Kopieren der IP-Adresse des virtuellen Computers](../images/copy-ip-address.png)

    _Kopieren der IP-Adresse des virtuellen Computers_

1. Starten Sie den X2Go-Client, und stellen Sie mithilfe der IP-Adresse in der Zwischenablage und dem Benutzernamen, den Sie in der vorherigen Übung angegeben haben, eine Verbindung mit der Data Science Virtual Machine her. Stellen Sie die Verbindung über Port **22** (für SSH-Verbindungen verwendeter Standardport) her, und geben Sie **XFCE** als Sitzungstyp ein. Klicken Sie auf die Schaltfläche **OK**, um Ihre Einstellungen zu bestätigen.

    ![Herstellen einer Verbindung mit X2Go](../images/new-session-1.png)

    _Herstellen einer Verbindung mit X2Go_

1. Wählen Sie im Bereich „Neue Sitzung“ auf der rechten Seite die Auflösung aus, die Sie für den Remotedesktop verwenden möchten. Klicken Sie dann am Anfang des Bereichs auf **Neue Sitzung**.

    ![Starten einer neuen Sitzung](../images/new-session-2.png)

    _Starten einer neuen Sitzung_

1. Geben Sie das Kennwort ein, das Sie in [Übung 1](#Exercise1) angegeben haben, und klicken Sie dann auf die Schaltfläche **OK**. Wenn Sie gefragt werden, ob Sie dem Hostschlüssel vertrauen, antworten Sie mit **Ja**. Ignorieren Sie auch alle Fehlermeldungen, die besagen, dass der SSH-Daemon nicht gestartet werden konnte.

    ![Anmelden beim virtuellen Computer](../images/new-session-3.png)

    _Anmelden beim virtuellen Computer_

1. Warten Sie, bis der Remotedesktop angezeigt wird, und vergewissern Sie sich, dass er dem folgenden ähnelt.

    > Wenn Text und Symbole auf dem Desktop zu groß sind, beenden Sie die Sitzung. Klicken Sie auf das Symbol in der unteren rechten Ecke des Bereichs „Neue Sitzung“, und wählen Sie **Sitzungseinstellungen...**  im Menü aus. Wechseln Sie im Dialogfeld „Neue Sitzung“ zur Registerkarte „Eingabe/Ausgabe“, passen Sie die Anzeige-DPI an, und starten Sie dann eine neue Sitzung. Starten Sie mit 96 DPI-Wert, und passen Sie den Wert nach Bedarf an.

    ![Verbunden!](../images/ubuntu-desktop.png)

    _Verbunden!_

Da Sie nun verbunden sind, nehmen Sie sich einen Moment Zeit, um die Verknüpfungen auf dem Desktop zu untersuchen. Hierbei handelt es sich um Verknüpfungen zu den zahlreichen Data Science-Tools, die auf dem virtuellen Computer vorinstalliert sind, darunter u.a. [Jupyter](http://jupyter.org/), [R Studio](https://www.rstudio.com/) und der [Microsoft Azure Storage-Explorer](https://azure.microsoft.com/en-us/features/storage-explorer/).