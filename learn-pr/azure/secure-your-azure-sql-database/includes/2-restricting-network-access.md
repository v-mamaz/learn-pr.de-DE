Nehmen wir an, Sie führen eine online-Geschäft, und Sie Ihre Datenbank in Azure veröffentlichen. Standardmäßig werden eine Azure SQL Server-Datenbank auf Azure-Anwendung oder Dienst unter Azure zugegriffen werden kann. Auch wenn Sie nur Dienste in Azure eine Verbindung herstellen können, sollten Sie Verbindungen mit der Datenbank immer noch auf genehmigte Anwendungen und Dienste einschränken.

In dieser Einheit betrachten wir zum Einschränken des Zugriffs auf Azure SQL-Datenbank über die IP-Adressbereiche.

## <a name="overview"></a>Übersicht

Eine neue Azure SQL-Datenbank, in der Standardeinstellung nur Azure-Diensten eine Verbindung damit herstellen können. Diese Konfiguration bedeutet nicht, dass ein Dienst eine Verbindung herstellen den Datenbankinhalt zugreifen kann, die sie ausprobieren können, um für die Datenbank zu authentifizieren. Erfordern einen Dienst für die Authentifizierung ist sicherer als uneingeschränkten öffentlichen Internetzugriff. Sie sollten immer noch den Zugriff auf Ihre Datenbank auf nur die Anwendungen und Dienste, die ihn benötigen.

Beispielsweise kann eine ASP.NET Core-Anwendung, die Kommunikation mit Azure SQL-Datenbank haben. Es ist ASP.NET Core-Anwendung, die auf Ihre Azure SQL Server-Datenbank zugreifen muss. Sehen wir uns, wie wir den Netzwerkzugriff auf die Datenbank von der Webanwendung einschränken würden.

## <a name="restricting-network-access-to-the-database"></a>Beschränken des Netzwerkzugriffs mit der Datenbank

Sie einschränken des Netzwerkzugriffs auf Ihre Datenbank, da Zugriff auf einen bestimmten Bereich von IP-Adresse zugelassen.

![Screenshot des Azure-Portal mit dem Server Firewall-Regel-Erstellung mit einer beschriebenen IP-Einschränkung-Konfiguration hinzugefügt.](../media-draft/2-setting-ip-address-ranges-on-firewall.png)

1. Um eine Firewallregel für den Server zu erstellen, geben Sie einen **REGELNAME**, **START-IP-** Adresse ein, und die **END-IP-** Adresse.
1. Klicken Sie dann auf **speichern** um die Änderungen zu erfassen.

Nur die IP-Adressen in den Regeln, die Sie erstellen, haben Zugriff auf die Datenbank.

## <a name="locking-down-access-at-the-database-level"></a>Sperren des Zugriffs auf Datenbankebene

Nehmen wir an, dass Sie eine failovergruppe für Azure SQL-Server ausgeführt werden. Mit einer failovergruppe befinden sich die sekundären Server normalerweise auf verschiedenen Regionen. Wenn der Hauptserver offline geschaltet wird, können die Server-Firewall-Regeln nicht mehr gültig. Serverfirewallregeln werden pro Server, die die Datenbank gehostet wird eingerichtet. Einrichten einer Firewallregel auf Datenbankebene wird sichergestellt, dass die Regeln der Sicherungen von Datenbanken repliziert wird.

Um eine Datenbank-Firewallregel zu erstellen, Verbinden mit der Datenbank mit SQL Server Management Studio oder SQL Operations Studio aus, und erstellen Sie eine neue Abfrage. Erstellen Sie eine Datenbankregel, die mithilfe der folgenden Konvention, übergeben Sie den Namen der Regel, die IP-Startadresse und die IP-Endadresse.

```sql
EXECUTE sp_set_database_firewall_rule N'<Rule Name>', '<From IP Address>', '<To IP Address>'
```

Um den Zugriff auf die Datenbank aus dem IP-Adressbereich 10.21.2.33 – 10.21.2.54, beschränken verwenden Sie z. B. eine Regel ähnlich der folgenden SQL:

```sql
EXECUTE sp_set_database_firewall_rule N'Web Apps Firewall Rule', '10.21.2.33', '10.21.2.54'
```

## <a name="enabling-transparent-data-encryption-tde"></a>Aktivieren von Transparent Data Encryption (TDE)

### <a name="what-is-transparent-data-encryption"></a>Was ist Transparent Data Encryption?

