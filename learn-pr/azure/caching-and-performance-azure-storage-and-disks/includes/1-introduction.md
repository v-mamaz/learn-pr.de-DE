Sie verwalten Ihre Unternehmensdatenbank-Infrastruktur von SQL Server-VMs in Azure ausgeführt wird. Die Zeit ist, und Sie müssen, um den Vorgang, bei der Verwaltung dennoch Kosten zentral hochzuskalieren. Ausführung einiger Datenbankvorgänge umfassen viele Lesevorgänge vorhandener Daten. Sind mit vielen Schreibvorgängen-Vorgänge, die reguläre Rechnung und die berichterstellung ausgeführt wird. Sie möchten, finden Sie eine Möglichkeit zur Optimierung Ihrer Infrastruktur, um alle Vorgangstypen zu behandeln. Entscheiden Sie vor der Investition in die Verbesserungen der Infrastruktur, VM-Datenträger-cachingoptionen zuerst untersuchen.

Das Zwischenspeichern ist eine gängige Methode zum Beschleunigen der computing-Ressourcen. Azure unterstützt verschiedene Typen des Zwischenspeicherns von Technologien zum Optimieren der Datenzugriff über die Azure-Landschaft, einschließlich der spezifischen Cacheoptionen für das Azure-Speicher und Datenträger, die von virtuellen Azure-Computern (VMs) verwendet.

Wir wollen alle Datenträger-cachingoptionen in Azure zu untersuchen und Verwalten von Datenträgercache mit dem Portal und PowerShell.

## <a name="learning-objectives"></a>Lernziele

In diesem Modul lernen Sie Folgendes:

- Beschreiben Sie die wichtigsten Überlegungen auf die datenträgerleistung in Azure (IOPS)
- Beschreiben Sie die Auswirkungen der Zwischenspeicherung auf die datenträgerleistung in Azure
- Aktivieren und Verwalten von Einstellungen des Caches mit dem Azure-portal
- Aktivieren und Verwalten von Einstellungen für Clientcache mit PowerShell