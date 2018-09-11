In dieser Übung installieren Sie Eclipse auf Ihrem lokalen Computer. Anschließend installieren Sie das Azure-Toolkit, um die Entwicklung von Java-Anwendungen mit Azure-Integration vorzubereiten. Die Installation erfolgt schnell und einfach. Am Ende der Übung ist alles eingerichtet, was Sie für Ihre erste Java-Anwendung benötigen, für die Sie die Features und Dienste von Azure nutzen können.

## <a name="install-eclipse-ide"></a>Installieren der Eclipse-IDE

1. Laden Sie die Eclipse-Version von http://www.eclipse.org/downloads/packages/installer herunter, die Ihrem Betriebssystem entspricht.
2. Starten Sie den Eclipse-Installer nach dem Download.

    1. Doppelklicken Sie unter Windows auf die heruntergeladene Datei.
    2. Entpacken Sie den Installer unter macOS und Linux aus der heruntergeladenen Datei. Starten Sie den Installer anschließend.

        > [!NOTE]
        > Wenn das Java Development Kit nicht vorhanden ist, fordert der Installer Sie möglicherweise dazu auf, dieses zu installieren.

3. Wählen Sie die Pakete aus, die installiert werden sollen. Wenn Sie Java-Entwickler sind, wählen Sie die Eclipse-IDE für Java oder Java EE aus.
4. Wählen Sie das Installationsziel auf Ihrem Computer aus.
5. Starten Sie Eclipse, um zu überprüfen, dass das Programm ordnungsgemäß installiert wurde.

## <a name="install-azure-toolkit-for-eclipse"></a>Installieren des Azure-Toolkits für Eclipse

Die Installation des Azure-Toolkits verläuft unter Windows, macOS und Linux gleich.

1. Starten Sie Eclipse.
2. Navigieren Sie zu **Help** > **Install New Software...** (Hilfe > Neue Software installieren...).

    Der folgende Screenshot zeigt die Position von **Install New Software...** (Neue Software installieren...) im Menü an.

    ![Screenshot der Option „Install New Software“ (Neue Software installieren), die im Hilfemenü von Eclipse hervorgehoben ist.](../media/7-eclipse-install-new-software.png)

3. Das Dialogfeld **Available Software** (Verfügbare Software) wird geöffnet. Geben Sie `http://dl.microsoft.com/eclipse/` in das Textfeld **Work with:** (Arbeiten mit:) ein, und drücken Sie die EINGABETASTE.
4. Überprüfen Sie die Option **Azure Toolkit for Java** (Azure-Toolkit für Java) in den Ergebnissen. Stellen Sie sicher, dass Sie die Option **Contact all update sites during install to find required software** (Während der Installation alle Updatesites kontaktieren, um erforderliche Software zu suchen) deaktivieren, sofern dies noch nicht der Fall ist.

    Im folgenden Screenshot wird die oben beschriebene Installationskonfiguration von **Available Software** (Verfügbare Software) dargestellt.

    ![Screenshot des Fensters „Available Software“ (Verfügbare Software) in Eclipse mit Feldern, die die Konfigurationen hervorheben, die zum Suchen und Installieren des Azure-Toolkits für Java erforderlich sind.](../media/7-eclipse-download-azure-toolkit-for-java.png)

5. Klicken Sie auf **Weiter**.
6. Lesen und akzeptieren Sie die Lizenzbedingungen, wenn Sie dazu aufgefordert werden, und klicken Sie auf **Finish** (Fertig stellen).
7. Eclipse lädt das Azure-Toolkit herunter und installiert es.
8. Starten Sie Eclipse neu (falls erforderlich).
9. Überprüfen Sie die Installation des Azure-Toolkits, indem Sie sicherstellen, dass die Menüoption **Tools** > **Azure** in Eclipse vorhanden ist.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie Eclipse für Java installiert und die Integration mit Azure-Diensten und -Produkten vorbereitet. Die Installation erfolgt schnell und einfach, wodurch Eclipse für die Java-Entwicklung mit Integration in Clouddienste optimal geeignet ist.
