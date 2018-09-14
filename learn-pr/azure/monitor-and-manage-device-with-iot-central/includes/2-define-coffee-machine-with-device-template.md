In Azure IoT Central ist die Daten, die ein Gerät mit Ihrer Anwendung austauschen kann in einer Gerätevorlage für, die das Verhalten und die Funktionen eines Geräts definiert oder in diesem Fall einen Kaffee Computer angegeben. Beim Erstellen einer Gerätevorlage wird aus der Vorlage ein simuliertes Gerät generiert. Das simulierte Gerät generiert, Telemetriedaten, mit dem Sie das Verhalten Ihrer Anwendung testen, bevor ein physischer bzw. Real-Gerät verbunden ist. 

In dieser Einheit erstellen Sie eine Gerätevorlage für einen Kaffee-Computer, der angibt, die folgenden Funktionen und Verhaltensweisen:
* **Messungen**: die Daten, die von Ihrem Gerät stammen. Sie können Ihrer Gerätevorlage mehrere Messungen hinzufügen, die den Funktionen Ihres Geräts entsprechen.
    * Telemetrie-Messungen: numerischen Datenpunkte, die Ihr Gerät im Laufe der Zeit erfasst. Diese werden als kontinuierlicher Datenstrom dargestellt. In diesem Szenario die Messungen Telemetriedaten sind Luftfeuchtigkeit und Temperatur Wasser. 

    * Status von Messungen: den Status des Geräts oder dessen Komponenten über einen Zeitraum. In diesem Szenario legen Sie Status als "/" Not Brewing Brauereien, Cup erkannt/Cup nicht erkannt

* **Einstellungen**: Sie Einstellungen zum Senden von Konfigurationsdaten für ein Gerät aus Ihrer Anwendung verwenden. In diesem Szenario müssen Sie die optimale Wassertemperatur in den Einstellungen anpassen und an die Kaffeemaschine zu senden. Wenn die Einstellung aktualisiert wird, wird es als ausstehend markiert in der Benutzeroberfläche, bis das Gerät bestätigt, dass es die einstellungsänderung geantwortet hat.

* **Eigenschaften**: die Metadaten des Geräts, das mit dem Gerät zugeordnet ist. Es gibt zwei Typen von Eigenschaften.
    * Verwenden Sie *Anwendungseigenschaften* um Informationen zu Ihrem Gerät in Ihrer Anwendung aufzuzeichnen. In diesem Szenario verwenden Sie die Eigenschaften zum Festlegen des Bereichs der ideale Wasser Temperatur des Computers Kaffee. Eigenschaften werden in der Anwendung gespeichert und nicht mit dem Gerät synchronisiert. 

    * *Geräteeigenschaften* dienen dazu, einem Gerät das Senden von Eigenschaftswerten an Ihre Anwendung zu ermöglichen. Diese Eigenschaften können nur durch das Gerät geändert werden. In diesem Szenario konfigurieren Sie die Geräte-Eigenschaft, die in IoT Central namens Gerät Garantie ist abgelaufen. Das Feld "Gerät Gewährleistung abgelaufen" bleibt leer, bis die Kaffeemaschine mit IoT Central verbunden ist. Nachdem die Verbindung hergestellt ist, sendet der Kaffeemaschine den Garantiestatus an die Anwendung an. 

* **Befehle**: Sie verwenden Befehle aus, um Ihr Gerät aus Ihrer Anwendung remote zu verwalten. Sie können Befehle auf Ihrem Gerät direkt aus der Cloud ausführen, um die Geräte zu steuern. In diesem Szenario führen Sie die Befehle auf dem Computer "Coffee" legen Sie ihn auf Wartung, oder starten die Brauereien an. 

## <a name="create-a-device-template-for-the-coffee-maker"></a>Erstellen einer Gerätevorlage für die Kaffeemaschine
Eine Gerätevorlage definiert das Verhalten und die Funktionen eines Geräts oder in diesem Fall Kaffeemaschine.

1. Navigieren Sie zur Startseite, und wählen Sie **Gerätevorlagen erstellen**.

1. Geben Sie *Kaffeemaschine verbunden* für Ihre benutzerdefinierte Vorlage. 
 
1. Klicken Sie auf **Erstellen**. Sie haben eine leere Gerätevorlage für Kaffeemaschine erstellt, in dem Sie das Verhalten und die Funktionen des Rechners definieren. 

## <a name="define-telemetry-measurement-temperature-and-humidity"></a>Definieren der Telemetriedatenmessung für Temperatur und Luftfeuchtigkeit
1.  Vergewissern Sie sich in der Gerätevorlage **Connected Coffee Maker**, dass Sie sich auf der Seite **Measurements** (Messungen) befinden, um die Telemetriedaten zu definieren. 

1.  Wählen Sie zum Hinzufügen der Telemetriedaten temperaturmessung **+ neue Systemmessung**. Wählen Sie dann **Telemetriedaten** wie der Maßeinheitstyp.

