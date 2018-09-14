Sie können die cacheeinstellungen für virtuelle Computer mit einem der folgenden Tools konfigurieren:

- Azure-Portal
- Resource Manager-Vorlagen
- Azure CLI
- Azure PowerShell

In der nächsten Übung werden wir Sie über das Portal zum Erstellen eines virtuellen Computers, und konfigurieren die Zwischenspeicherung für die Datenträger. Hier ist einiges zu bedenken.

Wenn Sie einen neuen virtuellen Computer über das Azure-Portal bereitstellen, können Sie nicht ändern das Standardverhalten beim Zwischenspeichern Konfiguration für den Betriebssystem-Datenträger von Lese-/Schreibzugriff, bis der virtuelle Computer bereitgestellt wird.

Wenn Sie einem vorhandenen virtuellen Computer einen Datenträger für Daten hinzufügen, können Sie die Cache-Option konfigurieren, bevor der Datenträger mit dem virtuellen Computer bereitgestellt wird.

Durch Ändern der cacheeinstellung für eine Azure-Datenträger wird getrennt und erneut angefügt wird der Zieldatenträger. Wenn es sich um die Betriebssystem-Datenträger handelt, wird der virtuelle Computer neu gestartet. Beenden Sie alle Anwendungen und Dienste, die von dieser Unterbrechung betroffen sein könnten, bevor Sie die Cacheeinstellung des Datenträgers ändern.

Erstellen eines virtuellen Computers, und ändern Sie die cacheeinstellungen, die über das Azure-Portal.
