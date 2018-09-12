Angenommen, Sie möchten Azure Active Directory bereitstellen und verwenden Richtlinien für bedingten Zugriff, sodass für den Zugriff auf das Azure-Portal Multi-Factor Authentication erforderlich ist. Sie müssen ein Verzeichnis erstellen und temporäre Lizenzen zuweisen.

## <a name="create-a-directory"></a>Erstellen eines Verzeichnisses
Zuerst wird ein neues Verzeichnis für First Up Consultants, in dem ohne Auswirkungen auf die Produktionsbenutzer getestet werden kann.

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/?azure-portal=true) an.

1. Klicken Sie im linken Navigationsbereich auf **Ressource erstellen** > **Identität** > **Azure Active Directory**.

1. Geben Sie auf dem Blatt **Verzeichnis erstellen** die folgenden Werte für **Organisationsname** und **Name der Anfangsdomäne** ein:

   1. ORGANISATIONSNAME: `First Up Consultants`
   1. NAME DER ANFANGSDOMÄNE: `firstupconsultants<XXXX>.onmicrosoft.com`

1. Warten Sie, bis das Verzeichnis erstellt wurde. Klicken Sie auf den Link, um in das neue Verzeichnis zu wechseln, oder klicken Sie oben im Fenster auf **Directory and subscription filter** (Verzeichnis- und Abonnementfilter), und wählen Sie das neu erstellte Verzeichnis aus.

## <a name="get-trial-licenses"></a>Erhalten von Testlizenzen

Damit Sie Features wie den bedingten Zugriff und Multi-Factor Authentication verwenden können, benötigen Sie mindestens eine Testlizenz. Im Anschluss finden Sie eine Anleitung für das Aktivieren einer Testlizenz:

1. Klicken Sie im Azure AD-Bereich **Übersicht** auf den Link **Kostenlose Testversion starten**.

1. Klicken Sie unter dem Element **Azure AD Premium P2** auf **Kostenlose Testversion**, und klicken Sie dann auf **Aktivieren**.

## <a name="create-a-test-user"></a>Erstellen eines Testbenutzers

Die Lizenz muss mit einem Benutzer getestet werden. Isabella Simonsen, ein Mitglied Ihres Teams, hilft Ihnen dabei. Sie benötigt dazu ein Konto für das Verzeichnis. Wie Sie eines erstellen, erfahren Sie in den folgenden Schritten.

1. Navigieren Sie zu **Azure Active Directory** > **Benutzer** > **Alle Benutzer**.

1. Klicken Sie auf **Neuer Benutzer**.

1. Erstellen Sie einen Benutzer namens **Isabella Simonsen** mit dem folgenden Benutzernamen:

   * `Isabella@firstupconsultants<XXXX>.onmicrosoft.com`

1. Aktivieren Sie das Kontrollkästchen **Kennwort anzeigen** für den Benutzer. Notieren Sie sich das Kennwort, damit Sie es später beim Testen verwenden können.

1. Klicken Sie auf **Erstellen**.

## <a name="create-a-pilot-group"></a>Erstellen einer Pilotgruppe

Die Richtlinie, die erstellt wird, soll einer Benutzergruppe zugewiesen werden. Dazu muss zunächst eine Gruppe für diese Richtlinie erstellt werden. Anhand der folgenden Schritte können Sie eine Sicherheitsgruppe für die Pilotbereitstellung erstellen.

1. Navigieren Sie zu **Azure Active Directory** > **Gruppen** > **Alle Gruppen**.

1. Klicken Sie auf **Neue Gruppe**.

1. Legen Sie als Gruppentyp **Sicherheit** fest.

1. Legen Sie als Gruppenname **CA-MFA-AzurePortal** fest.

1. Legen Sie als Mitgliedschaftstyp **Zugewiesen** fest.

1. Wählen Sie den Benutzer aus, der im vorherigen Schritt erstellt wurde, und klicken Sie auf **Auswählen**.

1. Klicken Sie auf **Erstellen**.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie erfahren, wie Sie ein Verzeichnis mit einer Testlizenz, einen Testbenutzer und eine Pilotgruppe im Azure-Portal erstellen.
