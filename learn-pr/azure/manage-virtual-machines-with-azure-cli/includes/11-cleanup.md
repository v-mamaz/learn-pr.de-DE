Sie haben mit der Azure CLI einen neuen virtuellen Linux-Computer erstellt, seine Größe geändert, ihn angehalten und gestartet und die Konfiguration aktualisiert.

<!-- Cleanup sandbox -->
[!include[](../../../includes/azure-sandbox-cleanup.md)]

Wenn Sie in Ihrem eigenen Abonnement arbeiten, können Sie den folgenden Azure CLI-Befehl zum Löschen der Ressourcengruppe und alle zugeordneten Ressourcen ausführen.

```azurecli
az group delete --name [resource-group-name] --no-wait
```

Wenn Sie dazu aufgefordert werden, antworten Sie mit „yes“, oder verwenden Sie den `--yes`-Parameter, um die Antwort automatisch zu geben.

Dieser Befehl löscht alle der Ressourcengruppe zugeordneten Ressourcen und hebt ihre Zuordnung garantiert in der richtigen Reihenfolge auf. Der Parameter „`--no-wait`“ verhindert eine Blockierung durch die Azure CLI, während der Löschvorgang ausgeführt wird. Lassen Sie den Parameter deaktiviert, um zu warten, bis die Ressourcen gelöscht wurden. Sie können auch den `az group wait -n [resource-group-name] --deleted`-Befehl später im Skript verwende, um darauf zu warten, dass der Löschvorgang beendet wird.


## <a name="further-reading"></a>Weitere nützliche Informationen

- [Übersicht über die Azure CLI](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)
- [Azure CLI-Befehlsreferenz](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest)
