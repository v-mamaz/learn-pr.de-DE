Nehmen Sie an, Sie arbeiten für ein Unternehmen, das in der Medizinforschung tätig ist, und Ihre Aufgabe ist die Verwaltung der lokalen Server. Auf den Servern, die Sie verwalten, wird die gesamte Infrastruktur des Unternehmens (von Webservern bis hin zu Datenbanken) ausgeführt. Die Hardware altert jedoch zunehmend und kann mit einigen der neuen Anwendungen für Datenanalysen, die darauf bereitgestellt werden, nicht mehr mithalten.

Sie könnten nun ein Upgrade für die Hardware durchführen. Dies ist jedoch aus mehreren Gründen nicht empfehlenswert:

1. Die Server stehen an verschiedenen Standorten und werden von sehr wenigen Mitarbeitern betreut. Das Upgrade soll sich auf unser Büro zuhause beschränken.

1. Die benutzerdefinierte Software für Datenanalysen wird im Unternehmen in verschiedenen Versionen und auf verschiedenen Windows- und Linux-Varianten ausgeführt. Die Konfigurationen können gelegentlich ungewöhnlich eingerichtet und schlecht nachvollziehbar sein. Bereitstellungen müssen vollständig getestet werden können. Außerdem müssen unterschiedliche Konfigurationen ausprobiert werden, um sicherzustellen, dass alles funktioniert, bevor die Arbeit übergeben wird.

1. Das Geschäft floriert, und das Unternehmen wächst schnell. Die Last auf den internen Servern, insbesondere auf den Datenbanken, wird wahrscheinlich weiter wachsen, sodass entweder zukunftssicher investiert oder ein Skalierungsplan erstellt werden muss, um dem Wachstum zu begegnen.

Sie möchten nun die Cloud nutzen, da Sie wissen möchten, ob damit Ihr Last- und Skalierungsproblem gelöst werden kann. Da Sie über verschiedene Server und benutzerdefinierte Software verfügen, können Sie einen Server nach dem anderen mit Azure Virtual Machines (VMs) zu Azure verschieben.

Eine Azure-VM ist eine von vielen bedarfsgesteuerten, skalierbaren Computerressourcen, die von Azure angeboten werden. Sie bieten Ihnen vollständige Kontrolle über die Konfiguration und unterstützen die Installation aller für Ihre Arbeit erforderlichen Programme. Sie müssen also keine Hardware erwerben, um Ihr Rechenzentrum zu skalieren oder zu erweitern. Außerdem bietet Azure zusätzliche Dienste, mit denen Sie Updates und Patches für das Betriebssystem überwachen, absichern und verwalten können.

Im Folgenden werden die Entscheidungen vor der Erstellung einer VM sowie die Optionen, Dienste und Erweiterungen zum Erstellen und Verwalten der VM besprochen.

## <a name="learning-objectives"></a>Lernziele

In diesem Modul wird Folgendes thematisiert:

- Erstellen einer Checkliste zum Erstellen von VMs
- Optionen zum Erstellen und Verwalten von VMs
- Zusätzliche, verfügbare Dienste zum Verwalten von VMs