Transparent Data Encryption (TDE) führt in Echtzeit Ver- und Entschlüsselung von der Datenbank, Sichern von Dateien und Protokolldateien.

Wenn neue Azure SQL-Datenbanken erstellt werden, müssen sie TDE standardmäßig aktiviert.

Es ist wichtig zu überprüfen, ob die datenverschlüsselung wurde nicht deaktiviert wurde, und ältere Azure SQL Server-Datenbanken möglicherweise keine TDE aktiviert.

So stellen Sie sicher, und aktivieren TDE:

1. Wählen Sie die Datenbank im Portal.
1. Wählen Sie die Option "Transparent Data Encryption".
1. Wählen Sie in der Data Encryption-Option 'On'.
1. Klicken Sie auf "Speichern".

## <a name="create-a-secure-connection-to-the-server"></a>Erstellen Sie eine sichere Verbindung mit dem server

Ihre Anwendungen auf Ihre Datenbanken auf sichere Weise eine Verbindung herstellen soll. Sie können eine Verbindungszeichenfolge mit das richtige Maß an Sicherheit verwenden, um eine sichere Verbindung zu erstellen. Diese Verbindungen müssen verschlüsselt werden, um die Wahrscheinlichkeit eines Man-in-the-Middle-Angriffs zu verringern.

Betrachten Sie zum Abrufen der Verbindungszeichenfolge für eine Datenbank aus.

Über das Portal, navigieren Sie zu Ihrem SQL Server. Wählen Sie die Datenbank, die, der Sie Zugriff auf möchten.

Wählen Sie die *-Datenbank-Verbindungszeichenfolgen anzeigen* Option.

Nun aus den verfügbaren Optionen aus, wählen Sie die Registerkarte, die die Programmiersprache entspricht, und kopieren Sie die angezeigte Verbindungszeichenfolge. Sie müssen, führen das Kennwort, wie sie geheime und nicht angezeigte hier beibehalten.

![Screenshot des Azure-Portal mit der Verbindung mit der Zeichenfolgen im Abschnitt mit ADO.NET ausgewählt und hervorgehoben Feld mit dem angegebenen Wert.](../media-draft/2-viewing-connection-strings.png)

Es ist wichtig, um die Verbindungszeichenfolge aus externen Augen zu schützen. Verbindungszeichenfolgen sollten nicht in Ihrem Projekt, der Versionskontrolle oder der continuous Integration-Systemen in Azure Key Vault gespeichert werden.

### <a name="what-is-the-azure-key-vault"></a>Was ist Azure Key Vault?

Azure Key Vault ist ein Tool zum sicheren Speichern von Anmeldeinformationen und anderen Schlüsseln und Geheimnissen verwendet. Diese Geheimnisse können entweder durch Software- oder Hardwarefehlern geschützt werden.

## <a name="open-the-correct-ports-for-server-access"></a>Öffnen Sie die richtigen Ports für den Zugriff auf server

Ihre Azure-Datenbank ermöglicht die ausgehende Kommunikation über Port 1433. Wenn Sie keinen Zugriff auf diesen Port haben, wenden Sie sich an Ihren Netzwerkadministratoren, die Netzwerkdatenverkehr zulässt.

## <a name="restrict-server-access-with-azure-virtual-networks"></a>Beschränken Sie den Serverzugriff in Azure virtual networks

### <a name="what-is-a-virtual-network"></a>Was ist ein virtuelles Netzwerk?

Ein virtuelles Netzwerk ist eines logisch isolierten Netzwerks im Azure-Netzwerk erstellt. Sie können ein virtuelles Netzwerk verwenden, um zu steuern, welche Azure-Ressourcen auf andere Ressourcen verbinden können.

Stellen Sie sich vor, dass Sie eine Webanwendung ausführen, die einer Datenbank herstellt. Sie werden Subnetze verwenden, um verschiedene Teile des Netzwerks zu isolieren. Ein Subnetz ist ein Teil des Netzwerks basierend auf einen Bereich von IP-Adressen.

Um diesen Subnetzen zu konfigurieren, Sie erstellen ein virtuelles Netzwerk und dann das Netzwerk in Subnetze unterteilen. Die Webanwendung wird für ein Subnetz und die Datenbank in einem anderen Subnetz verwendet werden. Jedes Subnetz müssen eigene Regeln für die Kommunikation zu und von anderen Netzwerk. Diese Regeln bieten Ihnen die Möglichkeit, den Zugriff auf die Webanwendung aus der Datenbank zu beschränken.

