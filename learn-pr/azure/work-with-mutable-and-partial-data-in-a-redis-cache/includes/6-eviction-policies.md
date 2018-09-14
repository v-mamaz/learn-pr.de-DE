Speicher ist die wichtigste Ressource für Azure Redis Cache, da es sich um eine speicherinterne Datenbank handelt. Sie können Probleme auftreten, wenn Sie damit beginnen, Daten hinzufügen, die die Menge des verfügbaren Arbeitsspeichers überschreitet. Azure Redis Cache unterstützt entfernungsrichtlinien, die angeben, wie Daten behandelt werden sollen, wenn nicht Arbeitsspeicher genügend.

Legen Sie hier eine Entfernungsrichtlinie, um zu bestimmen, was Ihre Daten ausführen soll, wenn Sie die Höchstmenge an Arbeitsspeicher überschreiten.

## <a name="what-is-an-eviction-policy"></a>Was ist eine Entfernungsrichtlinie?

Eine Entfernungsrichtlinie ist einem Plan, der bestimmt, wie Ihre Daten verwaltet werden sollen, wenn Sie die Höchstmenge des verfügbaren Arbeitsspeichers überschreiten. Beispielsweise können über eine Entfernungsrichtlinie, Sie Azure Redis Cache löschen Sie einen zufälligen Schlüssel, um Platz für das Einfügen von neuen Daten zu schaffen teilen.

### <a name="types-of-eviction-policies"></a>Typen von entfernungsrichtlinien

Es gibt sechs verschiedene entfernungsrichtlinien, die von Azure Redis Cache bereitgestellt. Alle diese Werte ausführen eine Aktion, wenn Sie versuchen, Daten einfügen, wenn Sie nicht genügend Arbeitsspeicher sind.

* **"noeviction":** keine Entfernungsrichtlinie. Gibt eine Fehlermeldung zurück, wenn Sie versuchen, Daten einzufügen.

* **AllKeys-Lru:** entfernt den am längsten nicht verwendeten Schlüssel.

* **AllKeys-random:** einen zufälligen Schlüssel entfernt.

* **Volatile-Lru:** entfernt den am längsten nicht verwendeten Schlüssel aus der alle Schlüssel mit einem Satz Ablauf.

* **Volatile-Ttl:** entfernt, die der Schlüssel mit der kürzesten Zeit die Gültigkeitsdauer auf des Ablaufs Grundlage für ihn festgelegt.

* **Volatile-random:** entfernt einen zufälligen Schlüssel mit einer Ablaufzeit festlegen.

## <a name="how-to-set-an-eviction-policy"></a>Wie Sie eine Entfernungsrichtlinie festlegen

Azure bietet ein einfache Dropdown-Menü zum Festlegen von der Entfernungsrichtlinie für Azure Redis Cache. Wählen Sie **Erweiterte Einstellungen**, und verwenden Sie die **Maxmemory-Policy** Dropdown-Menü.

Da Speicher für Azure Redis Cache wichtig ist, ist Unterstützung für entfernungsrichtlinien. Eine Entfernungsrichtlinie bestimmt, was mit vorhandenen Daten ausgeführt werden soll, wenn Sie nicht genügend Arbeitsspeicher und versucht, neue Daten einfügen.