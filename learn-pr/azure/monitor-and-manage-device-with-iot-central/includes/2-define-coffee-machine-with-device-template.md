In Azure IoT Central werden die Daten, die ein Gerät mit Ihrer Anwendung austauschen kann, in einer Gerätevorlage angegeben, mit der das Verhalten und die Funktionen eines Geräts definiert werden (in diesem Fall einer Kaffeemaschine). Beim Erstellen einer Gerätevorlage wird aus der Vorlage ein simuliertes Gerät generiert.

Das simulierte Gerät generiert Telemetriedaten, mit denen Sie das Verhalten Ihrer Anwendung testen können, bevor eine Verbindung zwischen einem physischen und einem echten Gerät hergestellt wird. 

In dieser Einheit erstellen Sie eine Gerätevorlage für eine Kaffeemaschine, mit der die folgenden Funktionen und Verhalten angegeben werden:

### <a name="measurements"></a>Messungen

Messungen sind die Daten, die von Ihrem Gerät stammen. Sie können Ihrer Gerätevorlage mehrere Messungen hinzufügen, die den Funktionen Ihres Geräts entsprechen.

* **Telemetriemessungen:** Die numerischen Datenpunkte, die im Laufe der Zeit von Ihrem Gerät erfasst werden. Diese werden als kontinuierlicher Datenstrom dargestellt. In diesem Szenario betreffen die Telemetriemessungen die Luftfeuchtigkeit und Wassertemperatur. 

* **Zustandsmessungen:** Der Zustand des Geräts oder der zugehörigen Komponenten über einen bestimmten Zeitraum. In diesem Szenario legen Sie Zustände wie „Brühvorgang/Kein Brühvorgang“ und „Tasse erkannt/Keine Tasse erkannt“ fest.

### <a name="settings"></a>Einstellungen

Einstellungen dienen dazu, Konfigurationsdaten aus Ihrer Anwendung an ein Gerät zu senden. In diesem Szenario passen Sie die optimale Wassertemperatur in den Einstellungen an und senden sie an die Kaffeemaschine. Wenn die Einstellung aktualisiert wird, wird sie auf der Benutzeroberfläche als ausstehend markiert, bis das Gerät bestätigt hat, dass auf die Einstellungsänderung reagiert wurde.

### <a name="properties"></a>Eigenschaften

Die Gerätemetadaten, die dem Gerät zugeordnet sind. Es gibt zwei Typen von Eigenschaften.

* Sie nutzen *Anwendungseigenschaften* zum Erfassen von Geräteinformationen in Ihrer Anwendung. In diesem Szenario verwenden Sie Anwendungseigenschaften zum Festlegen des idealen Wassertemperaturbereichs für die Kaffeemaschine. Anwendungseigenschaften werden in der Anwendung gespeichert und nicht mit dem Gerät synchronisiert. 

* *Geräteeigenschaften* dienen dazu, einem Gerät das Senden von Eigenschaftswerten an Ihre Anwendung zu ermöglichen. Diese Eigenschaften können nur durch das Gerät geändert werden. In diesem Szenario konfigurieren Sie die Geräteeigenschaft namens „Device Warranty Expired“ (Gerätegarantie abgelaufen) in IoT Central. Das Feld „Device Warranty Expired“ (Gerätegarantie abgelaufen) bleibt leer, bis die Kaffeemaschine mit IoT Central verbunden wird. Nachdem die Verbindung hergestellt wurde, sendet die Kaffeemaschine den Garantiestatus an die Anwendung. 

### <a name="commands"></a>Befehle

Verwenden Sie Befehle, um Ihr Gerät aus Ihrer Anwendung remote zu verwalten. Sie können Befehle auf Ihrem Gerät direkt aus der Cloud ausführen, um das Gerät zu steuern. In diesem Szenario führen Sie die Befehle auf Ihrer Kaffeemaschine aus, um den Wartungsmodus zu aktivieren oder den Brühvorgang zu starten. 

