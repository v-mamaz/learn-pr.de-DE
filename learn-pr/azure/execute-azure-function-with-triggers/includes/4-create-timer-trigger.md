In dieser Übung erstellen wir eine Azure-Funktion, die alle 20 Sekunden mithilfe eines Zeitgebertriggers aufgerufen wird.

> [!NOTE] 
> Um diese Übung zu absolvieren, stellen Sie sicher, dass Sie im [Azure-Portal](https://portal.azure.com?azure-portal=true) mit einem gültigen Konto angemeldet sind.

## <a name="create-an-azure-function"></a>Erstellen einer Azure-Funktion

Wir beginnen, indem wir eine Azure-Funktion im Portal erstellen.

1. Klicken Sie im linken Navigationsbereich auf **Ressource erstellen**.

2. Wählen Sie **Compute** aus.

3. Wechseln Sie zu **Funktionen-App**. Sie können optional auch die Suchleiste verwenden, um die Vorlage zu finden.

    ![Auswählen von „Funktionen-App“](../media-drafts/4-click-function-app.png)

4. Geben Sie einen eindeutigen **App-Namen** ein.

5. Wählen Sie ein **Abonnement** aus.

6. Erstellen Sie eine neue **Ressourcengruppe**.

7. Wählen Sie **Windows** als Ihr **Betriebssystem** aus.

8. Wählen Sie als **Hostingplan** die Option **Verbrauchstarif**. Jede Ausführung der Funktion wird Ihnen in Rechnung gestellt. Ressourcen werden basierend auf dem Workload Ihrer Anwendung automatisch zugeordnet.

9. Wählen Sie einen **Standort** aus.

10. Erstellen Sie ein neues **Speicherkonto**. Sie können den Namen des Kontos ändern, wenn Sie möchten. Standardmäßig wird eine Variation des App-Namens ausgewählt.

11. Deaktivieren Sie **Application Insights**.

12. Klicken Sie auf **Erstellen**. Der Erstellungsvorgang nimmt einige Minuten in Anspruch. Sie können den Fortschritt über das Symbol **Benachrichtigungen** im Symbolleistenbereich nachverfolgen. Sobald die Ressource erstellt wurde, wird eine Schaltfläche zum Öffnen der Ressource im Azure-Portal angezeigt.

## <a name="create-a-timer-trigger"></a>Erstellen eines Zeitgebertriggers

Wir erstellen nun in unserer Azure-Funktion einen Zeitgebertrigger.

1. Nachdem die Azure-Funktion erstellt wurde, wählen Sie im linken Navigationsbereich **Alle Ressourcen** aus.

2. Wählen Sie Ihre Azure-Funktion aus.

3. Zeigen Sie auf dem neuen Blatt auf **Funktionen**, und wählen Sie das Pluszeichen (+) aus.

    ![Auf „Funktionen“ zeigen und Pluszeichen auswählen](../media-drafts/4-hover-function.png)

4. Wählen Sie **Zeitgeber** aus.

5. Wählen Sie **CSharp** als Sprache aus.

6. Wählen Sie **Diese Funktion erstellen** aus.

## <a name="configure-the-timer-trigger"></a>Konfigurieren des Zeitgebertriggers

Wir haben eine Azure-Funktion mit Logik zum Ausgeben einer Meldung im Protokollfenster. Wir stellen den Zeitplan des Zeitgebers so ein, dass er alle 20 Sekunden ausgeführt wird.

1. Wählen Sie **Integrieren** aus.

2. Geben Sie den folgenden Wert in das Feld **Zeitplan** ein:

    ```
    */20 * * * * *
    ```

3. Wählen Sie **Speichern** aus.

## <a name="start-the-timer"></a>Starten des Zeitgebers

Nachdem wir den Zeitgeber konfiguriert haben, können wir ihn starten.

1. Wählen Sie **TimerTriggerCSharp1** aus. 

    > [!NOTE]
    > **TimerTriggerCSharp1** ist ein Standardname. Er wird beim Erstellen des Zeitgebers automatisch generiert.

2. Klicken Sie auf **Ausführen**. 

An diesem Punkt sollte im Protokollfenster alle 20 Sekunden eine Meldung angezeigt werden.

## <a name="clean-up"></a>Bereinigen

Um sicherzustellen, dass Sie für diese Funktion keine Gebühren anfallen, wählen Sie über das Protokollfenster **Anhalten** aus, um den Zeitgeber anzuhalten.

![Anhalten](../media-drafts/4-pause-timer.png)


