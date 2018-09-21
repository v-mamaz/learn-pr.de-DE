Angenommen, Sie möchten Azure Active Directory bereitstellen und verwenden Richtlinien für bedingten Zugriff, sodass für den Zugriff auf das Azure-Portal Multi-Factor Authentication erforderlich ist. Sie müssen ein Verzeichnis erstellen und temporäre Lizenzen zuweisen.

## <a name="launch-lab-and-sign-in-to-the-azure-portal"></a>Starten des Labs und Anmelden beim Azure-Portal

1. Klicken Sie auf den obigen Link **VM-Modus starten**, um das Lab zu starten.

1. Melden Sie sich beim Azure-Portal als LabAdmin-<XXXXXXX>@triplecrownlabsoutlook.onmicrosoft.com an. Den Benutzernamen und das Kennwort finden Sie oben im Fenster auf der Registerkarte „Ressourcen“.

## <a name="create-a-directory"></a>Erstellen eines Verzeichnisses

Zuerst wird ein neues Verzeichnis für First Up Consultants erstellt, in dem ohne Auswirkungen auf die Produktionsbenutzer getestet werden kann.

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an.

1. Klicken Sie im linken Navigationsbereich auf **Ressource erstellen** > **Identität** > **Azure Active Directory**.

1. Geben Sie auf dem Blatt **Verzeichnis erstellen** die folgenden Werte für **Organisationsname** und **Name der Anfangsdomäne** ein:

   1. Organisationsname: `First Up Consultants`
   1. Name der Anfangsdomäne: `firstupconsultants<XXXXXXX>`, wobei <XXXXXXX> die Zahl ist, die nach dem Benutzernamen auf der Registerkarte **Ressourcen** am oberen Rand des Fensters mit den Anweisungen angezeigt wird.

1. Warten Sie, bis das Verzeichnis erstellt wurde. Klicken Sie auf den Link, um in das neue Verzeichnis zu wechseln, oder klicken Sie oben im Fenster auf **Verzeichnis- und Abonnementfilter**, und wählen Sie das neu erstellte Verzeichnis aus.

## <a name="get-trial-licenses"></a>Erhalten von Testlizenzen

Um Features wie den bedingten Zugriff und Multi-Factor Authentication zu verwenden, benötigen Sie mindestens eine Testlizenz. Im Anschluss finden Sie eine Anleitung für das Aktivieren einer Testlizenz:

1. Klicken Sie im Azure AD-Bereich **Übersicht** auf den Link **Kostenlose Testversion starten**.

1. Klicken Sie unter dem Element **Azure AD Premium P2** auf **Kostenlose Testversion**, und klicken Sie dann auf **Aktivieren**.

## <a name="create-a-test-user"></a>Erstellen eines Testbenutzers

Die Lizenz muss mit einem Benutzer getestet werden. Isabella Simonsen, ein Mitglied Ihres Teams, hilft Ihnen dabei. Sie benötigt dazu ein Konto für das Verzeichnis. Wie Sie eines erstellen, erfahren Sie in den folgenden Schritten.

1. Navigieren Sie zu **Azure Active Directory** > **Benutzer**.

1. Klicken Sie auf **Neuer Benutzer**.

1. Erstellen Sie einen Benutzer namens **Isabella Simonsen** mit dem folgenden Benutzernamen:

   `Isabella@firstupconsultants<XXXXXXX>.onmicrosoft.com`

   Ordnen Sie die Domäne nach dem @-Zeichen der Domäne zu, die Sie im Abschnitt *Erstellen eines Verzeichnisses* oben erstellt haben.

1. Aktivieren Sie das Kontrollkästchen **Kennwort anzeigen** für den Benutzer. Notieren Sie sich das Kennwort, damit Sie es später beim Testen verwenden können.

1. Klicken Sie auf **Erstellen**.

## <a name="create-a-pilot-group"></a>Erstellen einer Pilotgruppe

Die Richtlinie, die erstellt wird, soll einer Benutzergruppe zugewiesen werden. Dazu muss zunächst eine Gruppe für diese Richtlinie erstellt werden. Anhand der folgenden Schritte können Sie eine Sicherheitsgruppe für die Pilotbereitstellung erstellen.

1. Navigieren Sie zu **Azure Active Directory** > **Gruppen**.

1. Klicken Sie auf **Neue Gruppe**.

1. Legen Sie als Gruppentyp **Sicherheit** fest.

1. Legen Sie als Gruppenname **CA-MFA-AzurePortal** fest.

1. Legen Sie als Mitgliedschaftstyp **Zugewiesen** fest.

1. Wählen Sie den Benutzer aus, der im vorherigen Schritt erstellt wurde, und klicken Sie auf **Auswählen**.

1. Klicken Sie auf **Erstellen**.

In dieser Einheit haben Sie erfahren, wie Sie ein Verzeichnis mit einer Testlizenz, einen Testbenutzer und eine Pilotgruppe im Azure-Portal erstellen.