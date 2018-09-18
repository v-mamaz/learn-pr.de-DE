In diesem Modul haben Sie gelernt, wie Sie einen virtuellen Windows-Computer unter Verwendung des Azure-Portals erstellen. Anschließend haben Sie eine Verbindung mit der öffentlichen IP-Adresse dieses virtuellen Computers hergestellt und ihn über RDP verwaltet. Sie haben erfahren, wie RDP in Azure eine ähnliche Oberfläche bereitstellt wie bei der interaktiven Anmeldung bei einem physischen Computer.

Sie haben gelernt, dass RDP eine Interaktion mit dem Betriebssystem und der Software des virtuellen Computers ermöglicht, während das Portal eine Konfiguration der virtuellen Hardware und der Konnektivität ermöglicht. Wenn Sie eine Befehlszeile oder eine skriptfähige Umgebung bevorzugt hätten, hätten wir auch PowerShell oder die Azure CLI verwenden können.

## <a name="clean-up"></a>Bereinigen
<!---TODO: Update for sandbox?--->

Sie bezahlen für virtuelle Computer, während diese ausgeführt werden, und für den verwendeten Speicherplatz. Wenn Sie virtuelle Computer nicht verwenden, sollten sie diese immer beenden und deren Zuordnung aufheben. Außerdem empfiehlt es sich, nicht mehr benötigte Ressourcen zu löschen. Um alle von Ihnen erstellte Ressourcen zu entfernen, können Sie diese entweder nacheinander löschen oder einfach die gesamte Ressourcengruppe löschen.

1. Melden Sie sich beim Azure-Portal an.

1. Wählen Sie im Menü links **Alle Dienste** aus.

1. Klicken Sie auf **Ressourcengruppen**.

1. Suchen Sie nach der Ressourcengruppe, die Sie in der ersten Übung erstellt haben. Klicken Sie auf die Auslassungspunkte (...) rechts neben der Listenansicht.

1. Klicken Sie auf die Option **Ressourcengruppe löschen**.

1. Geben Sie auf dem nächsten Bildschirm den Namen der Ressourcengruppe ein, um den Löschvorgang zu bestätigen.

1. Klicken Sie auf **Löschen**.
