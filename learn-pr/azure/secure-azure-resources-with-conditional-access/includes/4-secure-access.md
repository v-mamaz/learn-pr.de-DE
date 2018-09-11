In der vorherigen Übung haben wir zum Testen unserer Lösung Testlizenzen aktiviert bzw. ein Verzeichnis, einen Benutzer und eine Gruppe erstellt. In dieser Übung erstellen wir die Regel für bedingten Zugriff, sodass für den Zugriff auf das Azure-Portal Multi-Factor Authentication erforderlich ist.

## <a name="enable-conditional-access-based-multi-factor-authentication"></a>Aktivieren von Multi-Factor Authentication mit bedingtem Zugriff

Durch den bedingten Zugriff können Administratoren konfigurieren, was sie zulassen und was nicht. Sie können gleichzeitig mehrere Regeln verwenden, um den Zugriff auf Ressourcen zu gewähren oder zu verweigern. Hier ist die Regel, die wir erstellen müssen:

**Beim Zugriff auf das Azure-Portal: mehrstufige Authentifizierung anfordern**

Die folgenden Schritte führen Sie durch den Prozess zum Erstellen einer Regel für den bedingten Zugriff, damit Benutzer eine mehrstufige Authentifizierung durchführen müssen, wenn sie auf das Azure-Portal zugreifen.

1. Navigieren Sie zu **Azure Active Directory** > **Bedingter Zugriff**.

1. Klicken Sie auf **Neue Richtlinie**.

1. Benennen Sie die Richtlinie **Mehrstufige Authentifizierung für Zugriff auf Azure-Portal erforderlich**.

1. Klicken Sie unter **Zuweisungen** > **Benutzer und Gruppen** auf **Benutzer und Gruppen**. Wählen Sie die erstellte Gruppe **CA-MFA-AzurePortal** aus. Klicken Sie dann auf **Fertig**.

1. Klicken Sie unter **Cloud-Apps** > **Apps auswählen** auf **Microsoft Azure Management**.

1. Klicken Sie unter **Zugriffssteuerung** > **Gewähren** auf **Mehrstufige Authentifizierung anfordern**.

1. Legen Sie **Richtlinie aktivieren** auf **Ein** fest.

1. Klicken Sie auf **Erstellen**.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie gelernt, wie Sie eine Regel mit bedingtem Zugriff erstellen. Die Regel erfordert Multi-Factor Authentication beim Zugriff auf das Azure-Portal.
