Sie haben die wichtigsten Ressourcen für die Architektur Ihrer Onlinebank erstellt. In dieser Übung konfigurieren Sie Regeln für den Lastenausgleich und schließen das Setup dadurch ab.

Testen Sie den Lastenausgleich nach Abschluss des Setups, indem Sie eine VM aus dem Pool entfernen und überprüfen, ob die Clientanforderungen nicht mehr an diese VM gesendet werden.

Zunächst wird der Back-End-Pool im Lastenausgleich definiert. Dadurch wird festgelegt, wohin eingehende Anforderungen weitergeleitet werden.

## <a name="create-a-backend-address-pool"></a>Erstellen eines Back-End-Adresspools

1. Klicken Sie im [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) im Menü auf der linken Seite auf **Alle Ressourcen**. Wählen Sie dann Ihren Lastenausgleich (**woodgrove-LB**) aus der Ressourcenliste aus.

1. Klicken Sie auf **Einstellungen** > **Back-End-Pools**. Sie werden feststellen, dass bisher noch keiner definiert wurde.

1. Klicken Sie auf **Hinzufügen**, um einen neuen Back-End-Pool hinzuzufügen.

    ![Screenshot, der das Hinzufügen eines Back-End-Pools darstellt](../media/6-backend-pools.png)

1. Fügen Sie auf dem Blatt **Back-End-Pool hinzufügen** die folgenden Informationen hinzu:
    - Nennen Sie den Pool _woodgrove-BEP_.
    - Verknüpfen Sie den Pool mit einer **Verfügbarkeitsgruppe**.
    - Wählen Sie _woodgrove-AS_ als Verfügbarkeitsgruppe aus.

1. Klicken Sie auf **Zielnetzwerk-IP-Konfiguration hinzufügen**.

1. Wählen Sie in der Liste **Virtueller Zielcomputer** den Eintrag _woodgrove-VM1_ aus.

1. Wählen Sie in der Liste **Netzwerk-IP-Konfiguration** für die VM den IP-Adressenpool der VM aus.

1. Wiederholen Sie diese Schritte, um _woodgrove-VM2_ und _woodgrove-VM3_ zum Back-End-Pool hinzuzufügen.

    ![Screenshot, der das Blatt „Back-End-Pool hinzufügen“ mit allen drei ausgewählten VMs zeigt](../media/6-add-backend-pool.png)

1. Klicken Sie auf **OK**, um das Blatt zu schließen.

Warten Sie, bis die Konfiguration für den Lastenausgleich aktualisiert wurde, bevor Sie mit der Übung fortfahren.

## <a name="create-a-health-probe-for-the-load-balancer"></a>Erstellen eines Integritätstests für den Lastenausgleich

Fügen Sie als Nächstes einen Integritätstest für HTTP über Port 80 hinzu.

1. Klicken Sie auf dem Blatt **woodgrove-LB** unter **Einstellungen** auf **Integritätstests**. Sie werden feststellen, dass dieser Bereich derzeit leer ist.

1. Klicken Sie auf **Hinzufügen**, um einen neuen Integritätstest hinzuzufügen.

1. Legen Sie auf dem Blatt **Integritätstest hinzufügen** folgende Konfiguration fest:
    - **Name:** _woodgrove-HP_
    - **Protokoll:** _HTTP_
    - **Port:** _80_
    - **Pfad:** _/_
    - **Intervall:** _15_
    - **Fehlerhafter Schwellenwert:** _2_

1. Klicken Sie zum Speichern der Änderungen auf **OK**.

Warten Sie, bis die Konfiguration für den Lastenausgleich aktualisiert wurde, bevor Sie mit der Übung fortfahren.

## <a name="create-a-load-balancer-rule"></a>Erstellen einer Lastenausgleichsregel

Erstellen Sie abschließend eine Lastenausgleichsregel für HTTP über Port 80, mit der der Back-End-Pool dem Integritätstest zugeordnet wird.

1. Klicken Sie auf dem Blatt **woodgrove-LB** unter **Einstellungen** auf **Lastenausgleichsregeln**.

1. Klicken Sie auf **Hinzufügen**, um eine neue Regel hinzuzufügen.

1. Legen Sie auf dem Blatt **Lastenausgleichsregel hinzufügen** den **Namen** auf _woodgrove-HTTP-LBRule_ fest.

1. Überprüfen Sie, ob die folgenden Informationen automatisch eingegeben wurden:
    - IP-Version: **IPv4**
    - Front-End-IP-Adresse: **LoadBalancerFrontEnd**
    - Protokoll: **TCP**
    - Port: **80**
    - Back-End-Port: **80**
    - Back-End-Pool: **woodgrove-BEP**
    - Integritätstest: **woodgrove-HP**
    - Sitzungspersistenz: **Keine**
    - Leerlauftimeout: **4 Minuten**
    - Floating IP: **Deaktiviert**

1. Klicken Sie zum Speichern der Regel auf **OK**.

Warten Sie, bis die Konfiguration für den Lastenausgleich aktualisiert wurde, bevor Sie mit der Übung fortfahren.

## <a name="test-the-load-balancer"></a>Testen des Lastenausgleichs

1. Wechseln Sie zurück zur Seite **Übersicht** des Lastenausgleichs, und klicken Sie auf den Link **Öffentliche IP-Adresse**, um zur zugewiesenen IP-Adresse zu gelangen. Alternativ können Sie auf **Alle Ressourcen** klicken und in der Ressourcenliste **woodgrove-LB-ip** auswählen.

1. Wählen Sie auf dem Blatt **Übersicht** die **IP-Adresse** aus, und klicken Sie direkt daneben auf die Schaltfläche **Kopieren**. Dies ist die _öffentliche_ IP-Adresse des Lastenausgleichs.

    ![Screenshot, der die öffentliche IP-Adresse im Bereich „Übersicht“ anzeigt](../media/6-public-ip.png)

1. Öffnen Sie eine neue Browserregisterkarte, und fügen Sie die IP-Adresse in die Adressleiste Ihres Browsers ein. Notieren Sie sich den Namen des Servers, und lassen Sie die Registerkarte geöffnet.

1. Klicken Sie im Azure-Portal im Menü auf der linken Seite auf **Alle Ressourcen**. Klicken Sie in der Ressourcenliste dann auf den Server, den Sie sich oben notiert haben.

1. Klicken Sie auf dem Blatt **Übersicht** auf **Beenden** und dann auf **Ja**.

1. Warten Sie, bis die VM beendet wurde, und wechseln Sie dann zu der Registerkarte, die Sie in Schritt 3 angezeigt haben. Aktualisieren Sie die Seite.

1. Der Lastenausgleich sendet Ihre HTTP-Anforderung an eine Ihrer anderen VMs.

In dieser Übung haben Sie erfahren, wie Sie Back-End-VMs und den Lastenausgleich bereitstellen.
