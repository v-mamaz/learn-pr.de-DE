In diesem Modul wurden vier verschiedene Azure-Dienste vorgestellt, die es Ihnen ermöglichen, zuverlässige und resiliente verteilte Anwendungen zu erstellen. Die Wahl des richtigen Diensts hängt in erster Linie von dem Typ der Daten ab, die an die einzelnen Komponenten (Nachrichten und Ereignisse) übergeben werden sollen. Zudem spielt es eine Rolle, welche Features zugestellt und welche Daten verarbeitet werden müssen.

## <a name="clean-up-the-azure-subscription"></a>Bereinigen des Azure-Abonnements

Wenn ein Speicherkonto Daten enthält, verursacht dieses Kosten im Zusammenhang mit Ihrem Azure-Abonnement. Allerdings sind die Kosten bei kurzen Warteschlangen mit wenigen Nachrichten nur gering. Wenn Sie die Warteschlange nicht mehr verwenden, sollten Sie diese entfernen, damit keine unnötigen Änderungen an ihr vorgenommen werden können. Da Sie sämtliche Ressourcen in nur einer Ressourcengruppe erstellt haben, können Sie Ihr Azure-Abonnement am einfachsten bereinigen, indem Sie die Ressourcengruppe entfernen, die wiederum all ihre Inhalte entfernt:

```powershell
Remove-AzureRmResourceGroup -Name "MusicSharingResourceGroup" -Force
```

Wenn Sie aufgefordert werden, den Löschvorgang zu bestätigen, klicken Sie auf **Ja**.

Der Befehl zum Löschen der Ressourcen kann mehrere Minuten in Anspruch nehmen.
