In diesem Modul haben Sie gelernt, wie Sie mithilfe des Azure-Portals einen virtuellen Linux-Computer erstellen. Anschließend haben Sie eine Verbindung mit der öffentlichen IP-Adresse dieses virtuellen Computers hergestellt und ihn mit einer SSH-Verbindung verwaltet. 

Sie haben gelernt, dass SSH eine Interaktion mit dem Betriebssystem und der Software des virtuellen Computers ermöglicht, während das Portal eine Konfiguration der virtuellen Hardware und der Konnektivität ermöglicht. Wenn eine Befehlszeile oder eine skriptfähige Umgebung bevorzugt gewesen wäre, hätten wir auch PowerShell oder die Azure CLI verwenden können.

## <a name="clean-up-the-resources"></a>Bereinigen der Ressourcen

Sie bezahlen für virtuelle Computer, während diese ausgeführt werden und für den verwendeten Speicherplatz. Wenn Sie virtuelle Computer nicht benutzen, sollten Sie diese immer beenden und deren Zuordnung aufheben. Außerdem ist es ratsam, nicht mehr benötigte Ressourcen zu löschen. Um alle von Ihnen erstellte Ressourcen zu entfernen, können Sie diese entweder nacheinander oder die gesamte Ressourcengruppe löschen.

1. Melden Sie sich beim Azure-Portal an.

1. Wählen Sie im Menü links **Alle Dienste** aus.

1. Klicken Sie auf **Ressourcengruppen**.

1. Suchen Sie nach der Ressourcengruppe, die Sie in der ersten Übung erstellt haben. Klicken Sie auf die Auslassungspunkte (...) rechts neben der Listenansicht.

1. Klicken Sie auf die Option **Ressourcengruppe löschen**.

1. Geben Sie auf dem nächsten Bildschirm den Namen der Ressourcengruppe ein, um den Löschvorgang zu bestätigen.

1. Klicken Sie auf **Löschen**.
