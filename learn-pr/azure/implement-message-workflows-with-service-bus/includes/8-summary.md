In diesem Modul haben Sie mithilfe des Azure-Portals einen Service Bus-Namespace, eine Warteschlange und ein Thema in Ihrem Abonnement erstellt und Nachrichten durch die Warteschlange und über das Thema gesendet und empfangen.

Service Bus-Warteschlangen und -Themen sind hervorragende Tools, mit denen Sie die Resilienz der Kommunikation innerhalb einer verteilten Anwendung steigern können. Indem sie als temporärer Speicherort dienen, lassen sie das Erfordernis direkter Kommunikation zwischen Komponenten entfallen und fangen Spitzen in der Auslastung weich ab. Erwägen Sie ihren Einsatz immer dann, wenn Sie eine Komponente verwenden, die mit anderen in einer locker gekoppelten Konfiguration kommunizieren kann.

## <a name="clean-up"></a>Bereinigen

Service Bus-Warteschlangen und -Themen in Ihrem Azure-Abonnement haben ihren Preis, der bei wenigen, kleinen Nachrichten aber wahrscheinlich niedrig ist. Die einfachste Möglichkeit zum Bereinigen Ihres Azure-Abonnements besteht darin, die Ressourcengruppe zu entfernen, die Sie während der ersten Übung erstellt haben. Auf diese Weise werden auch alle Themen, Warteschlangen, Namespaces und sonstigen in der Gruppe enthaltenen Ressourcen gelöscht. Führen Sie die folgenden Schritte aus, wenn Sie dieses Modul abgeschlossen haben:

1. Klicken Sie im **Azure-Portal** im linken Navigationsbereich auf **Ressourcengruppen**.
1. Klicken Sie in der Liste der Ressourcengruppen auf **SalesTeamRG**.
1. Klicken Sie auf dem Blatt **Ressourcengruppe** auf **Ressourcengruppe löschen**.
1. Geben Sie im Textfeld **TYPE THE RESOURCE GROUP NAME** (NAMEN DER RESSOURCENGRUPPE EINGEBEN) **SalesTeamAppRG** ein, und klicken Sie dann auf **Löschen**. Azure entfernt die Ressourcengruppe und alle darin enthaltenen Ressourcen.