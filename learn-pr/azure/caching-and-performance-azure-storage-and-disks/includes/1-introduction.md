Sie verwalten Ihre Unternehmensdatenbank-Infrastruktur von SQL Server-VMs, die in Azure ausgeführt werden. Die Zeiten sind gut, und Sie müssen ihren Betrieb hochskalieren, aber dennoch dabei die Kosten kontrollieren. Bei manchen Datenbankvorgängen sind viele Lesevorgänge für vorhandene Daten erforderlich. Die regulären Rechnungs- und Berichterstellungsvorgänge sind sehr schreibintensiv. Sie möchten eine Möglichkeit zur Optimierung Ihrer Infrastruktur finden, die alle Vorgangstypen behandelt. Sie entscheiden, vor der Investition in die Verbesserungen der Infrastruktur zuerst VM-Datenträger-Zwischenspeicheroptionen zu untersuchen.

Das Zwischenspeichern ist eine gängige Methode zum Beschleunigen der Computingressourcen. Azure unterstützt eine Reihe von Technologien zum Zwischenspeichern, um den Datenzugriff in der Azure-Landschaft zu optimieren, einschließlich der spezifischen Cacheoptionen für den Azure-Speicher und Datenträger, die von virtuellen Azure Virtual Machines (VMs) verwendet werden.

Wir untersuchen alle verfügbaren Datenträger-Zwischenspeicheroptionen in Azure und erfahren, wie das Datenträgerzwischenspeichern mit dem Portal und PowerShell verwaltet wird.

## <a name="learning-objectives"></a>Lernziele

In diesem Modul lernen Sie Folgendes:

- Beschreiben der wichtigsten Überlegungen zur Datenträgerleistung in Azure
- Beschreiben der Auswirkungen des Zwischenspeicherns auf die Datenträgerleistung in Azure
- Aktivieren und Verwalten von Cacheeinstellungen mit dem Azure-Portal
- Aktivieren und Verwalten von Cacheeinstellungen mit PowerShell

## <a name="prerequisites"></a>Voraussetzungen  

Keine