## <a name="create-a-device-template-for-the-coffee-maker"></a>Erstellen einer Gerätevorlage für die Kaffeemaschine
Mit einer Gerätevorlage werden das Verhalten und die Funktionen eines Geräts definiert (in diesem Fall einer Kaffeemaschine).

1. Navigieren Sie zu der **Startseite** Ihrer Anwendung im Azure IoT Central-Portal, und klicken Sie auf **Create Device Templates** (Gerätevorlagen erstellen).

> [!TIP]
> Sie können zur Startseite navigieren, indem Sie im linken Menü auf das Symbol „Startseite“ klicken.

1. Geben Sie für Ihre benutzerdefinierte Gerätevorlage *Connected Coffee Maker* (Verbundene Kaffeemaschine) ein. 
 
1. Klicken Sie auf **Erstellen**. Sie haben eine leere Gerätevorlage für die Kaffeemaschine erstellt, mit der Sie das Verhalten und die Funktionen der Maschine definieren. 

## <a name="define-telemetry-measurements-of-temperature-and-humidity"></a>Definieren der Telemetriedatenmessung der Temperatur und Luftfeuchtigkeit
1. Vergewissern Sie sich in der Gerätevorlage **Connected Coffee Maker**, dass Sie sich auf der Seite **Measurements** (Messungen) befinden, wo die Telemetriedaten definiert werden. 

1. Klicken Sie auf **New Measurement** (Neue Messung), um die Messung für die Temperaturtelemetrie hinzuzufügen, und dann auf **+ New Measurement** (+ Neue Messung). Wählen Sie **Telemetry** (Telemetrie) als Messungstyp aus.

1. Jede Art von Telemetrie, die Sie für eine Gerätevorlage definieren, umfasst Konfigurationsoptionen, z.B.:
    * Anzeigeoptionen
    * Telemetriedetails
    * Simulationsparameter

    Verwenden Sie zum Konfigurieren der Telemetriedaten für die Temperatur und Luftfeuchtigkeit die Informationen aus der folgenden Tabelle. Beim Erstellen von Telemetrieelementen müssen Sie eine neue Messung hinzufügen, indem Sie für jedes Element in der Tabelle **+ New Measurement** (+ Neue Messung) auswählen.
    
    |Anzeigename|Feldname|Einheiten|Min|Max|Dezimalstellen|
    |---|---|---|---|---|---|
    |Wassertemperatur|waterTemperature|Celsius|86|100|1|
    |Luftfeuchtigkeit|airHumidity|%|20|100|0|
   
    Sie können auch eine Farbe für die Telemetrieanzeige auswählen. Klicken Sie auf **Speichern**, um die Telemetriedefinition zu speichern. Wenn Sie in der verbleibenden Einheit weitere Definitionen für Messungen, Einstellungen, Eigenschaften und Befehle erstellen, sollten Sie daran denken, zu speichern, wenn Sie fertig sind.  

    > [!NOTE]
    > Geben Sie Feldnamen genau wie in der Tabelle angegeben in die Gerätevorlage ein. Wenn die Feldnamen nicht mit den Eigenschaftennamen im entsprechenden Gerätecode übereinstimmen, können die Telemetriedaten nicht in der Anwendung angezeigt werden. Gehen Sie beim Eingeben von Informationen zu Einstellungen und Eigenschaften genauso vor.

    ![Erstellen einer Gerätevorlage](../media/2-device-template-a.png)

## <a name="define-state-measurement-for-brewingnot-brewing-and-cup-detectedcup-not-detected"></a>Definieren der Zustandsmessung für „Brühvorgang/Kein Brühvorgang“ und „Tasse erkannt/Keine Tasse erkannt“
Fügen Sie auf der Seite **Measurements** (Messungen) die folgenden Zustände hinzu, indem Sie auf **Vorlage bearbeiten** und dann auf die Option **+ New Measurement** klicken. Wählen Sie dann **Zustand** als Messungstyp aus:

