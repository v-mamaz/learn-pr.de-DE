## <a name="module-summary"></a>Modul-Zusammenfassung
In diesem Modul können Sie eine Ressourcengruppe erstellen und Bereitstellen einer Web-app einen kleinen Satz von Befehlen mit Azure CLI-Befehle verwendet. Diese Befehle können in einem Shell-Skript als Teil des Automation-Lösung kombiniert werden.

Der Azure-Befehlszeilenschnittstelle ist eine gute Wahl für alle Benutzer, die noch nicht mit Azure Befehlszeilen- und skriptumgebung. Die einfache Syntax und plattformübergreifende Kompatibilität verringern das Risiko von Fehlern bei der reguläre und sich wiederholende Aufgaben ausführen.

## <a name="cleanup"></a>Cleanup
Ausführen von Web-apps fallen Kosten für Ihr Abonnement an. Entfernen Sie nicht benötigte Ressourcen, um unnötige Gebühren zu vermeiden. Die einfachste Möglichkeit zum Bereinigen von Ihrem Azure-Abonnement ist so entfernen Sie die Ressourcengruppe aus. Dabei werden auch alle Ressourcen in der Gruppe gelöscht. Wenn Sie mit diesem Modul fertig sind, führen Sie das folgende Azure PowerShell-Cmdlet:

    ```azurecli
    az group delete --resource-group popupResGroup
    ```

Wenn Sie aufgefordert werden, um den Löschvorgang zu bestätigen, beantworten **Ja**. Der Befehl dauert mehrere Minuten dauern, da Ressourcen gelöscht wurden. 