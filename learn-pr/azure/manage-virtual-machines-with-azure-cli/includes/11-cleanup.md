Sie haben mit der Azure CLI einen neuen virtuellen Linux-Computer erstellt, seine Größe geändert, ihn angehalten und gestartet und die Konfiguration aktualisiert.

## <a name="cleanup"></a>Bereinigen

Jetzt sind wir mit dem Bearbeiten des virtuellen Computers fertig und benötigen ihn nicht mehr. Also löschen wir die Ressourcen. Diese Bereinigung ist wichtig, damit die Compute- und Speicherressourcen nicht weiter für Ihr Konto abgerechnet werden. 

Sie können mit dem Befehl „`delete`“ einzelne Ressourcen löschen. Die einfachste Methode besteht aber darin, mit „`az group delete`“ alles zu entfernen. Führen Sie in der Azure CLI folgenden Befehl aus:

```azurecli
az group delete --name ExerciseResources --no-wait
```

Wenn Sie dazu aufgefordert werden, antworten Sie mit „yes“, oder verwenden Sie den `--yes`-Parameter, um die Antwort automatisch zu geben.

Dieser Befehl löscht alle der Ressourcengruppe zugeordneten Ressourcen und hebt ihre Zuordnung garantiert in der richtigen Reihenfolge auf. Der Parameter „`--no-wait`“ verhindert eine Blockierung durch die Azure CLI, während der Löschvorgang ausgeführt wird. Lassen Sie den Parameter deaktiviert, um zu warten, bis die Ressourcen gelöscht wurden. Sie können auch den `az group wait -n ExerciseResources --deleted`-Befehl später im Skript verwende, um darauf zu warten, dass der Löschvorgang beendet wird.


## <a name="further-reading"></a>Weitere nützliche Informationen

- [Übersicht über die Azure CLI](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)
- [Azure CLI-Befehlsreferenz](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest)
