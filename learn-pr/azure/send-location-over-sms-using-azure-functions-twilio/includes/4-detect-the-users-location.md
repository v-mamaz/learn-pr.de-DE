Die App verfügt über eine Benutzeroberfläche und ein ViewModel. In dieser Einheit fügen Sie mit Xamarin.Essentials die Suche nach dem Standort zum ViewModel hinzu.

## <a name="enable-location-permissions"></a>Aktivieren von Standortberechtigungen

Alle mobilen Plattformen schützen Benutzerinformationen und Hardware, wie z.B. die Kamera, die Bildergalerie und den Standort des Benutzers. Bevor eine App auf den Standort des Benutzers zugreifen kann, muss der Benutzer diese Berechtigung erteilen. Diese Berechtigungen werden entweder implizit beim Installieren oder zur Laufzeit erteilt. Wenn Sie eine UWP-App im Store anzeigen, werden die von der App benötigten Berechtigungen aufgelistet. Wenn Sie die App installieren, erteilen Sie implizit die Berechtigung. Diese Berechtigungen werden in einer Manifestdatei der App konfiguriert.

1. Öffnen Sie im `ImHere.UWP`-App-Projekt die `Package.appxmanifest`-Datei.

1. Navigieren Sie zur Registerkarte **Funktionen**, und überprüfen Sie die Funktion *Standort*.

    ![Die Registerkarte „UWP-Funktionen“](../media/4-uwp-location-capability.png)

## <a name="query-for-the-users-location"></a>Abfragen des Benutzerstandorts

Es kann entweder der letzte bekannte oder der aktuelle Standort ermittelt werden. Die Ermittlung des aktuellen Standorts dauert möglicherweise länger, da das Gerät gegebenenfalls einen GPS-Link einrichten und warten muss, bis der genaue Standort abgerufen werden kann. Am schnellsten wird der dem Gerät zuletzt bekannte Standort ermittelt. Der zuletzt bekannte Speicherort ist möglicherweise ungenauer, kann allerdings schneller aufgerufen werden. Standorte werden in Längengrad und Breitengrad mit [Dezimalstellen](https://en.wikipedia.org/wiki/Decimal_degrees?azure-portal=true) und der Höhe des Geräts in Metern über dem Meeresspiegel angegeben.

1. Öffnen Sie die `MainViewModel`-Klasse im .NET Standard-Projekt `ImHere`.

1. Rufen Sie in der `SendLocation`-Methode die statische `GetLastKnownLocationAsync`-Methode in der `Geolocation`-Klasse im `Xamarin.Essentials`-Namespace auf. Sie müssen eine using-Anweisung für den `Xamarin.Essentials`-Namespace hinzufügen.

    ```csharp
    Location location = await Geolocation.GetLastKnownLocationAsync();
    ```

1. Aktualisieren Sie die `Message`-Eigenschaft mit dem Standort des Benutzers, falls dieser ermittelt werden konnte.

    ```csharp
    if (location != null)
    {
        Message = $"Location found: {location.Latitude}, {location.Longitude}.";
    }
    ```

    Im Folgenden finden Sie den vollständigen Code für diese Methode.
    
    ```csharp
    async Task SendLocation()
    {
        Location location = await Geolocation.GetLastKnownLocationAsync();
    
        if (location != null)
        {
            Message = $"Location found: {location.Latitude}, {location.Longitude}.";
        }
    }
    ```

1. Führen Sie die App aus, und klicken Sie auf die Schaltfläche **Standort senden**, um den Standort auf der Benutzeroberfläche anzuzeigen.

    ![Die ausgeführte App, die den Standort des Benutzers anzeigt](../media/4-running-app-showing-location.png)    

> [!NOTE]
> Diese App verwendet den letzten bekannten Standort. Wenn Sie in einer App mit Produktionsqualität den exakten aktuellen Standort mit einem Timeout erhalten möchten und dieser nicht ohne Zeitüberschreitung gefunden wird, nutzen Sie den zuletzt bekannten Standort. Weitere Informationen dazu erhalten Sie unter [Xamarin.Essentials Geolocation-Dokumentation](https://docs.microsoft.com/xamarin/essentials/geolocation?tabs=uwp#using-geolocation?azure-portal=true).
> 
> Diese App verfügt nicht über Möglichkeiten zur Fehlerbehandlung. In einer App mit Produktionsqualität müssen Sie alle Ausnahmen, die auftreten, behandeln, z.B. wenn der Standort nicht verfügbar war.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie gelernt, wie Sie Xamarin.Essentials verwenden, um den Standort des Benutzers zu erhalten. In der nächsten Einheit erstellen Sie eine Azure-Funktion, die als Back-End für die mobile App fungiert.