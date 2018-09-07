In diesem Modul wurden vier verschiedene Azure-Dienste vorgestellt, die es Ihnen ermöglichen, zuverlässige und resiliente verteilte Anwendungen zu erstellen. Die Wahl des richtigen Diensts hängt in erster Linie vom Typ der Daten (Nachrichten oder Ereignisse) ab, die an die einzelnen Komponenten übergeben werden sollen. Zudem spielt es eine Rolle, welche Features Sie zum Bereitstellen und Verarbeiten der Daten benötigen.

## <a name="clean-up"></a>Bereinigen

Wenn ein Speicherkonto Daten enthält, verursacht dieses Kosten im Zusammenhang mit Ihrem Azure-Abonnement. Allerdings sind die Kosten bei kurzen Warteschlangen mit wenigen Nachrichten nur gering. Wenn Sie die Warteschlange nicht mehr verwenden, sollten Sie sie entfernen, um unnötige Kosten zu vermeiden. Da Sie sämtliche Ressourcen in der gleichen Ressourcengruppe erstellt haben, können Sie Ihr Azure-Abonnement am einfachsten bereinigen, indem Sie die Ressourcengruppe entfernen. Dadurch werden alle ihre Inhalte entfernt:

```powershell
Remove-AzureRmResourceGroup -Name "MusicSharingResourceGroup" -Force
```

Wenn Sie aufgefordert werden, den Löschvorgang zu bestätigen, klicken Sie auf **Ja**.

Der Befehl zum Löschen der Ressourcen kann mehrere Minuten in Anspruch nehmen.