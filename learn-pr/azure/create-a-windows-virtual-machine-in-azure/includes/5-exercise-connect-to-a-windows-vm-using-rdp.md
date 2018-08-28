In dieser Übung verwenden Sie den RDP-Client, um eine Verbindung mit der Windows-VM herzustellen, die Sie in der vorherigen Übungseinheit erstellt haben. Sie können die Verbindung herstellen, indem Sie eine RDP-Datei über das Azure-Portal ausführen. Diese RDP-Datei enthält Folgendes:

* Die öffentliche IP-Adresse der VM.
* Die Portnummer.

## <a name="motivation"></a>Motivation

Für dieses Übungsszenario können Sie sich vorstellen, dass Sie ein Student sind, der lernen möchte, wie man einem Windows Server-Computer Rollen und Features hinzufügt. Ihr Netzwerkadministrator möchte jedoch nicht, dass Sie dies an einem physischen Computer im Netzwerk ausprobieren, und die Computer der Schule sind nicht gut genug ausgestattet, um Windows Hyper-V auszuführen. Azure bietet die ideale Lösung.

## <a name="configure-network-and-public-ip-address-settings"></a>Konfigurieren der Einstellungen des Netzwerks und der öffentlichen IP-Adresse

1. Stellen Sie sicher, dass das Blatt für die zuvor erstellte VM im Azure-Portal geöffnet ist. Wenn Sie das Blatt öffnen müssen, finden Sie dieses unter **Alle Ressourcen**.

1. Navigieren Sie zum Abschnitt **Netzwerk**. Ganz oben in diesem Abschnitt finden Sie Links zum virtuellen Subnetz und zur dynamischen IP-Adresse, die zusammen mit der VM erstellt wurden, da die Standardwerte verwendet wurden. Wenn Sie die Ressourcen ändern möchten (z.B. zu einer statischen IP-Adresse wechseln), können Sie diese Links verwenden.

1. Klicken Sie auf **Regel für eingehenden Port hinzufügen**.

1. Klicken Sie am oberen Rand des Dialogfelds **Regel für eingehenden Port hinzufügen** auf **Basic**.

1. Wählen Sie unter **Dienst** **RDP** aus, und klicken Sie anschließend auf **Hinzufügen**.

## <a name="connect-to-the-vm-by-using-rdp"></a>Herstellen einer Verbindung mit der VM mit RDP

Führen Sie die folgenden Schritte aus, um die RDP-Datei herunterzuladen und eine Verbindung mit der VM herzustellen.

### <a name="download-the-rdp-file"></a>Herunterladen der RDP-Datei

1. Klicken Sie im Abschnitt **Übersicht** des Blatts der VM auf **Verbinden**.

1. Notieren Sie sich die Einstellungen für die **IP-Adresse** und die **Portnummer** auf dem Blatt **Verbindung mit virtuellem Computer herstellen**, und klicken Sie dann auf **RDP-Datei herunterladen**.

1. Klicken in Ihrem Browser auf **Öffnen** oder **Ausführen**, um die RDP-Datei zu öffnen.

### <a name="connect-to-the-windows-vm"></a>Herstellen einer Verbindung mit der Windows-VM

1. Notieren Sie sich die Sicherheitswarnung und die IP-Adresse des Remotecomputers, die im Dialogfeld **Remotedesktopverbindung** angezeigt werden, und klicken Sie dann auf **Verbinden**.

1. Geben Sie im Dialogfeld **Windows-Sicherheit** Ihren Benutzernamen und Ihr Kennwort ein, die Sie bereits in den Schritten 6 und 7 verwendet haben.

1. Notieren Sie sich die Zertifikatfehler im zweiten Dialogfeld **Remotedesktopverbindung**, und klicken Sie dann auf **Ja**.

   > [!Note]
   > Es dauert eine Weile, bis der Desktop des virtuellen Computers angezeigt wird. Der Grund hierfür ist, dass das B1-Image den Anforderungen nicht entspricht. Ihnen wird möglicherweise eine Meldung über unzureichenden Arbeitsspeicher angezeigt.

1. Klicken Sie im Dialogfeld **Netzwerke** auf **Nein**.

### <a name="resize-the-vm-in-the-azure-portal"></a>Ändern der Größe der VM im Azure-Portal

1. Wechseln Sie zurück zum Azure-Portal. Klicken Sie auf der Eigenschaftenseite der VM unter **Einstellungen** auf **Größe**.

1. Klicken Sie auf **D2s_v3** (2 vCPUs, 8-GB RAM), und klicken Sie dann auf **Auswählen**. Dann wird eine Meldung zur Größenänderung der VM angezeigt. Außerdem wird die VM im RDP-Fenster geschlossen.

1. Wechseln Sie zurück zum Azure-Portal. Klicken Sie im linken Bereich auf **Virtuelle Computer**.

1. Warten Sie darauf, dass unter **Virtuelle Computer** der Status **Wird ausgeführt** für Ihre VM angezeigt wird. Möglicherweise müssen Sie auf **Aktualisieren** klicken.

1. Klicken Sie auf den Namen der VM, und klicken Sie dann in den **Einstellungen** auf **Größe**. Stellen Sie sicher, dass die VM-Größe nun auf **D2s_v3** festgelegt ist.

### <a name="reconnect-to-the-resized-vm"></a>Wiederherstellen der Verbindung mit der VM mit der geänderten Größe

1. Klicken Sie auf **Virtuelle Computer**, und klicken Sie dann auf Ihre VM. Beachten Sie, dass sich der Wert für die **öffentliche IP-Adresse** vermutlich geändert hat. Klicken Sie auf **Verbinden**, und klicken Sie anschließend in Ihrem Browser auf **Ausführen** oder auf **Öffnen**.

1. Notieren Sie sich die Sicherheitswarnung und die IP-Adresse des Remotecomputers, die im Dialogfeld **Remotedesktopverbindung** angezeigt werden, und klicken Sie dann auf **Verbinden**.

1. Geben Sie im Dialogfeld **Windows-Sicherheit** Ihren Benutzernamen und Ihr Kennwort ein, die Sie bereits in den Schritten 6 und 7 verwendet haben.

1. Notieren Sie sich die Zertifikatfehler im zweiten Dialogfeld **Remotedesktopverbindung**, und klicken Sie dann auf **Ja**. Sie werden merken, dass die VM nun viel schneller auf den Anmeldevorgang reagiert.

1. Klicken Sie mit der rechten Maustaste auf die Taskleiste, und klicken Sie dann auf **Task-Manager starten**.

1. Klicken Sie im Fenster **Windows Task-Manager** auf **Weitere Details**.

1. Klicken Sie auf die Registerkarte **Leistung**. Beachten Sie, dass der gesamte verfügbare Arbeitsspeicher 8 GB beträgt, wovon etwa 1,2 GB genutzt werden. Schließen Sie den **Task-Manager**.

## <a name="summary"></a>Zusammenfassung

Sie haben über RDP eine Verbindung mit einer Windows-VM hergestellt. Über den Zugriff auf die Desktop-Benutzeroberfläche können Sie diese VM wie jeden anderen Windows-Computer verwalten.
