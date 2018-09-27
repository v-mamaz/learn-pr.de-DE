In dieser Einheit erfahren Sie, wie Sie eine Azure-Funktions-App erstellen, die alle 20 Sekunden mithilfe eines Timertriggers aufgerufen wird.

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-an-azure-function-app"></a>Erstellen einer Azure-Funktions-App

Erstellen Sie zuerst eine Azure-Funktions-App im Portal.

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) mit dem Konto an, über das Sie die Sandbox aktiviert haben.

1. Wählen Sie im linken Navigationsbereich **Ressource erstellen** aus.

1. Wählen Sie **Compute** aus.

1. Wechseln Sie zu **Funktionen-App**. Sie können optional auch die Suchleiste verwenden, um die Vorlage zu finden.

    ![Screenshot: Blatt „Ressource erstellen“ im Azure-Portal mit hervorgehobener Funktions-App.](../media/4-click-function-app.png)

1. Geben Sie einen global eindeutigen **App-Namen** ein.

1. Wählen Sie ein **Abonnement** aus.

1. Wählen Sie die vorhandene **Ressourcengruppe** <rgn>[Name der Sandboxressourcengruppe]</rgn> aus.

1. Wählen Sie **Windows** als Ihr **Betriebssystem** aus.

1. Wählen Sie als **Hostingplan** die Option **Verbrauchstarif**. Jede Ausführung der Funktion wird Ihnen in Rechnung gestellt. Ressourcen werden basierend auf dem Workload Ihrer Anwendung automatisch zugeordnet.

1. Wählen Sie einen **Standort** aus der unten verfügbaren Liste aus.

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

1. Erstellen Sie ein neues **Speicherkonto**. Sie können den Namen des Kontos ändern, wenn Sie möchten. Standardmäßig wird eine Variation des App-Namens ausgewählt.

1. Wählen Sie **Erstellen** aus. Sobald die Funktions-App bereitgestellt ist, wechseln Sie im Portal zu **Alle Ressourcen**. Die Funktions-App wird mit dem Typ **App Service** aufgelistet und hat den Namen, den Sie ihr gegeben haben.

## <a name="create-a-timer-trigger"></a>Erstellen eines Timertriggers

Wir erstellen nun in unserer Funktion einen Timertrigger.

1. Wenn die Funktion erstellt wurde, klicken Sie im linken Navigationsbereich auf **Alle Ressourcen**.

1. Suchen Sie in der Liste nach der Funktions-App, und wählen Sie sie aus.

1. Zeigen Sie auf dem neuen Blatt auf **Funktionen**, und klicken Sie auf das Pluszeichen (+).

    ![Screenshot: Blatt „Funktions-App“ im Azure-Portal mit hervorgehobenem Pluszeichen (+) im Untermenü „Funktionen“](../media/4-hover-function.png)

1. Klicken Sie auf **Zeitgeber**.

1. Wählen Sie **CSharp** als Sprache aus.

1. Wählen Sie **Diese Funktion erstellen** aus.

## <a name="configure-the-timer-trigger"></a>Konfigurieren des Timertriggers

Wir verfügen über eine Azure-Funktions-App mit Logik zum Ausgeben einer Meldung im Protokollfenster. Der Zeitplan des Timers wird so eingestellt, dass er alle 20 Sekunden ausgeführt wird.

1. Wählen Sie **Integrieren** aus.

1. Geben Sie den folgenden Wert in das Feld **Zeitplan** ein:

    ```log
    */20 * * * * *
    ```

1. Wählen Sie **Speichern** aus.

## <a name="test-the-timer"></a>Testen des Timers

Nachdem Sie nun den Timer konfiguriert haben, ruft er die Funktion in dem von uns definierten Intervall auf.

1. Wählen Sie **TimerTriggerCSharp1** aus.

    > [!NOTE]
    > **TimerTriggerCSharp1** ist ein Standardname. Er wird beim Erstellen des Triggers automatisch generiert.

1. Öffnen Sie unten in der Anzeige den Bereich **Protokolle**.

1. Beobachten Sie, wie alle 20 Sekunden neue Meldungen im Protokollfenster eingehen.

1. Damit die Funktion nicht mehr länger ausgeführt wird, wählen Sie **Verwalten**, und ändern Sie dann den **Funktionszustand** in *Deaktiviert*.