### <a name="what-is-a-network-security-group"></a>Was ist eine Netzwerksicherheitsgruppe?

Eine Netzwerksicherheitsgruppe definiert Regeln, die zulassen oder Verweigern von Netzwerkdatenverkehr zu und von Quell-und Zieladressen. Jedes Subnetz wird eine Netzwerksicherheitsgruppe zugewiesen haben.

Das folgende Diagramm zeigt ein Beispiel für die Gruppierungen, die erstellt werden. Die websubnetz ermöglicht Zugriff auf das Internet, sondern nur für HTTP-Verbindungen. Das datenbanksubnetz kann nur Zugriff aus dem websubnetz. Das virtuelle Netzwerk einrichten, fügt Einschränkungen darüber, wie die Dienste zugegriffen werden kann, und fungiert als einer Firewall für gehostete Dienste hinzu.

![Virtuelles Netzwerk für eine Webanwendung mit einer verbundenen Datenbank](../media-draft/2-virtualnetwork-overview.png)

Im nächste Beispiel wird davon ausgegangen, dass Sie virtuelle Computer verwenden, die mit Ihrer Datenbank verbinden und fungieren als Ihre Web-Hosts. Wir sehen uns Gewusst wie: Erstellen eines virtuellen Netzwerks, um diese geplanten Infrastruktur einzurichten.

1. Wählen Sie im Azure-Portal die **erstellen Sie eine Ressource** Link.
1. Wählen Sie im Azure Marketplace **Networking** > **virtuelles Netzwerk**. Wenn sie ein Bereitstellungsmodell auswählen möchte, wählen Sie **Resource Manager**
1. Klicken Sie auf die Schaltfläche **Erstellen** .
1. Geben Sie die **Namen** für das virtuelle Netzwerk.
1. Geben Sie eine **Adressraum** verwendet werden kann. Ein Adressraum ist eine Möglichkeit, einen Bereich von IP-Adressen zu gliedern. In unserem Beispiel `172.16.0.0/16` bezieht sich auf einen Adressbereich 172.16.0.0, 172.16.255.255.

   Ein Adressraum, der nicht bereits verwendet wird, werden Empfehlungen gegeben. Wenn eine IP-Adresse aus diesem Bereich erkannt wird, wird sie als in diesem Subnetz definiert werden.

1. Wählen Sie Ihr Azure- **Abonnement**.
1. Wählen oder erstellen Sie ein neues **Ressourcengruppe**.
1. Geben Sie die **Namen** des Subnetzes, die Sie erstellen.
1. Geben Sie eine **Adressbereich**.
1. Klicken Sie auf die **erstellen** klicken, um das virtuelle Netzwerk zu erstellen.

![Screenshot des Azure-Portal mit erstellen Sie ein Blatt des virtuellen Netzwerks mit der beschriebenen Konfiguration.](../media-draft/2-create-virtual-network-settings.png)

Sie erhalten eine Benachrichtigung, sobald das virtuelle Netzwerk erstellt wurde. Klicken Sie auf die **zu Ressource wechseln** in der Benachrichtigung.

Sie gelangen nun auf dem Blatt "virtuelles Netzwerk". Wählen Sie die **Einstellungen** > **Subnetze** Konfigurationsabschnitt. An diesem Punkt müssen Sie das Subnetz an, die, das Sie erstellt haben, wenn Sie das erste Netzwerk, mit dem Namen Web_subnet einrichten.

Sie müssen ein anderes Subnetz zu erstellen, das die IP-Adressen für die Datenbankserver darstellt.

1. Klicken Sie auf die __+ Subnetz__ Schaltfläche, um den Prozess des Hinzufügens eines neuen Subnetzes für die Datenbank zu starten.

1. Geben Sie einen **Namen** für das Subnetz. Im obigen Beispiel wird aufgerufen, wir es Database_subnet.

1. Überprüfen Sie die **Adressbereich (CIDR-Block)**. Sie sehen, dass der Adressbereich erneut mit einem Bereich aufgefüllt wird, die nicht in Konflikt mit anderen Subnetzen im System.