1.  Jede Art von Telemetrie, die Sie für eine Gerätevorlage definieren, umfasst Konfigurationsoptionen, z.B.:
    * Anzeigeoptionen
    * Telemetriedetails
    * Simulationsparameter

    Verwenden Sie die Informationen in der folgenden Tabelle, um Ihre Telemetriedaten zu Temperatur und Luftfeuchtigkeit zu konfigurieren. Wenn telemetrieelemente erstellen zu können, müssen Sie eine neue systemmessung fügen **+ neue Systemmessung** für jedes Element in der Tabelle.
    
    |Anzeigename|Feldname|Einheiten|Min|Max|Dezimalstellen|
    |---|---|---|---|---|---|
    |Wassertemperatur|waterTemperature|Celsius|86|100|1|
    |Luftfeuchtigkeit|airHumidity|%|20|100|0|
   
    Sie können auch eine Farbe für die Telemetrieanzeige auswählen. Wählen Sie zum Speichern der Definition der Telemetriedaten **speichern**. Wenn Sie mehrere Definitionen für die Messungen, Einstellungen, Eigenschaften und Befehle in der restlichen Einheit erstellen, denken Sie daran, zu speichern, wenn Sie fertig sind.  
    
    ![Erstellen einer Gerätevorlage](../images/2-device-template-a.png)

    Geben Sie die Feldnamen genau wie in der Tabelle in die Geräte aus. Wenn die Feldnamen nicht mit die Eigenschaftennamen in der entsprechenden Gerätecode übereinstimmen, kann die Telemetriedaten in der Anwendung angezeigt werden. Gehen Sie beim Eingeben von Informationen zu Einstellungen und Eigenschaften genauso vor. 

## <a name="define-state-measurement-for-brewingnot-brewing-cup-detectedcup-not-detected"></a>Definieren der Zustandsmessung für Brühvorgang/Kein Brühvorgang, Tasse erkannt/Keine Tasse erkannt
Fügen Sie die folgenden Zustände in der **Messungen** Seite durch Auswahl **+ neue Systemmessung**. Wählen Sie dann **Zustand** als Messungstyp aus:
    
   |Anzeigename|Feldname|Wert 1|Anzeigename des 1|Wert 2|Anzeigename des 2|
   |---|---|---|---|---|---|
   |Brühvorgang|stateBrewing|true|Brühvorgang|false|Kein Brühvorgang|
   |Tasse erkannt|stateCupDetected|true|Tasse erkannt|false|Keine Tasse erkannt|


Auf dem Status > Brauereien Seite an, Sie fügen Sie den Wert "true". Fügen Sie den anderen Wert als "false", mit dem optionalen Anzeigenamen als Brauereien nicht durch Klicken auf **+** neben **Werte**.

> [!NOTE]
> Nach der Definition von Telemetrie- und Statusdaten über die Geräte aus, auf dem Bildschirm die generierten simulierten Daten angezeigt. Die simulierten Daten können Sie das Verhalten Ihrer Anwendung testen, bevor Sie ein physisches Gerät mit IoT Central verbinden. 

## <a name="use-settings-to-set-the-optimal-temperature-of-the-coffee-machine"></a>Verwenden von „Einstellungen“ zum Festlegen der optimalen Temperatur der Kaffeemaschine
Navigieren Sie zu der Seite Einstellungen auf der Registerkarte neben Messungen. Aktivieren Sie den **Entwurfsmodus**. Fügen Sie die folgenden **Anzahl** Einstellung unter **Bibliothek** auf die **Einstellungen** Seite:

|Anzeigename|Feldname|Einheiten|Dezimalstellen|Min|Max|Anfangswert|
|---|---|---|---|---|---|---|---|
|Optimale Temperatur|setTemperature|Celsius|1|86|100|95|

## <a name="use-properties-to-store-warranty-info-and-water-temperature-range"></a>Verwenden von „Eigenschaften“ zum Speichern der Garantieinformationen und des Wassertemperaturbereichs

Fügen Sie die folgenden **Anzahl** Eigenschaften für die **Eigenschaften** Seite nach der ersten Einschalten **Entwurfsmodus**:

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
|Legen Sie den Wartungsmodus|cmdSetMaintenance|30|text| 
|Brühvorgang starten|cmdStartBrewing|30|text|

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie einen neuer Gerätetyp, einen Kaffee-Computer mithilfe der Gerätevorlage erstellt. In der Gerätevorlage müssen Sie die Daten, die eine Kaffeemaschine austauschen kann mit der Anwendung angegeben. Sie haben die Telemetriedaten, z.B. Temperatur und Luftfeuchtigkeit, und den Zustand definiert, z.B. Brühvorgang/Kein Brühvorgang. Sie definiert das Verhalten und die Funktionen des Computers Kaffee weiter durch Konfigurieren von Einstellungen, Eigenschaften und Befehle. 

