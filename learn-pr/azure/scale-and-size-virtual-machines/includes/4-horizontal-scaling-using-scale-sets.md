Sie erhalten die Ressourcen benötigten mit einen großen virtuellen Computer oder mehrere kleine virtuelle Computer mit einem Load Balancer auf um Anforderungen zwischen den virtuellen Computern zu verteilen.

Der VM-Pool hat es sich um den schön Vorteil, dass Sie hinzufügen oder Entfernen von virtuellen Computern schnell bei wechselnden können. Im Szenario Unternehmen Spielzeug wäre diese Strategie nützlich, um unerwartete Spitzen Nachfrage zu bewältigen. Sie können VMs zum Pool hinzufügen, bei Bedarf erhöht, und entfernen Sie sie bei Bedarf in den Normalzustand zurückgegeben. Der Pool bietet auch Redundanz. Wenn ein virtueller Computer ein Fehler auftritt, können die anderen weiterhin zur Verarbeitung von Anforderungen ohne Unterbrechung des Diensts.

In diesem Abschnitt sehen Sie, wie zum Bereitstellen mehrerer virtueller Computer mithilfe von skalierungsgruppen und automatisch hinzufügen und Entfernen von Instanzen als Reaktion auf bei Bedarf ändern. 

## <a name="what-is-horizontal-scaling"></a>Was ist die horizontale Skalierung?

*Die horizontale Skalierung* ist der Prozess des Hinzufügens und Entfernens von virtuellen Computern aus einem Pool zum Anpassen der Anzahl der verfügbaren Ressourcen. Hinzufügen von Computern wird aufgerufen, _horizontales hochskalieren_, und Entfernen von Computern, heißt _Herunterskalieren_. Lösungen, die die horizontale Skalierung verwenden, enthalten einen Lastenausgleich oder das Gateway, um Anforderungen für den virtuellen Computer im Pool zu verteilen. Die folgende Abbildung zeigt ein Beispiel für die Anzahl der Instanzen virtueller Computer ändern.

![Eine Abbildung mit Horizontales Skalieren von Ressourcen, behandeln bei Bedarf und Skalieren von Daten in die Ressourcen, um Kosten zu senken.](../media/4-ScaleInOut.png)

Dieses Verfahren funktioniert am besten für Anwendungen, die auf mehreren Servern ausgeführt werden können. Beispielsweise können Sie den Webserver und die Webseiten auf mehreren virtuellen Computern duplizieren, und werden alle bieten die gleiche Antwort unabhängig davon, welcher Server die Anforderung empfängt. Auf der anderen Seite ist ein virtuellen Computer, die Ihre Back-End-Datenbank ausgeführt wird kein idealer Kandidat da Ausführen mehrerer Kopien der Datenbank einen gewissen Aufwand Kopien synchron zu halten.

## <a name="what-is-a-scale-set"></a>Was ist eine Skalierungsgruppe?

Ein *Skalierungsgruppe* ist ein Pool mit identischer virtueller Computer, einem Lastenausgleich oder das Gateway, um Anforderungen zu verteilen und einen optionalen Satz von Regeln, die steuern, wann VMs hinzugefügt oder aus dem Pool entfernt werden. Hier bedeutet "identischen", dass jede VM in der Gruppe mit dem gleichen Image erstellt und die gleiche Größe hat wird.

Sie können einige in der Konfiguration eines neuen virtuellen Computers mit der Software, die Sie benötigen. Sie können mit einem vordefinierten Image für das Basisbetriebssystem starten und dann Skripts zu installieren, oder kopieren Sie Dateien automatisch nach dem Einrichten des Betriebssystems. Alternativ können Sie ein benutzerdefiniertes VM-Image mit dem Betriebssystem und Ihre Anwendungssoftware bereits installiert erstellen.

## <a name="how-to-distribute-requests"></a>Wie Sie die Verteilung von Anforderungen

Sie können entweder ein Lastenausgleichsmodul oder ein Application Gateway verwenden, Anforderungen an die VM-Instanzen in einer Skalierungsgruppe zu verteilen.

