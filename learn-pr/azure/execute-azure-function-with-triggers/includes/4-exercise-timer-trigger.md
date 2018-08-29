In dieser Übung erstellen wir eine Azure-Funktion, die alle 20 Sekunden mithilfe eines Zeitgebertriggers aufgerufen wird.

> [!NOTE] 
> Um diese Übung zu absolvieren, stellen Sie sicher, dass Sie im [Azure-Portal](https://portal.azure.com/) mit einem gültigen Konto angemeldet sind.

## <a name="create-an-azure-function"></a>Erstellen einer Azure-Funktion

Wir beginnen, indem wir eine Azure-Funktion im Portal erstellen.

1. Klicken Sie im linken Navigationsbereich auf **Ressourcengruppe erstellen**.

1. Wählen Sie **Compute** aus.

1. Wechseln Sie zu **Funktionen-App**. Sie können optional auch die Suchleiste verwenden, um die Vorlage zu finden.

    ![Auswählen von „Funktionen-App“](../media/4-click-function-app.png)

1. Geben Sie einen eindeutigen **App-Namen** ein.

1. Wählen Sie ein **Abonnement** aus.

1. Erstellen Sie eine neue **Ressourcengruppe**.

1. Wählen Sie **Windows** als Ihr **Betriebssystem** aus.

1. Wählen Sie als **Hostingplan** die Option **Verbrauchstarif**. Jede Ausführung der Funktion wird Ihnen in Rechnung gestellt. Ressourcen werden basierend auf dem Workload Ihrer Anwendung automatisch zugeordnet.

1. Wählen Sie einen **Speicherort** aus.

1. Erstellen Sie ein neues **Speicherkonto**. (Dieser Wert ist erforderlich, wird aber hier nicht verwendet.)

1. Deaktivieren Sie **Application Insights**.

1. Klicken Sie auf **Erstellen**.

## <a name="create-a-timer-trigger"></a>Erstellen eines Zeitgebertriggers

Wir erstellen nun in unserer Azure-Funktion einen Zeitgebertrigger.

1. Nachdem die Azure-Funktion erstellt wurde, wählen Sie im linken Navigationsbereich **Alle Ressourcen** aus.

1. Wählen Sie Ihre Azure-Funktion aus.

1. Zeigen Sie auf dem neuen Blatt auf **Funktionen**, und wählen Sie das Pluszeichen (+) aus.

    ![Auf „Funktionen“ zeigen und „Plus“ auswählen](../media/4-hover-function.png)

1. Wählen Sie **Zeitgeber** aus.

1. Wählen Sie **CSharp** als Sprache aus.

1. Wählen Sie **Diese Funktion erstellen** aus.

## <a name="configure-the-timer-trigger"></a>Konfigurieren des Zeitgebertriggers

Wir haben eine Azure-Funktion mit Logik zum Ausgeben einer Meldung im Protokollfenster. Wir stellen den Zeitplan des Zeitgebers so ein, dass er alle 20 Sekunden ausgeführt wird.

1. Wählen Sie **Integrieren** aus.

1. Geben Sie den folgenden Wert in das Feld **Zeitplan** ein:

    ```
    */20 * * * * *
    ```

1. Wählen Sie **Speichern** aus.

## <a name="start-the-timer"></a>Starten des Zeitgebers

Nachdem wir den Zeitgeber konfiguriert haben, können wir ihn starten.

1. Wählen Sie **TimerTriggerCSharp1** aus. 

    > [!NOTE]
    > **TimerTriggerCSharp1** ist ein Standardname. Er wird beim Erstellen des Zeitgebers automatisch generiert.

1. Klicken Sie auf **Ausführen**. 

An diesem Punkt sollte im Protokollfenster alle 20 Sekunden eine Meldung angezeigt werden.

## <a name="clean-up"></a>Bereinigen

Um sicherzustellen, dass Sie für diese Funktion keine Gebühren anfallen, wählen Sie über das Protokollfenster **Anhalten** aus, um den Zeitgeber anzuhalten.

![Anhalten](../media/4-pause-timer.png)


