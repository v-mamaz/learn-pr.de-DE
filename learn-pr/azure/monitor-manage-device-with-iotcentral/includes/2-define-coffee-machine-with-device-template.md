In Azure IoT Central werden die Daten, die ein Gerät mit Ihrer Anwendung austauschen kann, in einer Gerätevorlage angegeben, mit der das Verhalten und die Funktion eines Geräts definiert werden (in diesem Fall einer Kaffeemaschine). Beim Erstellen einer Gerätevorlage wird aus der Vorlage ein simuliertes Gerät generiert. Das simulierte Gerät generiert Telemetriedaten, mit denen Sie das Verhalten Ihrer Anwendung testen können, bevor Sie eine Verbindung mit einem physischen Gerät herstellen. Später im nächsten Modul stellen Sie eine Verbindung mit einer generischen Node.js-Anwendung her, die für eine physische Kaffeemaschine steht. 

In diesem Modul erstellen Sie eine Gerätevorlage für eine Kaffeemaschine, mit der die folgenden Funktionen und Verhalten angegeben werden:
* Messungen 
    * Telemetrie: Luftfeuchtigkeit, Wassertemperatur
    * Zustand: Brühvorgang/Kein Brühvorgang, Tasse erkannt/Keine Tasse erkannt
* Einstellungen: Optimale Temperatur
* Eigenschaften: Höchste und niedrigste Kaffeemaschinentemperatur, Gerätegarantie abgelaufen
* Befehle: Wartungsmodus aktivieren, Brühvorgang starten


## <a name="create-a-device-template-for-the-coffee-maker"></a>Erstellen einer Gerätevorlage für die Kaffeemaschine
Eine Gerätevorlage, mit der das Verhalten und die Funktion eines Geräts definiert wird (in diesem Fall einer Kaffeemaschine).

1. Navigieren Sie zur Startseite, und wählen Sie die Option „Create Device Templates“ (Gerätevorlagen erstellen).
![Erstellen einer Gerätevorlage](../images/2-device-template-a1.png)

1. Geben Sie einen Namen für Ihre benutzerdefinierte Gerätevorlage ein. Geben Sie in diesem Modul beispielsweise „Connected Coffee Maker“ (Verbundene Kaffeemaschine) ein.
![Erstellen einer Gerätevorlage](../images/2-device-template-a2.png)
 
1. Sie haben eine leere Gerätevorlage für die Kaffeemaschine erstellt, mit der Sie das Verhalten und die Funktionen der Maschine definieren. 

## <a name="define-telemetry-measurement-temperature-and-humidity"></a>Definieren der Telemetriedatenmessung für Temperatur und Luftfeuchtigkeit
1.  Vergewissern Sie sich in der Gerätevorlage **Connected Coffee Maker**, dass Sie sich auf der Seite **Measurements** (Messungen) befinden, um die Telemetriedaten zu definieren. Jede Gerätevorlage, die Sie definieren, umfasst individuelle Seiten für Folgendes:
    * Angeben der Messungen, die vom Gerät gesendet werden (z.B. Telemetriedaten, Ereignisse und Zustände)
    * Definieren der Einstellungen zum Steuern des Geräts
    * Definieren der Eigenschaften zum Aufzeichnen von Geräteinformationen und der vom Gerät gesendeten Geräteeigenschaft
    * Definieren der Regeln für das Gerät
    * Anpassen des Gerätedashboards zum Anzeigen von relevanten Informationen zum Gerät 

1.  Klicken Sie auf **New Measurement** (Neue Messung), um die Messung für die Temperaturtelemetrie hinzuzufügen. Wählen Sie anschließend **Telemetry** (Telemetrie) als Typ für die Messung aus: ![Erstellen einer Gerätevorlage](../images/2-device-template-c.png)

1.  Jede Art von Telemetrie, die Sie für eine Gerätevorlage definieren, umfasst Konfigurationsoptionen, z.B.:
    * Anzeigeoptionen
    * Telemetriedetails
    * Simulationsparameter

    Verwenden Sie zum Konfigurieren der Telemetriedaten für die Temperatur und Luftfeuchtigkeit die Informationen aus der folgenden Tabelle:
    
    |Anzeigename|Feldname|Einheiten|Min|Max|Dezimalstellen|
    |---|---|---|---|---|---|
    |Wassertemperatur|waterTemperature|Celsius|90|98|1|
    |Luftfeuchtigkeit|airHumidity|%|20|100|0|
   
    Sie können auch eine Farbe für die Telemetrieanzeige auswählen. Wählen Sie **Speichern**, um die Telemetriedefinition zu speichern: ![Erstellen einer Gerätevorlage](../images/2-device-template-d.png)

    Geben Sie Feldnamen genau wie in der Tabelle angegeben in die Gerätevorlage ein. Wenn die Feldnamen nicht übereinstimmen, können die Telemetriedaten nicht in der Anwendung angezeigt werden. Gehen Sie beim Eingeben von Informationen zu Einstellungen und Eigenschaften genauso vor. 

