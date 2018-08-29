## <a name="module-summary"></a>Zusammenfassung des Moduls
In diesem Modul haben Sie die Azure CLI-Befehle verwendet, um eine Ressourcengruppe zu erstellen und eine Web-App mithilfe einer kleinen Menge von Befehlen bereitzustellen. Diese Befehle können als Teil der Automatisierungslösung zu einem Shellskript zusammengefasst werden.

Die Azure CLI ist eine gute Wahl für alle, die mit der Azure-Befehlszeile und Skripterstellung noch nicht vertraut sind. Durch die einfache Syntax und plattformübergreifende Kompatibilität wird das Fehlerrisiko bei regelmäßigen und sich wiederholenden Aufgaben reduziert.

## <a name="cleanup"></a>Bereinigen
Für die Ausführung von Web-Apps fallen Kosten in Ihrem Abonnement an. Entfernen Sie nicht benötigte Ressourcen, um unnötige Gebühren zu vermeiden. Die einfachste Möglichkeit, Ihr Azure-Abonnement zu bereinigen, ist das Entfernen der Ressourcengruppe. Dabei werden auch alle VMs in der Gruppe gelöscht. Wenn Sie mit diesem Modul fertig sind, führen Sie das folgende Azure PowerShell-Cmdlet aus:

    ```azurecli
    az group delete --resource-group popupResGroup
    ```

Sie werden aufgefordert, den Löschvorgang zu bestätigen. Wählen Sie **Ja** aus. Der Befehl zum Löschen der Ressourcen kann mehrere Minuten in Anspruch nehmen. 