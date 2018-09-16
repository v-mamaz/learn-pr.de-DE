In dieser Einheit installieren Sie Visual Studio auf Ihrem Windows- oder macOS-Computer. Unter Windows muss die Workload „Azure-Entwicklung“ installiert werden. Mit Visual Studio für Mac können Sie durch den integrierten Workflow „Verbundene Dienste“ Apps für Azure App Service erstellen. Am Ende der Einheit können Sie mit dem Erstellen von Anwendungen und deren Veröffentlichung in Azure beginnen.

## <a name="exercise-steps"></a>Schritte

Bei der Installation von Visual Studio unter Windows und macOS gibt es geringfügige Unterschiede. Diese werden in den folgenden Abschnitten behandelt.

### <a name="windows"></a>Windows

1. Laden Sie den Visual Studio-Installer von https://visualstudio.microsoft.com/downloads/ herunter.

1. Führen Sie den Installer aus. Dadurch wird das Fenster „Workloads“ geöffnet.

1. Wählen Sie die Workload **Azure-Entwicklung** aus.

    Der folgende Screenshot stellt den Visual Studio-Installer mit der ausgewählten Workload dar, durch die die Azure-Entwicklung in Visual Studio ermöglicht wird.

    ![Screenshot des Visual Studio-Installers mit der hervorgehobenen Workload „Azure-Entwicklung“](../media/5-select-azure-workload.png)

1. (Optional) Installieren Sie die Workload „ASP.NET und Webentwicklung“, damit Sie Webanwendungen für Azure erstellen können.

1. Klicken Sie auf **Installieren**, und warten Sie, bis Visual Studio installiert ist.

1. Öffnen Sie Visual Studio nach der Installation.

1. Navigieren Sie zum Menü „Ansicht“ in Visual Studio, und stellen Sie sicher, dass die Option **Cloud-Explorer** vorhanden ist.

    Auf dem folgenden Screenshot wird die Menüoption „Cloud-Explorer“ dargestellt, die vorhanden ist, wenn die Workload „Azure-Entwicklung“ installiert ist.

    ![Screenshot des Visual Studio-Menüs „Ansicht“ mit der hervorgehobenen Menüoption „Cloud-Explorer“](../media/5-verify-cloud-explorer.png)

### <a name="macos"></a>macOS

1. Navigieren Sie zu https://visualstudio.microsoft.com/, und laden Sie den Installer für Visual Studio für Mac herunter.

1. Klicken Sie auf die Datei „VisualStudioInstaller.dmg“, um den Installer einzubinden, und führen Sie diesen anschließend aus, indem Sie auf das Logo doppelklicken.

1. Stimmen Sie den Datenschutzbestimmungen und Lizenzbedingungen zu, wenn diese angezeigt werden.

1. Wählen Sie im Installer die Komponenten aus, die installiert werden sollen. Azure-Komponenten sind in Visual Studio für Mac bereits enthalten, es wird jedoch empfohlen, die Plattform **.NET Core** zu installieren, um Webinhalte für Azure entwickeln zu können.

    Der folgende Screenshot zeigt die .NET Core-Plattform an, die zum Hinzufügen von Azure-Entwicklungsfunktionen zu Visual Studio für Mac erforderlich ist.

    ![Screenshot des Visual Studio für Mac-Installers mit der hervorgehoben Option für die Plattform „.NET Core“](../media/5-vsmac-install-net-core.png)

1. Klicken Sie auf **Installieren und aktualisieren**, sobald Sie mit der Auswahl zufrieden sind, und warten Sie, bis die Installation abgeschlossen ist.

1. Wenn Sie dazu aufgefordert werden, die Berechtigungen zu erhöhen, verwenden Sie Ihre Administratoranmeldeinformationen.

1. Starten Sie Visual Studio für Mac nach der Installation.
