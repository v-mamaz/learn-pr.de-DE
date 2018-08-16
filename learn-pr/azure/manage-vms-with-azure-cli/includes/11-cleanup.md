Sie haben einen neuen virtuellen Linux-Computer erstellt, seine Größe geändert, beendet und gestartet und aktualisiert die Konfiguration mit der Azure CLI.

## <a name="cleanup"></a>Cleanup

Nun, wir sind nun mit dem virtuellen Computer fertig, und ihn nicht mehr benötigen, löschen wir die Ressourcen an. Bereinigung ist wichtig für Compute und Speicher-Ressourcen, die über Ihr Konto abgerechnet werden fortgesetzt werden können. 

Sie können einzelne Ressourcen Löschen der `delete` Befehl, doch die einfachste Möglichkeit, alles zu entfernen ist `az group delete`. Führen Sie den folgenden Befehl in der Azure CLI:

```azurecli
az group delete --name ExerciseResources --no-wait
```

Beantworten Sie "Ja", auf die Aufforderung, wenn Sie angezeigt werden soll, oder verwenden Sie die `--yes` Parameter an der Eingabeaufforderung automatische Antworten.

Dieser Befehl löscht alle Ressourcen der Ressourcengruppe zugeordnet und ist garantiert, sie in der richtigen Reihenfolge aufgehoben. Der Parameter `--no-wait` verhindert eine Blockierung durch die CLI, während der Löschvorgang ausgeführt wird. Lassen Sie sie aus, warten, bis die Ressourcen gelöscht werden soll. Oder verwenden Sie die `az group wait -n ExerciseResources --deleted` Befehl später im Skript zu warten, bis der Löschvorgang abgeschlossen.


## <a name="further-reading"></a>Weitere Informationen

* [Übersicht über die Azure CLI](https://docs.microsoft.com/en-us/cli/azure/?view=azure-cli-latest)
* [Azure CLI-Befehlsreferenz](https://docs.microsoft.com/en-us/cli/azure/reference-index?view=azure-cli-latest)
