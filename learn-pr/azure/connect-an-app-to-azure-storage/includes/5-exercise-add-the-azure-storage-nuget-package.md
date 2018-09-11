In dieser Übung erfahren Sie, wie Sie die Azure Storage-Clientbibliothek in Ihre .NET Core-Konsolenanwendung integrieren.

## <a name="add-the-azure-storage-nuget-package"></a>Hinzufügen des NuGet-Pakets für Azure Storage

1. Klicken Sie erst mit der rechten Maustaste auf das Projekt und dann mit der linken auf **NuGet-Pakete verwalten...**.
  ![NuGet-Pakete verwalten]/' (..\media-draft\1-manage-nuget-packages.png)

1. Dann wird eine Seite angezeigt, auf der die zu diesem Zeitpunkt installierten NuGet-Pakete aufgeführt sind. Klicken Sie auf die Option **Durchsuchen**, und geben Sie **Storage** in das Suchfeld ein. Dann wird das **WindowsAzure.Storage**-Paket in den Suchergebnissen angezeigt.

1. Wählen Sie das Paket **WindowsAzure.Storage** aus. Auf der rechten Seite wird standardmäßig die neuste Version angezeigt (zum Zeitpunkt der Erstellung dieses Dokuments Version 9.3.0). Klicken Sie auf die Schaltfläche **Installieren**, um einen Verweis auf das Paket zu Ihrem Projekt hinzuzufügen.
  ![Paket finden](..\media-draft\3-find-package.png)

1. Visual Studio öffnet den Bereich **Ausgabe**, wenn Pakete wiederhergestellt werden. Abhängig von der Geschwindigkeit Ihrer Netzwerke dauert dies einige Sekunden. Es wird ein Dialogfenster mit einer **Vorschau der Änderungen** angezeigt, in dem angegeben wird, welche Pakete zur Ihrem Projekt hinzugefügt werden. Klicken Sie auf **OK**.
  ![Vorschau der Änderungen](..\media-draft\4-preview-changes.png)

1. Dann wird ein weiteres Dialogfeld angezeigt, in dem Sie aufgefordert werden, die Lizenz anzunehmen. Klicken Sie auf **I Accept** (Annehmen).
  ![Lizenz](..\media-draft\5-licence.png)

Nach wenigen Sekunden wird im Ausgabebereich in Visual Studio zusätzliche Aktivität angezeigt. Das bedeutet, dass das Paket zu Ihrem Projekt hinzugefügt wurde.
Sie können prüfen, ob das Paket erfolgreich gespeichert wurde, indem Sie erst die Option **Abhängigkeiten** in Ihrem Projekt und dann die Option **NuGet** erweitern. Dann wird ein Verweis auf **WindowsAzure.Storage** aufgelistet.

![Paketüberprüfung](..\media-draft\6-package-check.png)

