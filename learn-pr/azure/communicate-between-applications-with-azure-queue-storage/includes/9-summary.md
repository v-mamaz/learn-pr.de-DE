In diesem Modul haben Sie erfahren, wie mit Warteschlangen in Azure-Speicherkonten Nachrichten zwischen Komponenten in einer verteilten Anwendung ausgetauscht werden. Dadurch kann die Zuverlässigkeit und Fehlerresilienz bei starker Auslastung erhöht werden. Wenn Sie die Microsoft Azure Storage-Clientbibliothek für .NET verwenden, können Sie problemlos C#- oder VB.NET-Code schreiben, mit dem Warteschlangen erstellt oder diesen Warteschlangen Nachrichten hinzugefügt bzw. aus diesen abgerufen oder entfernt werden.

## <a name="clean-up-the-resources"></a>Bereinigen der Ressourcen

Bei Speicherkonten, die Daten enthalten, können Kosten im Zusammenhang mit Ihrem Azure-Abonnement anfallen. Da die hier genutzten Datenmengen gering sind, wären die Kosten zwar niedrig, jedoch empfiehlt es sich immer, alle Ressourcen zu entfernen.

Da Sie sämtliche Ressourcen in nur einer Ressourcengruppe erstellt haben, können Sie Ihr Azure-Abonnement am einfachsten bereinigen, indem Sie die Ressourcengruppe entfernen, die wiederum all ihre Inhalte entfernt:

```azurecli
az group delete --name ExerciseResources --yes --no-wait
```

Mit der `--no-wait`-Option können Sie mit dem nächsten Modul fortfahren, ohne auf den Abschluss des Befehls warten zu müssen.