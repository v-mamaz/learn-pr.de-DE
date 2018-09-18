In Azure IoT Central werden die Daten, die ein Gerät mit Ihrer Anwendung austauschen kann, in einer Gerätevorlage angegeben, mit der das Verhalten und die Funktionen eines Geräts definiert werden (in diesem Fall einer Kaffeemaschine). Beim Erstellen einer Gerätevorlage wird aus der Vorlage ein simuliertes Gerät generiert. Das simulierte Gerät generiert Telemetriedaten, mit denen Sie das Verhalten Ihrer Anwendung testen können, bevor eine Verbindung zwischen einem physischen und einem echten Gerät hergestellt wird. 

In dieser Einheit erstellen Sie eine Gerätevorlage für eine Kaffeemaschine, mit der die folgenden Funktionen und Verhalten angegeben werden:
* **Messungen**: Die Daten, die von Ihrem Gerät stammen. Sie können Ihrer Gerätevorlage mehrere Messungen hinzufügen, die den Funktionen Ihres Geräts entsprechen.
    * Telemetriemessungen: Die numerischen Datenpunkte, die im Laufe der Zeit von Ihrem Gerät erfasst werden. Diese werden als kontinuierlicher Datenstrom dargestellt. In diesem Szenario betreffen die Telemetriemessungen die Luftfeuchtigkeit und Wassertemperatur. 

    * Zustandsmessungen: Der Zustand des Geräts oder der zugehörigen Komponenten über einen bestimmten Zeitraum. In diesem Szenario legen Sie die Zustände „Brühvorgang“/„Kein Brühvorgang“, „Tasse erkannt“/„Keine Tasse erkannt“ fest.

* **Einstellungen**: Sie verwenden Einstellungen, um Konfigurationsdaten aus Ihrer Anwendung an ein Gerät zu senden. In diesem Szenario passen Sie die optimale Wassertemperatur in den Einstellungen an und senden sie an die Kaffeemaschine. Wenn die Einstellung aktualisiert wird, wird sie auf der Benutzeroberfläche als ausstehend markiert, bis das Gerät bestätigt hat, dass auf die Einstellungsänderung reagiert wurde.

* **Eigenschaften**: Die Gerätemetadaten, die dem Gerät zugeordnet sind. Es gibt zwei Typen von Eigenschaften.
    * Sie nutzen *Anwendungseigenschaften* zum Erfassen von Geräteinformationen in Ihrer Anwendung. In diesem Szenario verwenden Sie Anwendungseigenschaften zum Festlegen des idealen Wassertemperaturbereichs für die Kaffeemaschine. Anwendungseigenschaften werden in der Anwendung gespeichert und nicht mit dem Gerät synchronisiert. 

    * *Geräteeigenschaften* dienen dazu, einem Gerät das Senden von Eigenschaftswerten an Ihre Anwendung zu ermöglichen. Diese Eigenschaften können nur durch das Gerät geändert werden. In diesem Szenario konfigurieren Sie die Geräteeigenschaft mit dem Namen „Device Warranty Expired“ (Gerätegarantie abgelaufen) in IoT Central. Das Feld „Device Warranty Expired“ (Gerätegarantie abgelaufen) bleibt leer, bis die Kaffeemaschine mit IoT Central verbunden wird. Nachdem die Verbindung hergestellt wurde, sendet die Kaffeemaschine den Garantiestatus an die Anwendung. 

* **Befehle**: Verwenden Sie Befehle, um Ihr Gerät über Ihre Anwendung remote zu verwalten. Sie können Befehle auf Ihrem Gerät direkt aus der Cloud ausführen, um die Geräte zu steuern. In diesem Szenario führen Sie die Befehle auf Ihrer Kaffeemaschine aus, um den Wartungsmodus zu aktivieren oder den Brühvorgang zu starten. 

## <a name="create-a-device-template-for-the-coffee-maker"></a>Erstellen einer Gerätevorlage für die Kaffeemaschine
Mit einer Gerätevorlage werden das Verhalten und die Funktionen eines Geräts definiert (in diesem Fall einer Kaffeemaschine).