## <a name="define-state-measurement-for-brewingnot-brewing-cup-detectedcup-not-detected"></a>Definieren der Zustandsmessung für Brühvorgang/Kein Brühvorgang, Tasse erkannt/Keine Tasse erkannt
Fügen Sie auf der Seite **Measurements** (Messungen) die folgenden Zustände hinzu, indem Sie die Option **New Measurement** (Neue Messung) wählen. Wählen Sie dann **Zustand** als Messungstyp aus:
    
|Anzeigename|Feldname|Wert 1|Anzeigename|Wert 2|Anzeigename|
|---|---|---|---|---|---|
|Brühvorgang|stateBrewing|true|Kein Brühvorgang|false|Kein Brühvorgang|
|Tasse erkannt|stateCupDetected|true|Keine Tasse erkannt|false|Keine Tasse erkannt|

![Erstellen einer Gerätevorlage](../images/2-device-template-f.png)

Beim Erstellen einer Gerätevorlage wird aus der Vorlage ein simuliertes Gerät generiert. Das simulierte Gerät generiert Telemetriedaten, mit denen Sie das Verhalten Ihrer Anwendung testen können, bevor Sie eine Verbindung mit einem physischen Gerät herstellen.
![Erstellen einer Gerätevorlage](../images/2-device-template-m.png)

## <a name="use-settings-to-set-the-optimal-temperature-of-the-coffee-machine"></a>Verwenden von „Einstellungen“ zum Festlegen der optimalen Temperatur der Kaffeemaschine
Navigieren Sie zu „Einstellungen“. Aktivieren Sie den **Entwurfsmodus**. Fügen Sie auf der Seite **Einstellungen** folgende Zahleneinstellungen hinzu:

|Anzeigename|Feldname|Einheiten|Dezimalstellen|Min|Max|Anfangswert|
|---|---|---|---|---|---|---|---|
|Optimale Temperatur|setTemperature|Celsius|1|92|99|95|

![Erstellen einer Gerätevorlage](../images/2-device-template-q.png)

## <a name="use-properties-to-store-warranty-info-and-water-temperature-range"></a>Verwenden von „Eigenschaften“ zum Speichern der Garantieinformationen und des Wassertemperaturbereichs
Fügen Sie auf der Seite mit den **Eigenschaften** die folgende **Number**-Eigenschaft hinzu, indem Sie zuerst den **Entwurfsmodus** aktivieren:
|Anzeigename|Feldname|Einheit|Dezimalstellen|Min|Max|Anfangswert
|---|---|---|---|---|---|---|
|Niedrigste Temperatur der Kaffeemaschine|propertyMinTemperature|Celsius|1|88|92|90|    
|Höchste Temperatur der Kaffeemaschine|propertyMaxTemperature|Celsius|1|96|99|98| 

![Erstellen einer Gerätevorlage](../images/2-device-template-n.png)

Fügen Sie auf der Seite mit den **Eigenschaften** die folgende **Geräteeigenschaft** hinzu:

|Anzeigename|Feldname|Datentyp|
|---|---|---|
|Gerätegarantie abgelaufen|propertyWarrantyExpired|number|
![Erstellen einer Gerätevorlage](../images/2-device-template-u.png)

> [!NOTE]
> Die Geräteeigenschaft wird von Ihrem Gerät gesendet (in diesem Fall von Ihrer Kaffeemaschine). Nachdem Sie für die Kaffeemaschine eine Verbindung mit Azure IoT Central hergestellt haben, wird die Geräteeigenschaft für die Garantie an die Anwendung gesendet und im Feld „Device Warranty Expired“ (Gerätegarantie abgelaufen) angezeigt. 

## <a name="use-commands-to-set-maintenance-mode-and-start-brewing"></a>Verwenden von „Commands“ (Befehle) zum Festlegen des Wartungsmodus und Starten des Brühvorgangs

Fügen Sie auf der Seite **Commands** (Befehle) die folgenden Befehle hinzu, indem Sie zuerst den **Entwurfsmodus** aktivieren.
|Anzeigename|Feldname|Eingabefelder|Datentyp|
|---|---|---|---|---|---|---|
|Wartungsmodus aktivieren|cmdSetMaintance|30|text| 
|Brühvorgang starten|cmdStartBrewing|30|text|

![Erstellen einer Gerätevorlage](../images/2-device-template-s.png)


## <a name="summary"></a>Zusammenfassung

In diesem Modul haben Sie einen neuen Gerätetyp (eine Kaffeemaschine) erstellt, indem Sie über die Gerätevorlage die Daten angegeben haben, die eine Kaffeemaschine mit Ihrer Anwendung austauschen kann. Sie haben die Telemetriedaten, z.B. Temperatur und Luftfeuchtigkeit, und den Zustand definiert, z.B. Brühvorgang/Kein Brühvorgang. Außerdem haben Sie das Verhalten und die Funktion der Kaffeemaschine definiert, indem Sie Einstellungen, Eigenschaften und Befehle konfiguriert haben. 

