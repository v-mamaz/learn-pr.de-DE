Sie haben nun sowohl die Azure IoT Central-Anwendung verwendet als auch die Kaffeemaschine mit Azure IoT Central verbunden. Das heißt, Sie können bald mit der Überwachung und Verwaltung Ihrer Remote-Kaffeemaschine beginnen. In dieser Einheit führen Sie einen Moment Zeit, überprüfen Ihr Setup und die Verbindung mit der verbundenen Kaffeemaschine-Vorlage, die Sie zuvor definiert. Sie aktualisieren die optimale Temperatur in den Einstellungen, führen Sie Befehle für den Status Ihres Computers zu überprüfen und Ihre verbundenen Kaffeemaschine im Dashboard anzeigen. 

## <a name="update-settings-to-sync-your-application-with-the-coffee-machine"></a>Einstellungen für Ihre Anwendung mit der Kaffeemaschine synchronisieren

Senden Sie auf der Seite Einstellungen für Konfigurationsdaten an den Kaffee-Computer aus Ihrer Anwendung auf. 

In diesem Szenario ändern Sie die optimale Temperatur und klicken anschließend auf **Aktualisieren**. Die geänderte Einstellung wird auf der Benutzeroberfläche als ausstehend markiert, bis die Kaffeemaschine bestätigt, dass sie auf die Einstellungsänderung reagiert hat. 

> [!NOTE]
> Erfolgreiche Updates in den Einstellungen definieren den Datenfluss und die Verbindung zu überprüfen. Die Telemetriedaten Messungen reagiert auf das Update in der optimalen Temperatur. Die Änderung kann auf der Seite mit den Messungen beobachtet werden. 

## <a name="run-commands-on-the-coffee-machine"></a>Ausführen von Befehlen auf dem Computer Kaffee 
Navigieren Sie zu der **Befehle** Seite in der folgenden Übung. Um die Befehle-Einrichtung zu überprüfen, führen Sie Remote Befehle auf dem Computer Kaffee aus IoT Central. Bei erfolgreicher Ausführung werden Bestätigungsnachrichten vom Computer Coffee gesendet.

1. Wählen Sie zunächst Brewing Remote **ausführen**. 
    
    Die Kaffeemaschine startet den Vorgang, wenn die drei folgenden Bedingungen erfüllt sind:
    - Tasse erkannt
    - Nicht im Wartungsmodus
    - Noch kein Brühvorgang gestartet  

    > [!NOTE]
    > Nach erfolgreichem Start des Brühvorgangs wechselt der Zustand der Maschine unter „Measurements“ (Messungen) > „State“ (Zustand) zu Gelb. 
    
    Suchen Sie nach Meldungen zur benutzerbestätigung in das Konsolenprotokoll, auf dem Computer Kaffee. 

    ![Ausführen von Befehlen](../images/4-commands-brewing.png)

1. Legen Sie den Wartungsmodus dazu **ausführen**. Wird zur Wartung der Kaffeemaschine festgelegt, ist dies *nicht* bereits im Wartungsmodus.
    
    Suchen Sie nach Meldungen zur benutzerbestätigung in das Konsolenprotokoll, auf dem Computer Kaffee. 

    > [!NOTE]
    > Wie im wirklichen Leben weiterhin die Kaffeemaschine, wenn der Techniker den Computer offline geschaltet wird, notwendige Reparaturen ausführen, bevor Sie sie wieder online wechseln, in den Wartungsmodus zu bleiben, bis Sie den Clientcode einen Neustart.

    ![Ausführen von Befehlen](../images/4-commands-maintenance.png)

1. Es wird empfohlen, dass Sie der Node.js-Anwendung nicht mehr als 60 Minuten oder dies zu verhindern, dass Sie unerwünschte Benachrichtigungen/e-Mails senden die Anwendung ausführen. Beenden der Anwendung aus, wenn Sie nicht auf dem Lernprogramm arbeiten verhindert auch das tägliche Nachrichtenkontingent aufbrauchen.

## <a name="view-the-coffee-machine-in-the-dashboard"></a>Anzeigen der Kaffeemaschine im Dashboard
Navigieren Sie zu der **Dashboard** , in denen zusammen finden Sie die relevante Informationen über Ihren Computer Kaffee. Aktivieren Sie für der folgenden Übung **Entwurfsmodus** so konfigurieren Sie Ihr Dashboard. Wenn Sie fertig sind, wählen Sie **speichern**.

1. Wählen Sie **Liniendiagramm** und geben Sie den Titel als Telemetrie, um die Telemetriedaten Messungen finden Sie unter. Wählen Sie unter **Zeitbereich** die **letzten 30 Minuten** aus.

    ![Anzeigen des Dashboards](../images/4-dashboard-a.png)

1. Klicken Sie auf **Settings and Properties** (Einstellungen und Eigenschaften), und geben Sie als Titel die Zeichenfolge „Geräteeigenschaften“ ein. Wählen Sie unter **Hinzufügen/Entfernen** die Optionen für die höchste und niedrigste Kaffeemaschinentemperatur sowie die Option für die abgelaufene Gerätegarantie aus. 

1. Klicken Sie auf **Settings and Properties** (Einstellungen und Eigenschaften), und geben Sie als Titel die Zeichenfolge „Optimal Temperature“ (Optimale Temperatur) ein. Wählen Sie unter **Hinzufügen/Entfernen** die Option „Optimal Temperature“ (Optimale Temperatur) aus. 

## <a name="summary"></a>Zusammenfassung

In dieser Einheit hat Sie etwas Zeit, um die Verbindung zwischen dem Kaffeemaschine, und suchen Sie in der Azure IoT Central zu überprüfen. Sie erreicht Überprüfung durch Aktualisieren der optimalen Temperatur, die Befehle ausführen. Zum Schluss haben Sie außerdem das Dashboard eingerichtet, um Ihre Kaffeemaschine an einem zentralen Ort überwachen zu können. Dabei haben Sie definiert, welche Informationen zu Ihrer Kaffeemaschine angezeigt werden sollen. Diese Überprüfungsschritte sind erforderlich, bevor Sie mit anderen Aufgaben in der nächsten Einheit. 