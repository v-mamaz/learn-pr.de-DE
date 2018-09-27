Bisher haben Sie Ihre Kaffeemaschine mit der Azure IoT Central-Anwendung verbunden und so den Austausch von Daten aktiviert, mit deren Hilfe Sie Ihre Kaffeemaschine überwachen und verwalten können. In dieser Einheit erstellen Sie Regeln, die Aktionen auslösen, wenn die Wassertemperatur der Kaffeemaschine außerhalb des normalen Bereichs liegt. 

## <a name="create-rules-in-iot-central-with-email-as-the-action"></a>Erstellen von Regeln in IoT Central mit E-Mail als Aktion

Azure IoT Central kann Benachrichtigungen mithilfe seiner nativen E-Mail-Funktion senden. In diesem Szenario wird, wenn die Kaffeemaschine außerhalb des optimalen Temperaturbereichs liegt und nicht durch die Garantie abgedeckt ist, eine E-Mail von IoT Central an die Wartungsabteilung des Kunden gesendet.

1. Navigieren Sie zur Seite **Regeln** für die Übungen in dieser Einheit, und wechseln Sie in den Bearbeitungsmodus, indem Sie rechts **Vorlage bearbeiten** auswählen. 
1. Klicken Sie auf **+ Neue Regel**, und anschließend auf **Telemetrie**. 

1. Geben Sie den Namen `Coffee Maker Water Too Cold (Expired)` ein.

1. Fügen Sie der Regel die folgenden Bedingungen hinzu, indem Sie rechts neben **Bedingungen** auf das Pluszeichen (**+**) und dann auf **Speichern** klicken:      
    - Die Wassertemperatur liegt unterhalb der niedrigsten Temperatur der Kaffeemaschine.
    - Abgelaufene Gerätegarantie entspricht 1.

    ![Verwenden der Regel](../media/5-flow-a.png)

1. Scrollen Sie im Bereich **Configure Telemetry Rule** (Telemetrieregel konfigurieren) nach unten, und wählen Sie **+** neben **Aktionen** aus. Wählen Sie dann **E-Mail** aus.

1. Geben Sie die E-Mail-Adresse ein, die Sie für die Anmeldung bei der IoT Central-Anwendung verwendet haben, und fügen Sie den Hinweis `Coffee maker's water is too cold. Maintenance is required.  Warranty has expired.` hinzu.

1. Klicken Sie auf **Speichern**. Ihre Regel wird auf der Seite **Regeln** aufgeführt.

Nun wiederholen Sie diese Schritte für den Fall, dass das Wasser zu heiß ist. 

1. Klicken Sie auf **+ Neue Regel**, und anschließend auf **Telemetrie**.

1. Hinzufügen einer neuen Regel namens `Coffee Maker Water Too Hot (Expired)`

1. Fügen Sie der Regel die folgenden Bedingungen hinzu, indem Sie rechts neben **Bedingungen** auf das Pluszeichen (**+**) und dann auf **Speichern** klicken:      
    - Die Wassertemperatur liegt oberhalb der höchsten Temperatur der Kaffeemaschine.
    - Abgelaufene Gerätegarantie entspricht 1.

1. Scrollen Sie im Bereich **Configure Telemetry Rule** (Telemetrieregel konfigurieren) nach unten, und wählen Sie **+** neben **Aktionen** aus. Wählen Sie dann **E-Mail** aus.

1. Geben Sie die E-Mail-Adresse ein, die Sie für die Anmeldung bei der IoT Central-Anwendung verwendet haben, und fügen Sie den Hinweis `Coffee maker's water is too cold. Maintenance is required.  Warranty has expired.` hinzu.

1. Klicken Sie auf **Speichern**. Ihre Regel wird auf der Seite **Regeln** aufgeführt.

Legen Sie zum Auslösen der Regel die optimale Temperatur in **Einstellungen** auf eine Temperatur außerhalb des Bereichs fest, den Sie unter **Eigenschaften** angegeben haben. Deaktivieren Sie die Regeln nach Abschluss der Überprüfung, damit Ihr Posteingang nicht mit E-Mails überflutet wird.