1. **Netzwerksicherheitsgruppe** ist eine Core-Einstellung, die Sie benötigen, auf das Subnetz anzuwenden. Lassen Sie diese Einstellung vorerst leer. Später Sie die Netzwerksicherheitsgruppe zu erstellen, und kehren Sie zurück und legen Sie diesen Wert.

1. Klicken Sie auf die **OK** aus, um das Subnetz zu speichern.

![Screenshot des Azure-Portal mit dem Blatt "Subnetz hinzufügen", mit der beschriebenen Konfiguration.](../media-draft/2-create-database-subnet.png)

## <a name="creating-a-network-security-group"></a>Erstellen eine Netzwerksicherheitsgruppe.

Die Aufgabe die Netzwerksicherheitsgruppe ist, die als Firewall fungiert, und er steuert den Fluss des Datenverkehrs in und aus einem Subnetz. Sie erstellen zwei netzwerksicherheitsgruppen. Eine ist das Web-Subnetz aus, und die andere für das datenbanksubnetz ist.

1. Wählen Sie **erstellen Sie eine Ressource** , und wählen Sie **Networking** > **Netzwerksicherheitsgruppe**. Wenn Sie dazu aufgefordert, ein Bereitstellungsmodell aus, wählen Sie die Resource Manager.
1. Geben Sie einen **Namen** für die Netzwerksicherheitsgruppe.
1. Wählen Sie Ihre Azure-Abonnement, Ressourcengruppe und gewünschten Speicherort.
1. Klicken Sie auf die Schaltfläche **Erstellen** .

![Screenshot des Azure-Portal mit der Sicherheitsgruppe "Web", für das websubnetz ausgewählt.](../media-draft/2-define-nsg-for-web-subnet.png)

Nachdem Sie die Netzwerksicherheitsgruppe erstellt wurde, ist es Zeit, die Regeln für eingehenden und ausgehenden Datenverkehr für die Sicherheitsgruppe einrichten.

1. Wählen Sie die neue Netzwerksicherheitsgruppe aus.
1. Auf der **Übersicht** anzeigen, sehen Sie die Liste der ein- und ausgehende Regeln, die erstellt wurden. Es gibt bereits erstellten Regeln, die für den internen Azure-Zugriff verwendet werden.

    > [!NOTE]
    > Während diese Regeln nicht gelöscht werden können, können Sie zusätzliche Regeln mit höherer Priorität erstellen, die diese Regeln Vorrang hat.

![Screenshot des Azure-Portal zeigt die vorkonfiguriert, dass eingehende und ausgehende Sicherheitsregeln einer Netzwerksicherheitsgruppe.](../media-draft/2-view-web-apps-security-group-rules.png)

1. Um neue Regeln erstellen, wählen die **Eingangssicherheitsregeln** Abschnitt für die Netzwerksicherheitsgruppe hinzu.
1. Klicken Sie auf die Schaltfläche **Hinzufügen** . Von hier aus können Sie die Details für die Netzwerksicherheitsgruppe Sicherheitsregeln konfigurieren.

    > [!NOTE]
    > Standardmäßig sehen Sie die erweiterte Ansicht so konfigurieren Sie die Regel, aber indem Sie auf die **grundlegende** Schaltfläche, Sie werden das Protokoll auswählen, Sie zulassen möchten.

1. Sie möchten den Zugriff auf HTTP-Dienste über das Internet zu ermöglichen. Um für die HTTP-Protokoll zu filtern, wählen Sie **Diensttag** als die **Quelle** Wert.
1. Überprüfen Sie dann die **Quelldiensttag** nastaven NA hodnotu **Internet**.
1. Gruppe, die der Port Werte Bereiche `80,443` Ports dar, die verwendet werden, um diesen Dienst zugreifen. (Port 80 für HTTP verwendet wird, und Port 443 für HTTPS-Zugriff verwendet.)
1. Wählen Sie **TCP** als **Protokoll** aus.
1. Legen Sie **Aktion** zu **ermöglichen**.
1. Geben Sie die Regel ein **Priorität** Wert `100`.

    > [!NOTE]
    > Je niedriger die Zahl, desto wichtiger ist die Regel.

![Screenshot des Azure-Portal mit Blatts Regel eingangssicherheitsregel hinzufügen, mit der angegebenen Konfiguration und dem quelldiensttag (Internet) und der Zielport liegt (80,443) Felder hervorgehoben.](../media-draft/2-add-inbound-security-rule-for-web-nsg.png)