Fügen Sie auf der Seite **Zustand** > **Brühvorgang** den Wert als TRUE hinzu. Fügen Sie den anderen Wert als FALSE mit dem optionalen Anzeigenamen „Kein Brühvorgang“ hinzu, indem Sie neben **Werte** auf **+** klicken. Achten Sie darauf, Ihre Änderungen mit einem Klick auf **Speichern** zu speichern.

   |Anzeigename|Feldname|Wert 1|Anzeigename 1|Wert 2|Anzeigename 2|
   |---|---|---|---|---|---|
   |Brühvorgang|stateBrewing|true|Brühvorgang|false|Kein Brühvorgang|
   |Tasse erkannt|stateCupDetected|true|Tasse erkannt|false|Keine Tasse erkannt|

> [!NOTE]
> Nachdem Sie die Telemetriedaten und den Zustand definiert haben, werden die simulierten Daten, die über die Gerätevorlage generiert werden, auf dem Gerätebildschirm angezeigt. Mit den simulierten Daten können Sie das Verhalten Ihrer Anwendung testen, bevor Sie ein physisches Gerät mit IoT Central verbinden. 

## <a name="set-the-optimal-temperature-of-the-coffee-machine"></a>Festlegen der optimalen Temperatur der Kaffeemaschine
Navigieren Sie zur Seite **Einstellungen** (Registerkarte neben **Measurements** (Messungen)). Klicken Sie auf **Vorlage bearbeiten**. Fügen Sie auf der Seite **Einstellungen** unter **Bibliothek** die folgende Einstellung für **Zahl** hinzu:

|Anzeigename|Feldname|Einheiten|Dezimalstellen|Min|Max|Anfangswert|
|---|---|---|---|---|---|---|---|
|Optimale Temperatur|setTemperature|Celsius|1|86|100|95|

## <a name="use-properties-to-store-warranty-info-and-water-temperature-range"></a>Verwenden von Eigenschaften zum Speichern der Garantieinformationen und des Wassertemperaturbereichs

Fügen Sie auf der Seite **Eigenschaften** die folgenden **Zahl**-Eigenschaften hinzu, indem Sie auf **Vorlage bearbeiten** klicken:

|Anzeigename|Feldname|Einheiten|Dezimalstellen|Min|Max|Anfangswert
|---|---|---|---|---|---|---|
|Coffee Maker's Min Temperature (Niedrigste Temperatur der Kaffeemaschine)|propertyMinTemperature|Celsius|1|88|92|90|
|Coffee Maker's Max Temperature (Höchste Temperatur der Kaffeemaschine)|propertyMaxTemperature|Celsius|1|96|99|98| 

Fügen Sie auf der Seite **Eigenschaften** die folgende **Geräteeigenschaft** hinzu:

   |Anzeigename|Feldname|Datentyp|
   |---|---|---|
   |Device Warranty Expired (Gerätegarantie abgelaufen)|propertyWarrantyExpired|number (Zahl)|

> [!NOTE]
> Die Geräteeigenschaft wird von Ihrem Gerät gesendet (in diesem Fall von Ihrer Kaffeemaschine). Nachdem Sie die Kaffeemaschine mit Azure IoT Central verbinden, wird die Geräteeigenschaft für die Garantie an die Anwendung gesendet und im Feld „Device Warranty Expired“ (Gerätegarantie abgelaufen) angezeigt. 

## <a name="use-commands-to-set-maintenance-mode-and-start-brewing"></a>Verwenden von Befehlen zum Festlegen des Wartungsmodus und Starten des Brühvorgangs

Fügen Sie auf der Seite **Befehle** die folgenden Befehle hinzu, indem Sie auf **Vorlage bearbeiten** klicken.

|Anzeigename|Feldname|Standardzeitlimit|Datentyp|
|---|---|---|---|---|---|---|
|Wartungsmodus aktivieren|cmdSetMaintenance|30|text| 
|Brühvorgang starten|cmdStartBrewing|30|text (Text)|