Ein Azure Load Balancer arbeitet auf den OSI-Schicht 4 (TCP und UDP) und leitet den Datenverkehr basierend auf Quell-IP-Adresse und Port kombiniert mit dem Ziel-IP-Adresse und Port. Es kann es sich um Affinität, bereitstellen, in denen Datenverkehr von der gleichen IP-Quelladresse, auf dem gleichen Zielserver weitergeleitet wird, um Konsistenz für eine Clientsitzung zu ermöglichen. Der Load Balancer verfügt auch über einen Integritätsdienst Testmechanismus, der bestimmt, die Verfügbarkeit von Server-Instanzen. Wenn Sie ein virtuellen Computer auf den Integritätstest reagiert, wird der Load Balancer routing keine neuen Verbindungen auf diesen Computer vermeiden.

Ein Application Gateway wird während des OSI-Schicht 7 (Anwendungsschicht). Beispielsweise wenn Ihre VMs auf einen Webserver ausgeführt werden, können klicken Sie dann das Gateway die angeforderte URL routing ausführen. Dies bedeutet, Sie könnten Weiterleiten von Anforderungen mit `*/customers*` in der URL zu einem Pool von Servern und -Anforderungen mit `*/partners*` in der URL in einen anderen Pool. Das Application Gateway bieten auch HTTP auf HTTPS-Umleitung, Secure Sockets Layer (SSL)-Beendigung an die Verarbeitung auf die virtuellen Computer für die Verschlüsselung und einer Web Application Firewall (WAF), die Regeln verwendet, um bekannte Web erkennen reduzieren nutzt und verhindern, dass diese Anforderungen der Webserver erreicht.

## <a name="what-is-autoscaling"></a>Was ist für die automatische Skalierung?

_Für die automatische Skalierung_ basiert der Prozess automatisch horizontale hoch- oder Herunterskalieren auf einen Satz von Regeln. Die Regeln können durch Computer Last oder Zeitplan ausgelöst werden. Die folgende Abbildung zeigt, wie die Autoscale-Funktion-Instanzen, um die Last zu bewältigen verwaltet.

![Eine Abbildung zeigt, wie für die automatische Skalierung überwacht die CPU-Auslastung aus einem Pool von virtuellen Maschinen und zusätzlich Instanzen aus, wenn die CPU-Auslastung über dem Schwellenwert liegt.](../media/4-autoscale.png)

Um die automatische Skalierung für eine Skalierungsgruppe zu aktivieren, müssen Sie ein Profil für die automatische Skalierung erstellen. Das Profil definiert die minimale und maximale Anzahl von VM-Instanzen für die Gruppe und die Skalierung Regeln. Regeln zur automatischen Skalierung werden die folgenden Elemente aufweisen:

* Metrikquelle - die Quelle der Informationen oder Daten, die die Regel für die automatische Skalierung ausgelöst wird. Es gibt vier Optionen:
  * *Aktuelle Skalierungsgruppe* bietet hostbasierte Metriken, die keine zusätzliche Agents erforderlich sind.
  * *Speicherkonto*: Die Azure-diagnoseerweiterung schreibt Leistungsmetriken in Azure Storage. Diese Metriken werden verwendet, um Regeln zur automatischen Skalierung auszulösen.
  * *Azure Service Bus-Warteschlange* festlegbaren anwendungsbasierte oder andere Azure Service Bus-Nachrichten an die automatische Skalierung auszulösen.
  * *Azure Application Insights* verwendet ein instrumentierungspaket, die in der Anwendung auf die Skalierungsgruppe, die zum Streamen von metrischen Daten direkt aus der Anwendung installiert werden muss.
* Regelkriterien - ist dies die jeweilige Metrik zu verwenden, um eine Regel für die automatische Skalierung auszulösen. Wenn Sie hostbasierte Metriken verwenden, kann dies Aspekten wie z. B. CPU-Auslastung, die Menge an Netzwerkdatenverkehr, Datenträgervorgänge oder CPU-Guthaben enthalten. Sie können z. B. konfigurieren, dass eine Regel zum horizontalen hochskalieren, wenn der Datenträger-Schreibvorgänge pro Sekunde ein Schwellenwert überschritten. Mit dem Azure-diagnoseerweiterung oder Application Insights können Sie alle verfügbaren Measures verwenden, um die Regel jedoch erfordert die Konfiguration von den entsprechenden Agent.
* Aggregationstyp: Dies gibt an, wie Sie die metrischen Daten messen möchten und eine der folgenden Optionen:
  * Durchschnitt
  * Minimum
  * Maximum
  * Gesamt
  * Last (Letzter)
  * Count
