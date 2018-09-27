Sie haben nun sowohl die Azure IoT Central-Anwendung verwendet als auch die Kaffeemaschine mit Azure IoT Central verbunden. Das heißt, Sie können bald mit der Überwachung und Verwaltung Ihrer Remote-Kaffeemaschine beginnen. In dieser Einheit überprüfen Sie Ihr Setup und die Verbindung unter Verwendung der zuvor definierten Vorlage „Connected Coffee Maker“ (Verbundene Kaffeemaschine). Sie aktualisieren die optimale Temperatur in den Einstellungen, führen Befehle zur Überprüfung des Zustands der Maschine aus und sehen sich Ihre verbundene Kaffeemaschine auf dem Dashboard an. 

## <a name="update-settings-to-sync-your-application-with-the-coffee-machine"></a>Aktualisieren von Einstellungen, um Ihre Anwendung mit der Kaffeemaschine zu synchronisieren

Auf der Seite **Einstellungen** senden Sie Konfigurationsdaten von Ihrer Anwendung an die Kaffeemaschine. 

In diesem Szenario ändern Sie die optimale Temperatur und klicken anschließend auf **Aktualisieren**. Die geänderte Einstellung wird auf der Benutzeroberfläche als ausstehend markiert, bis die Kaffeemaschine bestätigt, dass sie auf die Einstellungsänderung reagiert hat. 

> [!NOTE]
> Die erfolgreiche Einstellungsänderung zeigt, dass der Datenfluss und somit die Verbindung funktioniert. Die Telemetriemessungen reagieren auf das Update der optimalen Temperatur. Die Änderung kann auf der Seite mit den **Messungen** beobachtet werden. 

## <a name="run-commands-on-the-coffee-machine"></a>Ausführen von Befehlen für die Kaffeemaschine 
Navigieren Sie für die folgende Übung zur Seite **Befehle**. Zur Überprüfung des Befehlssetups führen Sie über IoT Central Remotebefehle für die Kaffeemaschine aus. Nach erfolgreicher Ausführung der Befehle sendet die Kaffeemaschine Bestätigungsmeldungen.

1. Klicken Sie auf **Ausführen**, um per Remotezugriff einen Brühvorgang zu starten. 
    
    Die Kaffeemaschine startet den Vorgang, wenn die drei folgenden Bedingungen erfüllt sind:
    - Tasse erkannt
    - Nicht im Wartungsmodus
    - Noch kein Brühvorgang gestartet  

    > [!NOTE]
    > Nach erfolgreichem Start des Brühvorgangs wechselt der Zustand der Maschine unter **Measurements** > **State** (Messungen > Zustand) zu gelb. 
    
    Prüfen Sie das Konsolenprotokoll der simulierten Node.js-Kaffeemaschine auf Bestätigungsmeldungen. 

    ![Ausführen von Befehlen](../media/4-commands-brewing.png)

1. Klicken Sie auf **Ausführen**, um den Wartungsmodus festzulegen. Die Kaffeemaschine wird in den Wartungsmodus versetzt, sofern Sie sich *nicht* bereits im Wartungsmodus befindet.
    
    Prüfen Sie das Konsolenprotokoll der Kaffeemaschine auf Bestätigungsmeldungen. 

    > [!NOTE]
    > Die Kaffeemaschine bleibt im Wartungsmodus, bis Sie den Clientcode neu starten – genau wie in der Realität, wenn ein Techniker die Maschine offline schaltet, um notwendige Reparaturen durchzuführen, und sie anschließend wieder online schaltet.

    ![Ausführen von Befehlen](../media/4-commands-maintenance.png)

> [!IMPORTANT]
> Es empfiehlt sich, die Node.js-Anwendung nicht länger als etwa 60 Minuten auszuführen, um zu verhindern, dass Sie von der Anwendung unerwünschte Benachrichtigungen/E-Mails erhalten. Außerdem empfiehlt es sich, die Anwendung zu beenden, um das tägliche Nachrichtenkontingent nicht aufzubrauchen, wenn Sie nicht an dem Modul arbeiten.

## <a name="view-the-coffee-machine-in-the-dashboard"></a>Anzeigen der Kaffeemaschine auf dem Dashboard

1. Navigieren Sie zur Registerkarte **Dashboard** .

1. Klicken Sie auf **Vorlage bearbeiten**, um das Dashboard zu bearbeiten.

1. Wählen Sie aus dem seitlichen Menü **Liniendiagramm** aus.

1. Geben Sie unter **Configure Chart** (Diagramm konfigurieren) in das Feld **Titel** `Telemetry` ein. Zeigen Sie die Telemetriedaten mit diesem Diagramm an. 

1. Wählen Sie unter **Zeitbereich** die Option **Past 30 minutes** (Letzte 30 Minuten) aus. 

1. Klicken Sie im Bereich **Measures** auf das Sichtbarkeitssymbol jeweils rechts neben jeder Messung, um diese für unser Diagramm sichtbar zu machen. 

1. Klicken Sie auf **Speichern**, um die Konfiguration zu speichern und das Liniendiagramm anzuzeigen. 

    ![Anzeigen des Dashboards](../media/4-dashboard-a.png)

1. Klicken Sie im linken Menü auf **Settings and Properties** (Einstellungen und Eigenschaften), um den Bereich **Configure Device Details** (Gerätedetails konfigurieren) zu öffnen. 

1. Geben Sie in das Feld **Titel** `Device properties` ein.

1. Wählen Sie unter **Hinzufügen/Entfernen** die Optionen **Coffee Makers Max Temperature** (Höchste Kaffeemaschinentemperatur), **Coffee Makers Min Temperature** (Niedrigste Kaffeemaschinentemperatur), **Device Warranty Expired** (Gerätegarantie abgelaufen) und dann **OK** aus.

1. Klicken Sie auf **Speichern**, um das neue Panel *Geräteeigenschaften* im Dashboard zu erstellen. 

1. Klicken Sie noch einmal auf **Settings and Properties** (Einstellungen und Eigenschaften), und geben Sie `Optimal Temperature` als Titel ein. Wählen Sie unter **Hinzufügen/Entfernen** die Option **Optimal Temperature** (Optimale Temperatur) aus.

1. Klicken Sie auf **Speichern**, um Ihre Arbeit zu speichern und einen neuen Bereich im Dashboard anzuzeigen. 

1. Klicken Sie auf **Fertig**, um den Bearbeitungsmodus zu beenden und das neue Dashboard anzuzeigen. 