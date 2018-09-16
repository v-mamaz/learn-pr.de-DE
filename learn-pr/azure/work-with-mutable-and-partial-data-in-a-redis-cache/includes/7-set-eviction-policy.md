Hier fügen Sie dem Azure Redis Cache eine Entfernungsrichtlinie hinzu.

## <a name="set-an-eviction-policy"></a>Festlegen einer Entfernungsrichtlinie

Um eine Entfernungsrichtlinie in Azure festzulegen, verwenden wir einfach ein Dropdownmenü im Portal.

1. Öffnen Sie Ihren Redis Cache im Azure-Portal.

1. Wählen Sie das Blatt **Erweiterte Einstellungen** aus.

1. Verwenden Sie das **maxmemory-policy**-Dropdownmenü, und wählen Sie **allkeys-random** aus.

1. Klicken Sie auf **Speichern**. 

Wenn Ihnen nun der Speicherplatz ausgeht, wählt Redis einen zufälligen Schlüssel zum Löschen aus, um Platz für Ihre neuen Daten zu schaffen.