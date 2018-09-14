Hier fügen Sie eine Entfernungsrichtlinie für Azure Redis Cache.

## <a name="set-an-eviction-policy"></a>Legen Sie eine Entfernungsrichtlinie

Um eine Entfernungsrichtlinie in Azure zu festzulegen, verwenden wir einfach eine Dropdown-Menü im Azure-Portal an.

1. Öffnen Sie Ihren Azure Redis Cache im Azure-Portal an.

1. Wählen Sie die **Erweiterte Einstellungen** Blatt.

1. Verwenden der **Maxmemory-Policy** Dropdown-Menü, und wählen **Allkeys-random**.

1. Klicken Sie auf **Speichern**. 

An diesem Punkt: Wenn Sie nicht genügend Arbeitsspeicher ausgeführt, wird Azure Redis Cache löschen, um Platz für die neuen Daten stellen einen zufälligen Schlüssel aktivieren.