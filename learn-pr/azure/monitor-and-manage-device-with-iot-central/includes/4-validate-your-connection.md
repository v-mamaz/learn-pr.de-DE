Sie haben nun sowohl die Azure IoT Central-Anwendung verwendet als auch die Kaffeemaschine mit Azure IoT Central verbunden. Das heißt, Sie können bald mit der Überwachung und Verwaltung Ihrer Remote-Kaffeemaschine beginnen. In dieser Einheit überprüfen Sie Ihr Setup und die Verbindung unter Verwendung der zuvor definierten Vorlage „Connected Coffee Maker“ (Verbundene Kaffeemaschine). Sie aktualisieren die optimale Temperatur in den Einstellungen, führen Befehle zur Überprüfung des Zustands der Maschine aus und sehen sich Ihre verbundene Kaffeemaschine auf dem Dashboard an. 

## <a name="update-settings-to-sync-your-application-with-the-coffee-machine"></a>Aktualisieren von Einstellungen, um Ihre Anwendung mit der Kaffeemaschine zu synchronisieren

Auf der Seite „Einstellungen“ senden Sie Konfigurationsdaten von Ihrer Anwendung an die Kaffeemaschine. 

In diesem Szenario ändern Sie die optimale Temperatur und klicken anschließend auf **Aktualisieren**. Die geänderte Einstellung wird auf der Benutzeroberfläche als ausstehend markiert, bis die Kaffeemaschine bestätigt, dass sie auf die Einstellungsänderung reagiert hat. 

> [!NOTE]
> Die erfolgreiche Einstellungsänderung zeigt, dass der Datenfluss und somit die Verbindung funktioniert. Die Telemetriemessungen reagieren auf die Aktualisierung der optimalen Temperatur. Die Änderung kann auf der Seite mit den Messungen beobachtet werden. 

## <a name="run-commands-on-the-coffee-machine"></a>Ausführen von Befehlen für die Kaffeemaschine 
Navigieren Sie für die folgende Übung zur Seite **Befehle**. Zur Überprüfung des Befehlssetups führen Sie über IoT Central Remotebefehle für die Kaffeemaschine aus. Nach erfolgreicher Ausführung sendet die Kaffeemaschine Bestätigungsmeldungen.

1. Klicken Sie auf **Ausführen**, um per Remotezugriff einen Brühvorgang zu starten. 
    
    Die Kaffeemaschine startet den Vorgang, wenn die drei folgenden Bedingungen erfüllt sind:
    - Tasse erkannt
    - Nicht im Wartungsmodus
    - Noch kein Brühvorgang gestartet  

    > [!NOTE]
    > Nach erfolgreichem Start des Brühvorgangs wechselt der Zustand der Maschine unter „Measurements“ (Messungen) > „State“ (Zustand) zu Gelb. 
    
    Prüfen Sie das Konsolenprotokoll der Kaffeemaschine auf Bestätigungsmeldungen. 

    ![Auszuführende Befehle](../images/4-commands-brewing.png)

1. Klicken Sie auf **Ausführen**, um den Wartungsmodus festzulegen. Die Kaffeemaschine wird in den Wartungsmodus versetzt, sofern Sie sich *nicht* bereits im Wartungsmodus befindet.
    
    Prüfen Sie das Konsolenprotokoll der Kaffeemaschine auf Bestätigungsmeldungen. 

    > [!NOTE]
    > Die Kaffeemaschine bleibt im Wartungsmodus, bis Sie den Clientcode neu starten – genau wie in der Realität, wenn ein Techniker die Maschine offline schaltet, um Reparaturen durchzuführen, und sie anschließend wieder online schaltet.

    ![Auszuführende Befehle](../images/4-commands-maintenance.png)

1. Es empfiehlt sich, die Node.js-Anwendung nicht länger als etwa 60 Minuten auszuführen, um zu verhindern, dass Sie von der Anwendung unerwünschte Benachrichtigungen/E-Mails erhalten. Außerdem empfiehlt es sich, die Anwendung zu beenden, um das tägliche Nachrichtenkontingent nicht aufzubrauchen, wenn Sie nicht an dem Tutorial arbeiten.

## <a name="view-the-coffee-machine-in-the-dashboard"></a>Anzeigen der Kaffeemaschine auf dem Dashboard
Navigieren Sie zur Seite **Dashboard**. Hier laufen die relevanten Informationen zu Ihrer Kaffeemaschine zusammen. Aktivieren Sie für die folgende Übung den **Entwurfsmodus**, um Ihr Dashboard zu konfigurieren. Klicken Sie abschließend auf **Speichern**.

1. Klicken Sie auf **Liniendiagramm**, und geben Sie als Titel die Zeichenfolge „Telemetrie“ ein, um die Telemetriedaten anzuzeigen. Wählen Sie unter **Zeitbereich** die **letzten 30 Minuten** aus.

    ![Anzeigen des Dashboards](../images/4-dashboard-a.png)

1. Klicken Sie auf **Settings and Properties** (Einstellungen und Eigenschaften), und geben Sie als Titel die Zeichenfolge „Geräteeigenschaften“ ein. Wählen Sie unter **Hinzufügen/Entfernen** die Optionen für die höchste und niedrigste Kaffeemaschinentemperatur sowie die Option für die abgelaufene Gerätegarantie aus. 

1. Klicken Sie auf **Settings and Properties** (Einstellungen und Eigenschaften), und geben Sie als Titel die Zeichenfolge „Optimal Temperature“ (Optimale Temperatur) ein. Wählen Sie unter **Hinzufügen/Entfernen** die Option „Optimal Temperature“ (Optimale Temperatur) aus. 

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie die Verbindung zwischen der Kaffeemaschine und Azure IoT Central überprüft. Hierzu haben Sie durch Ausführen der entsprechenden Befehle die optimale Temperatur aktualisiert. Zum Schluss haben Sie außerdem das Dashboard eingerichtet, um Ihre Kaffeemaschine an einem zentralen Ort überwachen zu können. Dabei haben Sie definiert, welche Informationen zu Ihrer Kaffeemaschine angezeigt werden sollen. Diese Überprüfungsschritte sind erforderlich, bevor Sie mit den anderen Aufgaben in der nächsten Einheit fortfahren. 