* Operator - Operator gibt an, wie eine Metrik einen festgelegten Schwellenwert zum Auslösen der Aktion Regeln unterschiedlich sein muss. Dies ist besonders wichtig, beim identifizieren, ob die Regel hoch- oder Herunterskalieren wird. Operatoren sind möglich:
  * Größer als
  * Größer oder gleich
  * Kleiner als 
  * Kleiner als oder gleich
  * Ist gleich
  * Ungleich
* Aktion: Dadurch wird bestimmt, wie die Anzahl der Instanzen ändern wird, wenn die Regel ausgelöst wird. Die folgenden Aktionen sind verfügbar:
  * *Anzahl erhöhen um* eine feste Anzahl von virtuellen Computern.
  * *Prozentsatz erhöhen um* einen Prozentsatz der vorhandenen Instanzen.
  * *Anzahl erhöhen auf* eine bestimmte Anzahl von virtuellen Computern.
  * *Anzahl verringern um* eine feste Anzahl von virtuellen Computern.
  * *Prozentsatz verringern um* einen Prozentsatz der vorhandenen Instanzen.
  * *Anzahl verringern auf* eine bestimmte Anzahl von virtuellen Computern.

Sie können Regeln zur automatischen Skalierung, die auslösen, auch nach einem Zeitplan erstellen. Sie können z. B. eine Regel definieren, die horizontal hochskaliert, am Morgen, wenn Sie wissen, dass es sich bei Bedarf hoch ist, und klicken Sie dann nach der Mittagspause, wenn die Nachfrage in der Regel sinkt, horizontal herunterskaliert.

## <a name="how-to-create-a-scale-set"></a>Gewusst wie: Erstellen einer Skalierungsgruppe

Sie können eine Skalierungsgruppe mit Azure-Portal, Azure PowerShell oder der Azure-Befehlszeilenschnittstelle erstellen.

### <a name="portal"></a>Portal

Wenn Sie im Azure-Portal verwenden, um die Skalierungsgruppe zu erstellen, geben Sie an das Betriebssystemabbild einzuschließen, verwenden Sie für die virtuellen Computer und wie viele VM-Instanzen, um beim Start zu erstellen. Sie werden auch die Größe des virtuellen Computers für jede Instanz, und ob Sie der Azure Load balancer oder Application Gateway für den Lastenausgleich angeben. Wenn Sie einen Load Balancer auswählen, wird im Portal eine standardmäßige integritätsüberprüfung an Port 80 für sie erstellt.

### <a name="powershell"></a>PowerShell

Sie können angeben, erstellen eine VM-Skalierungsgruppe mit der **New-AzureRmVmss** PowerShell-Cmdlet. Dieses Cmdlet kann erstellen eine neue Skalierungsgruppe mit einem Load Balancer und IP-Adresse und der virtuellen netzwerkzuweisungen zu steuern. Wenn die Einstellungen im Cmdlet angegeben werden **New-AzureRmVmss** verwendet die folgenden Standardeinstellungen:

* Erstellen Sie zwei VM-Instanzen
* Verwenden Sie das Windows Server 2016 Datacenter-image
* Verwenden Sie die VM-Größe Standard DS1_v2
* Einrichten eines Load Balancers
* Erstellen Sie Load Balancer-Regeln für die Ports 3389 und 5985 für Windows, Port 22 für Linux

**New-AzureRmVmss** erstellt keinen Integritätstest für den Load Balancer. Die bewährte Methode zum Erstellen dieser mit wäre **Add-AzureRmLoadBalancerProbeConfig** nach der Erstellung der Skalierungsgruppe.

Die horizontale Skalierung mit skalierungsgruppen können Sie mehrere Server zum Ausführen der Anwendung. Mit mehreren Servern ermöglicht, die Sie, hoch behandeln lädt und stellt sicher, dass Ihre Dienste verfügbar bleiben, selbst wenn ein Server abstürzt. Sie können in Ihren skalierungsgruppen, für die automatische Skalierung hinzufügen, damit Ihr System um unerwartete Änderungen in bei Bedarf automatisch angepasst wird.