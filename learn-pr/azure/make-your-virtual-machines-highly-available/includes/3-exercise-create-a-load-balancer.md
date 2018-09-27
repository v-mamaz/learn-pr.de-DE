Zur Erinnerung: Sie arbeiten bei der Woodgrove Bank und möchten Onlinebankingdienste anbieten. Aufgrund des hohen Wettbewerbsdrucks in dieser Branche müssen Sie eine Dienstverfügbarkeit von 99,99 % gewährleisten. Sie haben ermittelt, dass Sie Azure Load Balancer mit einem Pool von drei virtuellen Computern benötigen, um dieses Ziel zu erreichen.

In dieser Übung erstellen Sie einen Lastenausgleich und ein virtuelles Netzwerk über das Azure-Portal. Sie können zwischen diesen beiden Optionen wählen und diese mithilfe des Portals ganz einfach erstellen.

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-public-load-balancer"></a>Erstellen eines öffentlichen Lastenausgleichs

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) mit dem Konto an, über das Sie die Sandbox aktiviert haben.

1. Klicken Sie in der Randleiste auf **Ressource erstellen**.

1. Wählen Sie den Abschnitt **Netzwerk** aus, und klicken Sie dann auf **Load Balancer**. Wenn diese Auswahl nicht angezeigt wird, können Sie das Suchfeld verwenden.

    ![Screenshot vom Azure Marketplace mit dem ausgewählten Abschnitt „Netzwerk“ und dem hervorgehobenen Load Balancer](../media/3-azure-marketplace.png)

1. Geben Sie auf dem Blatt **Lastenausgleich erstellen** folgende Informationen ein, oder wählen Sie sie aus:
    - **Name:** _woodgrove-LB_
    - **Typ:** _Öffentlich_
    - **SKU:** _Basic_
    - **Öffentliche IP-Adresse:** Klicken Sie auf **Neu erstellen**. Geben Sie im Textfeld _woodgrove-LB-ip_ ein. Übernehmen Sie für „Zuweisung“ den Wert _Dynamisch_.
    - **Abonnement:** Das _Concierge-Abonnement_ sollte bereits ausgewählt sein.
    - **Ressourcengruppe:** Wählen Sie zuerst **Vorhandene verwenden** und anschließend _<rgn>[Name der Sandboxressourcengruppe]</rgn>_ aus.
    - **Standort:** Wählen Sie aus der folgenden Liste eine Region in Ihrer Nähe aus.

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

    ![Screenshot vom Bildschirm der Erstellung eines neuen Lastenausgleichs](../media/3-create-load-balancer.png)

1. Klicken Sie auf **Erstellen**.

Während die Lastenausgleichsressource erstellt und bereitgestellt wird, können wir das Azure Virtual Network erstellen, das wir für das Back-End-Subnetz verwenden.

## <a name="create-a-virtual-network"></a>Erstellen eines virtuellen Netzwerks

1. Klicken Sie im Menü links auf **Ressource erstellen**. Klicken Sie auf dem Blatt **Neu** zuerst auf **Netzwerk** und anschließend auf **Virtuelles Netzwerk**.

    ![Screenshot vom Azure Marketplace mit dem ausgewählten Abschnitt „Netzwerk“ und dem hervorgehobenen Load Balancer](../media/3-azure-marketplace-2.png)

1. Geben Sie auf dem Blatt **Virtuelles Netzwerk erstellen** folgende Informationen ein, oder wählen Sie sie aus:
    - **Name:** _woodgrove-VNET_
    - **Adressraum:** _172.20.0.0/16_
    - **Abonnement:** Das _Concierge-Abonnement_ sollte bereits ausgewählt sein.
    - **Ressourcengruppe:** Wählen Sie aus der Liste die vorhandene Ressourcengruppe _<rgn>[Ressourcengruppenname]</rgn>_ aus.
    - **Subnetzname:** _backendSubnet_
    - **Subnetzadressbereich:** _172.20.0.0/24_
    - **DDoS-Schutz:** _Basic_
    - **Dienstendpunkte:** _Deaktiviert_

    ![Screenshot vom Bildschirm der Erstellung eines neuen Lastenausgleichs](../media/3-create-vnet.png)

1. Klicken Sie auf **Erstellen**.

Während das virtuelle Netzwerk bereitgestellt wird, erstellen wir eine Netzwerksicherheitsgruppe.

## <a name="create-and-configure-a-network-security-group"></a>Erstellen und Konfigurieren einer Netzwerksicherheitsgruppe

1. Klicken Sie auf **Ressource erstellen**.

1. Wählen Sie die Gruppe **Netzwerk** aus, und klicken Sie auf das Element **Netzwerksicherheitsgruppe**.

    ![Screenshot vom Azure Marketplace mit dem ausgewählten Abschnitt „Netzwerk“ und der hervorgehobenen Netzwerksicherheitsgruppe](../media/3-azure-marketplace-3.png)