1. Navigieren Sie zur Startseite, und wählen Sie die Option **Create Device Templates** (Gerätevorlagen erstellen).

1. Geben Sie für Ihre benutzerdefinierte Gerätevorlage *Connected Coffee Maker* (Verbundene Kaffeemaschine) ein. 
 
1. Klicken Sie auf **Erstellen**. Sie haben eine leere Gerätevorlage für die Kaffeemaschine erstellt, mit der Sie das Verhalten und die Funktionen der Maschine definieren. 

## <a name="define-telemetry-measurement-temperature-and-humidity"></a>Definieren der Telemetriedatenmessung für Temperatur und Luftfeuchtigkeit
1.  Vergewissern Sie sich in der Gerätevorlage **Connected Coffee Maker**, dass Sie sich auf der Seite **Measurements** (Messungen) befinden, um die Telemetriedaten zu definieren. 

1.  Klicken Sie auf **+ New Measurement** (+ Neue Messung), um die Messung für die Temperaturtelemetrie hinzuzufügen. Wählen Sie **Telemetry** (Telemetrie) als Messungstyp aus.

1.  Jede Art von Telemetrie, die Sie für eine Gerätevorlage definieren, umfasst Konfigurationsoptionen, z.B.:
    * Anzeigeoptionen
    * Telemetriedetails
    * Simulationsparameter

    Verwenden Sie zum Konfigurieren der Telemetriedaten für die Temperatur und Luftfeuchtigkeit die Informationen aus der folgenden Tabelle. Beim Erstellen von Telemetrieelementen müssen Sie eine neue Messung hinzufügen, indem Sie für jedes Element in der Tabelle **+ New Measurement** (+ Neue Messung) wählen.
    
    |Anzeigename|Feldname|Einheiten|Min|Max|Dezimalstellen|
    |---|---|---|---|---|---|
    |Wassertemperatur|waterTemperature|Celsius|86|100|1|
    |Luftfeuchtigkeit|airHumidity|%|20|100|0|
   
    Sie können auch eine Farbe für die Telemetrieanzeige auswählen. Klicken Sie auf **Speichern**, um die Telemetriedefinition zu speichern. Wenn Sie in der verbleibenden Einheit weitere Definitionen für Messungen, Einstellungen und Befehle erstellen, sollten Sie daran denken zu speichern, wenn Sie fertig sind.  
    
    ![Erstellen einer Gerätevorlage](../images/2-device-template-a.png)

    Geben Sie Feldnamen genau wie in der Tabelle angegeben in die Gerätevorlage ein. Wenn die Feldnamen nicht mit den Eigenschaftennamen im entsprechenden Gerätecode übereinstimmen, können die Telemetriedaten nicht in der Anwendung angezeigt werden. Gehen Sie beim Eingeben von Informationen zu Einstellungen und Eigenschaften genauso vor. 

## <a name="define-state-measurement-for-brewingnot-brewing-cup-detectedcup-not-detected"></a>Definieren der Zustandsmessung für Brühvorgang/Kein Brühvorgang, Tasse erkannt/Keine Tasse erkannt
Fügen Sie auf der Seite **Measurements** (Messungen) die folgenden Zustände hinzu, indem Sie die Option **+ New Measurement** (+ Neue Messung) wählen. Wählen Sie dann **State** (Zustand) als Messungstyp aus:
    
   |Anzeigename|Feldname|Wert 1|Anzeigename 1|Wert 2|Anzeigename 2|
   |---|---|---|---|---|---|
   |Brühvorgang|stateBrewing|true|Brühvorgang|false|Kein Brühvorgang|
   |Tasse erkannt|stateCupDetected|true|Tasse erkannt|false|Keine Tasse erkannt|


Auf der Seite „Zustand“ > „Brühvorgang“ fügen Sie den Wert als „true“ hinzu. Fügen Sie den anderen Wert als „false“ mit dem optionalen Anzeigenamen „Kein Brühvorgang“ hinzu, indem Sie neben **Werte** auf **+** klicken.

