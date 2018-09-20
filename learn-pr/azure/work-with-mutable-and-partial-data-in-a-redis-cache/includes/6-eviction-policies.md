Speicher ist die kritischste Ressource für den Azure Redis Cache, da es sich dabei um eine In-Memory-Datenbank handelt. Sie können auf Probleme stoßen, wenn Sie anfangen, Daten hinzuzufügen, die den verfügbaren Speicherplatz überschreiten. Der Azure Redis Cache unterstützt Entfernungsrichtlinien, die angeben, wie mit Daten umgegangen werden soll, wenn der Speicherplatz knapp wird.

Hier legen Sie eine Entfernungsrichtlinie fest, um anzugeben, wie mit Ihren Daten vorgegangen werden soll, wenn Sie den maximalen Speicherplatz überschreiten.

## <a name="what-is-an-eviction-policy"></a>Was ist eine Entfernungsrichtlinie?

Eine Entfernungsrichtlinie ist ein Plan, der bestimmt, wie Ihre Daten verwaltet werden sollen, wenn Sie den maximal verfügbaren Speicherplatz überschreiten. Mit einer Entfernungsrichtlinie können Sie den Azure Redis Cache beispielsweise anweisen, einen zufälligen Schlüssel zu löschen, um Platz für die neuen Daten zu schaffen, die eingefügt werden.

### <a name="types-of-eviction-policies"></a>Typen von Entfernungsrichtlinien

Der Azure Redis Cache stellt sechs verschiedene Entfernungsrichtlinien bereit. Alle diese Werte führen eine Aktion aus, wenn Sie versuchen, Daten einzufügen, obwohl nicht genügend Arbeitsspeicher vorhanden ist.

* **noeviction:** Keine Entfernungsrichtlinie. Gibt eine Fehlermeldung zurück, wenn Sie versuchen, Daten einzufügen.

* **allkeys-lru:** Entfernt den am längsten nicht verwendeten Schlüssel.

* **allkeys-random:** Entfernt einen zufälligen Schlüssel.

* **volatile-lru:** Entfernt den am längsten nicht verwendeten Schlüssel aller Schlüssel, für die ein Ablauf festgelegt ist.

* **volatile-ttl:** Entfernt den Schlüssel mit der kürzesten Gültigkeitsdauer basierend auf dem für ihn festgelegten Ablauf.

* **volatile-random:** Entfernt einen zufälligen Schlüssel, für den ein Ablauf festgelegt ist.

## <a name="how-to-set-an-eviction-policy"></a>Festlegen einer Entfernungsrichtlinie

Azure bietet ein einfaches Dropdownmenü zum Festlegen der Entfernungsrichtlinie für einen Azure Redis Cache. Wählen Sie **Erweiterte Einstellungen** aus, und verwenden Sie das **maxmemory-policy**-Dropdownmenü.

Da Speicher für einen Azure Redis Cache von entscheidender Bedeutung ist, werden Entfernungsrichtlinien unterstützt. Eine Entfernungsrichtlinie bestimmt, was mit vorhandenen Daten geschehen soll, wenn der Speicherplatz knapp ist und dennoch versucht wird, neue Daten einzufügen.