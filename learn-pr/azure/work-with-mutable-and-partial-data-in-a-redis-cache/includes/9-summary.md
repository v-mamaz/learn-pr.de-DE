Im Modul haben wir gesehen, wie Redis in vielerlei Hinsicht dazu beitragen kann, die Leistung unserer Anwendung zu verbessern. Wir haben zuerst gesehen, wie Transaktionen verwendet werden können, um sicherzustellen, dass mehrere Vorgänge zusammen ohne Unterbrechung aufgerufen werden. Wir haben dann gesehen, wie der Datenablauf verwendet wird, um Daten zu löschen, die nicht mehr verwendet werden. Allerdings können bei der Verwendung eines Caches noch immer gelegentlich Speicherprobleme auftreten, und wir haben erläutert, wie Entfernungsrichtlinien verwendet werden können, um Platz für neue Daten zu schaffen. Schließlich haben wir uns das cachefremde Muster angesehen, um sicherzustellen, dass Ihre häufig verwendeten Daten in einem Cache gespeichert sind, um die für den Abruf benötigte Zeit zu verkürzen.

<!-- Cleanup sandbox -->
[!include[](../../../includes/azure-sandbox-cleanup.md)]