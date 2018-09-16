In dieser Einheit installieren Sie Eclipse und das Azure-Toolkit auf Ihrem lokalen Computer. Die Installation erfolgt schnell und einfach. Am Ende der Übung verfügen Sie über alles, was Sie benötigen, um Ihre erste Java-Anwendung in Azure zu erstellen.

## <a name="install-eclipse-ide"></a>Installieren der Eclipse-IDE

1. Laden Sie die Eclipse-Version von http://www.eclipse.org/downloads/packages/installer herunter, die Ihrem Betriebssystem entspricht.

1. Starten Sie den Eclipse-Installer nach dem Download.

    1. Doppelklicken Sie unter Windows auf die heruntergeladene Datei.

    1. Entpacken Sie den Installer unter macOS und Linux aus der heruntergeladenen Datei, und führen Sie ihn aus.

        > [!NOTE]
        > Wenn das Java Development Kit nicht vorhanden ist, fordert der Installer Sie möglicherweise dazu auf, dieses zu installieren.

1. Wählen Sie die Pakete aus, die installiert werden sollen. Wenn Sie Java-Entwickler sind, wählen Sie die Eclipse-IDE für Java oder Java EE aus.

1. Wählen Sie das Installationsziel auf Ihrem Computer aus.

1. Starten Sie Eclipse, um zu überprüfen, dass das Programm ordnungsgemäß installiert wurde.

## <a name="install-azure-toolkit-for-eclipse"></a>Installieren des Azure-Toolkits für Eclipse

Die Installation des Azure-Toolkits verläuft unter Windows, macOS und Linux gleich.

1. Starten Sie Eclipse.

1. Navigieren Sie zu **Help** > **Install New Software...** (Hilfe > Neue Software installieren...).

    Der folgende Screenshot zeigt die Position von **Install New Software...** (Neue Software installieren...) im Menü an.

    ![Screenshot der Option „Install New Software“ (Neue Software installieren), die im Hilfemenü von Eclipse hervorgehoben ist.](../media/7-eclipse-install-new-software.png)

1. Das Dialogfeld **Available Software** (Verfügbare Software) wird geöffnet. Geben Sie `http://dl.microsoft.com/eclipse/` in das Textfeld **Work with:** (Arbeiten mit:) ein, und drücken Sie die EINGABETASTE.

1. Überprüfen Sie die Option **Azure Toolkit for Java** (Azure-Toolkit für Java) in den Ergebnissen. Stellen Sie sicher, dass Sie die Option **Contact all update sites during install to find required software** (Während der Installation alle Updatesites kontaktieren, um erforderliche Software zu suchen) deaktivieren, sofern dies noch nicht der Fall ist.

    Im folgenden Screenshot wird die oben beschriebene Installationskonfiguration von **Available Software** (Verfügbare Software) dargestellt.

    ![Screenshot des Fensters „Available Software“ (Verfügbare Software) in Eclipse mit Feldern, die die Konfigurationen hervorheben, die zum Suchen und Installieren des Azure-Toolkits für Java erforderlich sind.](../media/7-eclipse-download-azure-toolkit-for-java.png)

1. Klicken Sie auf **Weiter**.

1. Lesen und akzeptieren Sie die Lizenzbedingungen, wenn Sie dazu aufgefordert werden, und klicken Sie auf **Finish** (Fertig stellen).

1. Eclipse lädt das Azure-Toolkit herunter und installiert es.

1. Starten Sie Eclipse neu (falls erforderlich).

1. Überprüfen Sie die Installation des Azure-Toolkits, indem Sie sicherstellen, dass die Menüoption **Tools** > **Azure** in Eclipse vorhanden ist.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie Eclipse installiert und die Integration mit Azure-Diensten und -Produkten vorbereitet.