Jetzt ist es Zeit, um die Einstellungen für netzwerksicherheitsgruppen für die Datenbank einzurichten. Für die Datenbank Sie sind wir richten eine eingehende Regel, die SQL-Anforderungen aus dem IP-Adressbereich des Subnetzes, Web-Anwendungen ermöglicht und klicken Sie dann zu anderen eingehenden und ausgehenden Datenverkehr verweigern. Dadurch können Sie steuern den Zugriff auf die Datenbank, und stellen Sie sicher, dass nur Anforderungen von der Website auf das System gelangen und ansonsten keinen Zugriff auf die Datenbank zulässig ist.

1. Klicken Sie auf die **erstellen Sie eine Ressource** erneut aus, um ein weiteres erstellen **Networking** > **Netzwerksicherheitsgruppe** , die Ressourcen-Manager als Bereitstellungsmodell verwendet.

    Dieses Mal erstellen Sie eine für die Datenbank.

1. Geben Sie einen **Namen** für die Netzwerksicherheitsgruppe.
1. Wählen Sie Ihre Azure-Abonnement, Ressourcengruppe und gewünschten Speicherort.
1. Klicken Sie auf die **erstellen** klicken, um die neue Netzwerksicherheitsgruppe erstellen.

    ![Screenshot des Blatts erstellen Network Security Group mit einer Beispielkonfiguration mit Azure-Portal.](../media-draft/2-create-database-network-security-group.png)

    Sie müssen warten, bis die Netzwerksicherheitsgruppe erstellt wird.

1. Wählen Sie danach die **zu Ressource wechseln** Option in der Benachrichtigung zu beginnen, konfigurieren die Regeln für die Netzwerksicherheitsgruppe, die Sie erstellt haben.

Für die Netzwerksicherheitsgruppe aus ist das Hauptaugenmerk datenbankanforderungen von der Web Application-Subnetz nur. In diesem Fall müssen Sie eine eingehende TCP-Anforderungen an Port 1433 von der IP-Adressbereich des Subnetzes Web einzurichten.

1. In der **Eingangssicherheitsregeln** -Einstellungen auf der **hinzufügen** klicken, um eine neue Regel zu erstellen. In diesem Fall möchten Sie nur den Zugriff von der Web Application-Subnetz zu.
1. Erstellen Sie eine eingehende Regel, die festlegt der **Quelle** zu **IP-Adressen**.
1. Wenn die **Quell-IP-Adressen/CIDR-Bereiche** werden angezeigt, geben Sie die CIDR-Bereich aus dem websubnetz, das zuvor erstellt wurde.
1. Für die **Zielportbereiche**, geben Sie `1433` nur Azure SQL Server-Zugriff an.
1. Legen Sie die **Protokoll** zu **TCP** , eingehende Verbindungen weiter einzuschränken.
1. Sie möchten **zulassen** Zugriff auf für **Aktion**.
1. Geben Sie ihm eine **Priorität** von `100`.
1. **Namen** entsprechend die Sicherheitsregel.
1. Klicken Sie auf **hinzufügen** , um die Regel hinzuzufügen.

![Screenshot des Azure-Portal mit dem Blatt "eingangssicherheitsregel-Regel hinzufügen" mit der beschriebenen Konfiguration.](../media-draft/2-create-inbound-rule-for-db-security-group.png)

Die grundlegende Sicherheitsregeln sind jetzt Zugriff auf das Datenbanksystem zu begrenzen. Nun muss nur noch ist im Netzwerk-Sicherheitsgruppen mit den Subnetzen zugewiesen.

1. Öffnen Sie das virtuelle Netzwerk, die, das Sie zuvor erstellt haben. Wählen Sie die **Einstellungen** > **Subnetze** Abschnitt.
1. Wählen Sie das zuvor erstellte websubnetz.
1. Wählen Sie die **Netzwerksicherheitsgruppe** Option und die Netzwerksicherheitsgruppe, die speziell für das Web erstellt.
1. Klicken Sie auf **speichern** und die Netzwerksicherheitsgruppe für das Subnetz angewendet werden.

    ![Screenshot des Azure-Portal mit einer Netzwerksicherheitsgruppe, die für das websubnetz angewendete](../media-draft/2-define-nsg-for-web-subnet.png)

Möchten Sie den gleichen Vorgang zu wiederholen, für das datenbanksubnetz.

