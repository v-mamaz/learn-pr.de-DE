Sie haben nun sowohl die Azure IoT Central-Anwendung verwendet als auch die Kaffeemaschine mit Azure IoT Central verbunden. Das heißt, Sie können bald mit der Überwachung und Verwaltung Ihrer Remote-Kaffeemaschine beginnen. In diesem Modul überprüfen Sie das Setup und die Verbindung, indem Sie die optimale Temperatur in den Einstellungen aktualisieren, Befehle zum Überprüfen des Computerzustands ausführen und die verbundene Kaffeemaschine im Dashboard anzeigen. 

## <a name="edit-setting-to-see-if-the-application-syncs-with-the-coffee-machine"></a>Bearbeiten einer Einstellung, um sich zu vergewissern, dass die Anwendung mit der Kaffeemaschine synchronisiert wird

Senden Sie über die Einstellungen Ihrer Anwendung Konfigurationsdaten an die Kaffeemaschine. In diesem Szenario ändern Sie die optimale Temperatur und klicken anschließend auf **Aktualisieren**. Die geänderte Einstellung wird auf der Benutzeroberfläche als ausstehend markiert, bis die Kaffeemaschine bestätigt, dass sie auf die Einstellungsänderung reagiert hat. Die erfolgreiche Einstellungsänderung zeigt, dass der Datenfluss und somit die Verbindung funktioniert. Die Telemetriemessungen reagieren auf die Aktualisierung der optimalen Temperatur. Die Änderung kann auf der Seite mit den Messungen beobachtet werden. 

  ![Aktualisieren der Einstellungen](../images/3-settings-a.png)

## <a name="run-commands-and-receive-confirmation-messages-sent-by-the-coffee-machine"></a>Ausführen von Befehlen und Empfangen von Bestätigungsmeldungen von der Kaffeemaschine 
Aktivieren Sie den **Entwurfsmodus**, um **neue Befehle** hinzuzufügen.

1. Starten Sie einen Brühvorgang per Remotezugriff. Die Kaffeemaschine startet den Vorgang, wenn die drei folgenden Bedingungen erfüllt sind:
    - Tasse erkannt
    - Nicht im Wartungsmodus
    - Noch kein Brühvorgang gestartet

    Nach erfolgreichem Start des Brühvorgangs wechselt der Zustand der Maschine unter „Measurements“ (Messungen) > „State“ (Zustand) zu Gelb. 
    ![Auszuführende Befehle](../images/3-commands-b.png)

    Prüfen Sie das Konsolenprotokoll der simulierten Kaffeemaschine auf Bestätigungsmeldungen. 
    ![Auszuführende Befehle](../images/3-commands-brewing.png)

2. Aktivieren Sie den Wartungsmodus. Die Kaffeemaschine wird in den Wartungsmodus versetzt, sofern Sie sich *nicht* bereits im Wartungsmodus befindet.
    ![Auszuführende Befehle](../images/3-commands-c.png)
    
    Prüfen Sie das Konsolenprotokoll der simulierten Kaffeemaschine auf Bestätigungsmeldungen. 
    > [!NOTE]
    > Die simulierte Kaffeemaschine bleibt im Wartungsmodus, bis Sie den Clientcode neu starten – genau wie in der Realität, wenn ein Techniker die Maschine offline schaltet, um Reparaturen vorzunehmen, und sie anschließend wieder online schaltet.
    ![Auszuführende Befehle](../images/3-commands-maintenance.png)

## <a name="view-the-coffee-machine-in-the-dashboard"></a>Anzeigen der Kaffeemaschine im Dashboard
Im Dashboard laufen die relevanten Informationen zu Ihrer Kaffeemaschine zusammen. 

1. Klicken Sie auf **Liniendiagramm**, und geben Sie als Titel die Zeichenfolge „Temperatur“ ein, um die Telemetriedaten anzuzeigen. Wählen Sie unter **Zeitbereich** die **letzten 30 Minuten** aus.
![Anzeigen des Dashboards](../images/3-dashboard-a.png)

1. Klicken Sie auf **Settings and Properties** (Einstellungen und Eigenschaften), und geben Sie als Titel die Zeichenfolge „Geräteeigenschaften“ ein. Wählen Sie unter **Hinzufügen/Entfernen** die Optionen für die höchste und niedrigste Kaffeemaschinentemperatur sowie die Option für die abgelaufene Gerätegarantie aus. 
![Anzeigen des Dashboards](../images/3-dashboard-b.png)

1. Klicken Sie auf **Settings and Properties** (Einstellungen und Eigenschaften), und geben Sie als Titel die Zeichenfolge „Optimal Temperature“ (Optimale Temperatur) ein. Wählen Sie unter **Hinzufügen/Entfernen** die Option „Optimal Temperature“ (Optimale Temperatur) aus. 
![Anzeigen des Dashboards](../images/3-dashboard-c.png)


## <a name="summary"></a>Zusammenfassung

In diesem Modul haben Sie die Verbindung zwischen der simulierten Kaffeemaschine und Azure IoT Central überprüft. Hierzu haben Sie durch Ausführen der entsprechenden Befehle die optimale Temperatur aktualisiert. Zum Schluss haben Sie außerdem das Dashboard eingerichtet, um Ihre Kaffeemaschine an einem zentralen Ort überwachen zu können. Dabei haben Sie definiert, welche Informationen zu Ihrer Kaffeemaschine angezeigt werden sollen. Diese Überprüfungsschritte sind erforderlich, bevor Sie mit den anderen Aufgaben im nächsten Modul fortfahren. 