> [!NOTE]
> Nachdem Sie die Telemetriedaten und den Zustand definiert haben, werden die simulierten Daten, die über die Gerätevorlage generiert werden, auf dem Gerätebildschirm angezeigt. Mit den simulierten Daten können Sie das Verhalten Ihrer Anwendung testen, bevor Sie für ein physisches Gerät eine Verbindung mit IoT Central herstellen. 

## <a name="use-settings-to-set-the-optimal-temperature-of-the-coffee-machine"></a>Verwenden von „Einstellungen“ zum Festlegen der optimalen Temperatur der Kaffeemaschine
Navigieren Sie zur Seite „Einstellungen“ (Registerkarte neben „Messungen“). Aktivieren Sie den **Entwurfsmodus**. Fügen Sie auf der Seite **Einstellungen** unter **Bibliothek** die folgende Einstellung für **number** (Zahl) hinzu:

|Anzeigename|Feldname|Einheiten|Dezimalstellen|Min|Max|Anfangswert|
|---|---|---|---|---|---|---|---|
|Optimale Temperatur|setTemperature|Celsius|1|86|100|95|

## <a name="use-properties-to-store-warranty-info-and-water-temperature-range"></a>Verwenden von „Eigenschaften“ zum Speichern der Garantieinformationen und des Wassertemperaturbereichs

Fügen Sie auf der Seite mit den **Eigenschaften** die folgenden **Number**-Eigenschaften hinzu, indem Sie zuerst den **Entwurfsmodus** aktivieren:

|Anzeigename|Feldname|Einheiten|Dezimalstellen|Min|Max|Anfangswert
|---|---|---|---|---|---|---|
|Niedrigste Temperatur der Kaffeemaschine|propertyMinTemperature|Celsius|1|88|92|90|
|Höchste Temperatur der Kaffeemaschine|propertyMaxTemperature|Celsius|1|96|99|98| 

Fügen Sie auf der Seite mit den **Eigenschaften** die folgende **Geräteeigenschaft** hinzu:

   |Anzeigename|Feldname|Datentyp|
   |---|---|---|
   |Gerätegarantie abgelaufen|propertyWarrantyExpired|number|

> [!NOTE]
> Die Geräteeigenschaft wird von Ihrem Gerät gesendet (in diesem Fall von Ihrer Kaffeemaschine). Nachdem Sie für die Kaffeemaschine eine Verbindung mit Azure IoT Central hergestellt haben, wird die Geräteeigenschaft für die Garantie an die Anwendung gesendet und im Feld „Device Warranty Expired“ (Gerätegarantie abgelaufen) angezeigt. 

## <a name="use-commands-to-set-maintenance-mode-and-start-brewing"></a>Verwenden von „Commands“ (Befehle) zum Festlegen des Wartungsmodus und Starten des Brühvorgangs

Fügen Sie auf der Seite **Commands** (Befehle) die folgenden Befehle hinzu, indem Sie zuerst den **Entwurfsmodus** aktivieren.

|Anzeigename|Feldname|Standardzeitlimit|Datentyp|
|---|---|---|---|---|---|---|
|Wartungsmodus aktivieren|cmdSetMaintenance|30|text| 
|Brühvorgang starten|cmdStartBrewing|30|text|

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie mit der Gerätevorlage einen neuen Gerätetyp (Kaffeemaschine) erstellt. In der Gerätevorlage haben Sie die Daten angegeben, die von einer Kaffeemaschine mit Ihrer Anwendung ausgetauscht werden können. Sie haben die Telemetriedaten, z.B. Temperatur und Luftfeuchtigkeit, und den Zustand definiert, z.B. Brühvorgang/Kein Brühvorgang. Außerdem haben Sie das Verhalten und die Funktionen der Kaffeemaschine definiert, indem Sie Einstellungen, Eigenschaften und Befehle konfiguriert haben. 