1. Navigieren Sie zurück zu den Subnetzen.
1. Wählen Sie das datenbanksubnetz
1. Legen Sie dessen **Netzwerksicherheitsgruppe** der Netzwerk-Sicherheitsgruppe für die Datenbank.
1. Klicken Sie zum Speichern der Änderungen auf **Speichern**.

    ![Screenshot des Azure-Portal mit einer angewendete Netzwerksicherheitsgruppe für das datenbanksubnetz ausgewählt.](../media-draft/2-define-nsg-for-db-subnet.png)

Nun, dass Sie den Zugriff konfiguriert haben, ist es anzuwenden, die virtuellen Netzwerke und Subnetze für die Datenbank-Server und Webserver.

Beginnen wir mit dem Datenbankserver an.

1. Wählen Sie die Datenbank an.
1. Wählen Sie aus der Datenbank, die **Firewalls und virtuelle Netzwerke** Konfigurationseinstellung.

Klicken Sie auf der linken Seite sehen Sie die Details zur Konfiguration. Sie haben eine Reihe von Einstellungen auf spielen hier eine Rolle.

1. Aktivieren Sie zuerst **zulassen des Zugriffs auf Azure-Dienste** zu **OFF**. Dadurch wird sichergestellt, dass die Dienste, die Sie verwenden möchten, aktiviert sind.

    Sie werden bemerken, dass eine Client-IP-Adresse angezeigt. Die Client-IP-Adresse ist die IP-Adresse des Computers beim Herstellen einer Verbindung mit der Azure SQL-Datenbank. Sie können eine Client-IP-Adresse der Regelliste für Namen hinzugefügt haben. Dies ist nützlich, wenn Sie SQL Server Management Studio oder SQL Operations Studio mit Ihrem Server herstellen möchten. Dabei werden hinzugefügt, dass eine Regel, die angibt, der IP-Adressen eine Verbindung herstellen kann. Sie wird nicht tun, die in diesem Fall, aber Sie müssen werden einrichten, dass das virtuelle Netzwerk.

1. Klicken Sie auf **vorhandenes virtuelles Netzwerk hinzufügen**, und es werden ein Optionsbildschirm zur Eingabe der Details für die neue Regel angezeigt.

1. Geben Sie die **Namen** der Regel, die Sie verwenden möchten.
1. Wählen Sie das Abonnement, das Sie verwendet haben.
1. Wählen Sie wichtiger ist, das virtuelle Netzwerk, das Sie verwenden.
1. Wählen Sie das Subnetz mit der entsprechenden netzwerksicherheitsgruppen-Regeln für den Datenbankzugriff.
1. Nachdem Sie alle Einstellungen konfiguriert haben, wählen Sie die **aktivieren** Schaltfläche. Es wird die Datenbank mit dem Subnetz in Ihrem virtuellen Netzwerk angewendet.

Sobald die datenbanksubnetz konfiguriert ist, führen Sie ähnliche Schritte mit dem Webserver. Unabhängig davon, wie Sie Ihre Anwendung konfiguriert haben ist es eine Frage stellt sicher, dass die Webanwendungen im Subnetz für den Webzugriff verwenden.

Wenn Sie einen einzelnen virtuellen Computer oder einem Load Balancer mit virtuellen Computern in einer Skalierungsgruppe festgelegt haben, stellen Sie sicher, dass sie die websubnetz verwendet werden, müssen sie Zugriff auf die Datenbank. Wenn Sie Ressourcen wie virtuelle Computer erstellen, stellen Sie sicher, dass ihre virtuelle Netzwerk und Subnetze konfiguriert sind, um zu steuern, die Informationen, die gesendet wird, ein-und von diesen Diensten.

![Screenshot des Azure-Portal mit den Einstellungen auf dem Blatt Schritt erstellen einen neuen virtuellen Computer, in dem das virtuelle Netzwerk und Subnetz-Werte haben festgelegt wurde.](../media-draft/2-configure-virtual-machine-with-subnet.png)

Sobald die Subnetze in der Datenbank und den virtuellen Computern, die Web-apps angewendet werden, wird die entsprechende Konfiguration vorhanden sein. Klicken Sie dann eine engere Zugriff ist zwischen Ihren apps und die Datenbank.

Netzwerksicherheit ist der erste zentralen Punkt des Schutzes. Um sicherzustellen, dass nur die apps und Dienste, die eine Verbindung, auf die Datenbank herstellen soll mit der Datenbank hergestellt werden, wird Ihr System sicherer machen.
