Eine der Hauptaufgaben, die bei der Ausführung virtueller Computer anfällt, ist deren Starten und Beenden.

## <a name="stopping-a-vm"></a>Beenden einer VM

Wir können einen ausgeführten virtuellen Computer mit dem Befehl `vm stop` beenden. Sie müssen den Namen und die Ressourcengruppe oder die eindeutige ID der VM übergeben:

```azurecli
az vm stop -n SampleVM -g <rgn>[Sandbox resource group name]</rgn>
```

Wir können überprüfen, ob die VM beendet wurde, indem wir versuchen, die öffentliche IP-Adresse mit `ssh` oder über den Befehl `vm get-instance-view` zu pingen. Dieser letzte Ansatz liefert die gleichen grundlegenden Daten wie `vm show`, enthält aber Details zur Instanz selbst. Geben Sie den folgenden Befehl in Azure Cloud Shell ein, um den aktuellen Status Ihrer VM einzusehen:

```azurecli
az vm get-instance-view -n SampleVM -g <rgn>[Sandbox resource group name]</rgn> --query "instanceView.statuses[?starts_with(code, 'PowerState/')].displayStatus" -o tsv
```

Dieser Befehl sollte `VM stopped` als Ergebnis zurückgeben.

## <a name="starting-a-vm"></a>Starten einer VM

Den umgekehrten Vorgang können wir mit dem Befehl `vm start` auslösen.

```azurecli
az vm start -n SampleVM -g <rgn>[Sandbox resource group name]</rgn>
```

Dieser Befehl startet eine beendete VM. Wir können dies durch die Abfrage `vm get-instance-view` überprüfen, die nun `VM running` zurückgeben sollte.

## <a name="restarting-a-vm"></a>Neustarten einer VM

Schließlich können wir eine VM mit dem Befehl `vm restart` neu starten, nachdem wir Änderungen vorgenommen haben, die einen Neustart erfordern. Sie können das Flag `--no-wait` hinzufügen, wenn Sie möchten, dass die Azure CLI sofort wieder verfügbar ist, ohne auf den Neustart der VM zu warten.