1. Geben Sie ihr den Namen **woodgrove-NSG**, und platzieren Sie sie in der Ressourcengruppe der Azure-Sandbox.

1. Stellen Sie sicher, dass sie sich am gleichen Standort wie der Azure Load Balancer befindet.

    ![Screenshot vom Bildschirm der Erstellung einer Netzwerksicherheitsgruppe](../media/3-create-nsg.png)

1. Klicken Sie auf **Erstellen**.

Warten Sie, bis der Lastenausgleich, das virtuelle Netzwerk und die Netzwerksicherheitsgruppe (NSG) bereitgestellt werden. Dann können Sie die Netzwerksicherheitsgruppe konfigurieren.

## <a name="configure-the-network-security-group"></a>Konfigurieren der Netzwerksicherheitsgruppe

1. Wählen Sie die neue Netzwerksicherheitsgruppe entweder über die Bereitstellungsbenachrichtigung oder über die Suchleiste am oberen Rand des Azure-Portals aus.

    ![Screenshot von der erfolgreichen Bereitstellung im Panel „Benachrichtigung“](../media/3-deployment-success.png)

1. Wählen Sie den Abschnitt **Einstellungen** > **Eingangssicherheitsregeln** aus. Beachten Sie, dass es drei vordefinierte Regeln gibt, die immer angewendet werden. Zu diesen Regeln gehören:
    - **AllowVnetInbound:** Zulassen des gesamten internen Datenverkehrs im virtuellen Netzwerk Diese Regel erlaubt es den VMs, die sich in einem Netzwerk befinden, miteinander zu kommunizieren.
    - **AllowAzureLoadBalancerInBound:** Erlaubt es dem Lastenausgleich, Dienste im Netzwerk zu „pingen“, um herauszufinden, ob diese aktiv sind.
    - **DenyAllInbound:** Verweigern des gesamten anderen Datenverkehrs.

    Die **DenyAllInbound**-Regel ist besonders wichtig, da dadurch sichergestellt wird, dass sämtlicher eingehender Datenverkehr, der keine Regel mit höherer Priorität hat, blockiert wird. Daher muss eine neue Regel hinzugefügt werden, um HTTP-Datenverkehr (Port 80) für die Webserver zuzulassen.

    > [!NOTE]
    > Die Priorität in NSG-Regeln liegt zwischen 0 und 65500, und Regeln werden der Reihe nach ausgewertet. Die erste übereinstimmende Regel wird Entscheidungsträger. Sie sollten für Ihre Regeln immer recht niedrige Prioritäten festlegen (ca. 1000), sodass diese Vorrang vor den vordefinierten Regeln haben.

1. Klicken Sie auf **Hinzufügen**, um eine neue Regel hinzuzufügen.

    ![Screenshot von den eingehenden Netzwerksicherheitsregeln mit hervorgehobener Schaltfläche „Hinzufügen“](../media/3-inbound-security-rules.png)

1. Klicken Sie ganz oben auf die Schaltfläche **Basic**, um zur Ansicht „Basic“ zu wechseln.

1. Geben Sie die Details für die neue Regel an.
    - Wählen Sie für den **Dienst** _HTTP_ aus.
    - Legen Sie die **Priorität** auf _1000_ fest.
    - Geben Sie der Regel einen Namen (oder übernehmen Sie den Standardnamen).

    ![Screenshot von dem mit HTTP-Details ausgefüllten Dialogfeld „Eingangssicherheitsregel hinzufügen“](../media/3-add-inbound-rule.png)

1. Klicken Sie auf **Hinzufügen**, um die Regel hinzuzufügen.

    ![Screenshot von der neu hinzugefügten HTTP-Regel in der Liste von NSG-Regeln](../media/3-new-added-rule.png)

## <a name="apply-the-network-security-group-to-the-vnet"></a>Anwenden der Netzwerksicherheitsgruppe auf das VNet

Als Nächstes wenden Sie diese Netzwerksicherheitsgruppe auf das virtuelle Netzwerk an.

1. Suchen Sie Ihr virtuelles Netzwerk, indem Sie das Suchfeld oben verwenden. Der Name lautet **woodgrove-VNET**.

1. Wählen Sie **Einstellungen** > **Subnetze** aus, um die definierten Subnetze zu erhalten.

1. Klicken Sie auf den Eintrag **backendSubnet**, um die Eigenschaften zu öffnen.

    ![Screenshot von den backendSubnet-Einträgen im Bereich „Subnetze“ der Subnetze](../media/3-subnets.png)

1. Klicken Sie in der **Netzwerksicherheitsgruppe** auf den Eintrag „Keine“.

    ![Screenshot von der leeren Netzwerksicherheitsgruppe im backendSubnet](../media/3-add-network-security-group.png)

1. Wählen Sie die **woodgrove-NSG** aus, um sie diesem VNet hinzuzufügen.

1. Klicken Sie auf **Speichern**, um die Änderungen zu übernehmen.

Da das Netzwerk jetzt eingerichtet ist, können Sie virtuelle Computer im Netzwerk erstellen.