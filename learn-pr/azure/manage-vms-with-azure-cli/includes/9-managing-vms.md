Eine der Hauptaufgaben, die Sie sollten den ausgeführten virtuellen Computern ist zum Starten und beenden sie.

## <a name="stopping-a-vm"></a>Beenden eines virtuellen Computers

Wir können einen ausgeführten virtuellen Computer mit Beenden der `vm stop` Befehl. Sie müssen den Namen und die Ressourcengruppe oder die eindeutige ID für den virtuellen Computer übergeben:

```azurecli
az vm stop -n SampleVM -g ExerciseResources
```

Wir können sicherstellen, es wurde von beendet, es wird versucht, die öffentliche IP-Adresse pingen, die mithilfe von `ssh`, oder über die `vm get-instance-view` Befehl. Dieser letzte Ansatz gibt die gleichen grundlegenden Daten wie `vm show` aber enthält Details über die Instanz selbst. Wiederholen Sie den folgenden Befehl eingeben, in der Cloud-Shell, um den aktuellen Ausführungsstatus des virtuellen Computers finden Sie unter:

```azurecli
az vm get-instance-view -n SampleVM -g ExerciseResources --query "instanceView.statuses[?starts_with(code, 'PowerState/') == `true`].displayStatus" -o tsv
```

Dieser Befehl sollte zurückgeben `VM stopped` als Ergebnis.

## <a name="starting-a-vm"></a>Starten eines virtuellen Computers

Können wir das Gegenteil durch die `vm start` Befehl.

```azurecli
az vm start -n SampleVM -g ExerciseResources
```

Dieser Befehl startet einen angehaltenen virtuellen Computer. Wir können es durch Überprüfen der `vm get-instance-view` Abfrage, die jetzt zurückgeben soll `VM running`.

## <a name="restarting-a-vm"></a>Neustarten eines virtuellen Computers

Schließlich können wir einen virtuellen Computer starten, wenn wir Änderungen vorgenommen haben, die erfordern einen Neustart mit dem `vm restart` Befehl. Sie können hinzufügen, die `--no-wait` auszugeben, wenn Sie die CLI sofort zurückgegeben, ohne zu warten, für den virtuellen Computer neu starten möchten.

