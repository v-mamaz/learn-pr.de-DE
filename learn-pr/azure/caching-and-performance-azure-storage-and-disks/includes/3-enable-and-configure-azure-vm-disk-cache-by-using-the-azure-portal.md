Sie können die Cacheeinstellungen für virtuelle Computer mit einem der folgenden Tools konfigurieren:

- Azure-Portal
- Resource Manager-Vorlagen
- Azure CLI
- Azure PowerShell

In der nächsten Übung werden wir im Portal einen virtuellen Computer erstellen und das Zwischenspeichern auf seinen Datenträgern konfigurieren. Dabei ist Folgendes zu bedenken. 

Wenn Sie einen neuen virtuellen Computer über das Azure-Portal bereitstellen, können Sie die standardmäßige Zwischenspeicherkonfiguration für den Betriebssystem-Datenträger vom Lese-/Schreibzugriff nicht ändern, bis der virtuelle Computer bereitgestellt wird.

Wenn Sie einem vorhandenen virtuellen Computer einen Datenträger für Daten hinzufügen, können Sie die Cacheoption konfigurieren, bevor der Datenträger für den virtuellen Computer bereitgestellt wird.

Durch Ändern der Cacheeinstellung eines Azure-Datenträgers wird der Zieldatenträger getrennt und erneut angefügt. Wenn es sich um den Betriebssystemdatenträger handelt, wird der virtuelle Computer neu gestartet. Beenden Sie alle Anwendungen und Dienste, die von dieser Unterbrechung betroffen sein könnten, bevor Sie die Cacheeinstellung des Datenträgers ändern.

Wir erstellen einen virtuellen Computer und ändern die Cacheeinstellungen über das Azure-Portal.
