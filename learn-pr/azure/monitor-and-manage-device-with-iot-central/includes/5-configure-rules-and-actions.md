Sie haben Ihre Kaffeemaschine mit der Azure IoT Central-Anwendung verbunden und so den Austausch von Daten aktiviert, mit deren Hilfe Sie Ihre Kaffeemaschine überwachen und verwalten können. In dieser Einheit erstellen Sie Regeln, die Aktionen auslösen, wenn die Wassertemperatur die Kaffeemaschine außerhalb des normalen Bereichs liegt. Die Aktionen sind entweder E-Mails oder SMS-Benachrichtigungen, je nachdem, ob für die Maschine noch Garantie gilt oder nicht. Um Microsoft Flow als Aktion hinzuzufügen, benötigen Sie ein Azure-Abonnement. Wenn Sie nicht über ein Azure-Abonnement verfügen, ist das Hinzufügen von Microsoft Flow als Aktion optional.

## <a name="create-rules-in-iot-central-with-email-as-the-action"></a>Erstellen von Regeln in IoT Central mit E-Mail als Aktion
Azure IoT Central kann Benachrichtigungen mithilfe seiner nativen E-Mail-Funktion senden. In diesem Szenario wird, wenn die Kaffeemaschine außerhalb des optimalen Temperaturbereichs liegt und nicht durch Garantie geschützt ist, eine E-Mail von IoT Central an die Wartungsabteilung des Kunden gesendet.

Navigieren Sie zu der **Regeln** Seite für die Übungen in dieser Einheit. Wählen Sie **+ neue Regel**, klicken Sie dann **Telemetriedaten**. Fügen Sie die folgenden zwei Regeln hinzu, wenn die Garantie der Kaffeemaschine abgelaufen ist und die Wassertemperatur außerhalb des optimalen Bereichs liegt. Wählen Sie abschließend **Speichern** aus. 

> [!NOTE]
> Wenn die Bedingungen angewendet werden, müssen alle Aussagen wahr sein, damit die Regeln ausgeführt werden. Wenn Ihre Bedingung wie in einer "oder"-Anweisung ist Teilen dieses Szenario (z. B. die optimale Temperatur ist kleiner oder größer als die vordefinierte Werte während der Garantie ist abgelaufen), die Anweisung in zwei Regeln wie hier gezeigt.

1. Benennen Sie die Regel: Wasser in Kaffeemaschine zu kalt (abgelaufen)

    Fügen Sie die Bedingungen hinzu:      
    * Abgelaufene Gerätegarantie entspricht 1
    * Wassertemperatur ist kleiner als Kaffeemaschinen Min Temperatur

    ![Verwenden von Regelsätzen](../images/5-flow-a.png)

1. Benennen Sie die Regel: Wasser in Kaffeemaschine zu heiß (abgelaufen)

    Fügen Sie die Bedingungen hinzu:      
    * Abgelaufene Gerätegarantie entspricht 1
    * Wassertemperatur ist größer als die maximale Temperature Kaffeemaschinen

1. Hinzufügen einer **Aktion**, einen Bildlauf nach unten im Bereich Telemetriedaten Regel konfigurieren, und wählen Sie **+** neben Aktionen, und wählen Sie dann **-e-Mail**.

1. Um die Aktion zu definieren, fügen Sie die E-Mail-Adresse hinzu, die Sie für die Anmeldung bei der IoT Central-Anwendung verwendet haben. Fügen Sie die Benachrichtigungsmeldung für die zu hohe Wassertemperatur hinzu: „Das Wasser in der Kaffeemaschine ist zu heiß. Wartung erforderlich.  Die Garantie ist abgelaufen.“ Wiederholen Sie die gleichen Schritte für die zu kalte Wassertemperatur. Fügen Sie die Nachricht hinzu: „Das Wasser in der Kaffeemaschine ist zu kalt. Wartung erforderlich.  Die Garantie ist abgelaufen.“

1. Wählen Sie **Speichern** aus. Die Regel wird auf der Seite Regeln aufgeführt.

1. Damit die Regel ausgelöst wird, legen Sie die optimale Temperatur in den Einstellungen außerhalb des Bereichs, die Sie unter Eigenschaften angegeben. Sobald Sie mit der Überprüfung fertig sind, deaktivieren Sie die Regeln, um zu vermeiden, Ihren Posteingang mit e-Mails überfluten. 

## <a name="create-rules-in-iot-central-with-microsoft-flow-as-the-action"></a>Erstellen von Regeln in IoT Central mit Microsoft Flow als Aktion

Microsoft Flow automatisiert Workflows übergreifend über viele Anwendungen hinweg. Es ist eine der Aktionen, die durch Auslösen einer Regel in IoT Central eingeleitet werden können. In diesem Szenario sendet Microsoft Flow eine SMS-Benachrichtigung an einen lokalen Techniker, wenn die Kaffeemaschine einen bestimmten Temperaturschwellenwert erreicht und noch der Garantie unterliegt. Navigieren Sie zu **Regeln**, um Bedingungen zu konfigurieren und einen Flow als Aktion hinzuzufügen, wenn die Regel ausgelöst wird. 
 
> [!NOTE]
> Diese Übung ist optional, wenn Sie nicht über ein Azure-Abonnement verfügen, mit dem Sie Microsoft Flow aktivieren können.


### <a name="extend-your-iot-central-trial-to-30-days"></a>Verlängern Sie Ihre IoT Central-Testversion auf 30 Tage

1. Um Microsoft Flow zu aktivieren, müssen Sie sich zum Verlängern des Testzeitraums um 30 Tage. Wählen Sie zu diesem Zweck **Testversion auf 30 Tage verlängern** wählen Sie auf der Seite "Abrechnung" eine Azure Active Directory und Azure-Abonnement. Mit einem Azure-Abonnement können Sie Instanzen von Azure-Diensten erstellen. Azure IoT Central sucht automatisch nach allen Azure-Abonnements, auf die Sie Zugriff haben, und zeigt sie im Dropdownmenü an.
    
1. Wenn Sie kein Azure-Abonnement besitzen, können Sie auf der Seite [Azure-Registrierungsseite](https://aka.ms/createazuresubscription) ein Abonnement erstellen. Nachdem Sie das Azure-Abonnement erstellt haben, navigieren Sie zurück zu den **Anwendungsmanager** Seite. Ihr neues Abonnement wird in der Dropdownliste **Azure-Abonnement** angezeigt.
        

### <a name="add-the-following-rules-when-the-coffee-machine-is-under-warranty"></a>Fügen Sie die folgenden Regeln hinzu, wenn für die Kaffeemaschine noch Garantie gilt. 

1. Benennen Sie die Regel: Wasser in Kaffeemaschine zu kalt (Garantie)

    Fügen Sie die Bedingungen hinzu:      
    * Abgelaufene Gerätegarantie entspricht 0
    * Wassertemperatur ist kleiner als Kaffeemaschinen Min Temperatur

1. Benennen Sie die Regel: Wasser in Kaffeemaschine zu heiß (Garantie)

    Fügen Sie die Bedingungen hinzu:      
    * Abgelaufene Gerätegarantie entspricht 0
    * Wassertemperatur ist größer als die maximale Temperature Kaffeemaschinen

1. Nachdem Sie die Regelbedingungen gespeichert haben, wählen Sie Microsoft Flow als neue Aktion aus, wenn für die Kaffeemaschine noch Garantie gilt. In Ihrem Browser sollte eine neue Registerkarte oder ein neues Fenster geöffnet werden, um Ihnen den Zugang zu Microsoft Flow zu ermöglichen. Sie gelangen auf eine Übersichtsseite, auf der ein IoT Central-Connector angezeigt wird, der eine Verbindung mit einer benutzerdefinierten Aktion herstellt. Klicken Sie auf **Weiter**. 

    Sie werden an den Microsoft Flow-Designer weitergeleitet, um Ihren Workflow zu erstellen. Der Workflow verfügt über einen IoT Central-Auslöser, in den Ihre Anwendung und Regel bereits eingetragen sind.

    An diesem Punkt können Sie Ihrem Workflow eine beliebige Aktion hinzufügen. Als Beispiel senden wir eine Mobiltelefonbenachrichtigung. Suchen Sie nach „Benachrichtigung“, und wählen Sie „Benachrichtigungen – Mobiltelefonbenachrichtigung an mich senden“ aus.

    Füllen Sie in der Aktion das Feld „Text“ mit dem Inhalt der Benachrichtigung aus. Sie können dynamische Inhalte aus Ihrer IoT Central-Regel einschließen, um wichtige Informationen wie die Geräte-ID und den Namen des Geräts zu übergeben.
    
    ![Verwenden von Microsoft Flow als Aktion](../images/5-flow-b.png)

1. Sobald Sie den Workflow in Microsoft Flow eingerichtet haben, laden Sie die [Flow-App](https://www.microsoft.com/en-us/p/microsoft-flow/9nkn0p5l9n84?activetab=pivot%3aoverviewtab) aus dem Microsoft Store auf Ihr mobiles Gerät herunter. Melden Sie sich mit dem gleichen Konto an, das Sie verwendet haben, um den Flow in der Flow-Web-App einzurichten. Legen Sie zu Testzwecken die optimale Temperatur außerhalb des gültigen Bereichs, um die Regel ein. 

    > [!NOTE]
    > Geräteeigenschaft: Gerätegarantie abgelaufen (1 für abgelaufen oder 0 für unter Garantie im Gerätecode) wird vom Gerät nach dem Zufallsprinzip generiert und dann vom Gerät an die Azure IoT Central-Anwendung gesendet. Für Testzwecke verwendet werden, wenn Sie Geräte Garantie abgelaufen ist (1 oder 0) steuern möchten, neu starten Sie Ihrer Kaffeemaschine bis Sie den Zustand vorgesehenen Garantie für die Aktion auszulösen, die Sie testen empfangen. Um eine Benachrichtigung auf Ihrem Mobilgerät zu erhalten, starten Sie Ihre Kaffeemaschine neu, bis Sie sehen, dass Geräte Gewährleistung abgelaufen 0 in das Konsolenprotokoll. 

    Nach einigen Minuten werden Sie in der mobilen Flow-app Benachrichtigungen angezeigt.

    ![Verwenden von Microsoft Flow als Aktion](../images/5-flow-c.png)

## <a name="summary"></a>Zusammenfassung
Sie haben das Erstellen von Regeln in IoT Central gelernt und Aktionen wie das Senden einer E-Mail oder einer SMS-Benachrichtigung mithilfe von Microsoft Flow beim Auslösen der Regel ausgelöst. Wenn die Wassertemperatur die Kaffeemaschine außerhalb des Bereichs optimal ist, werden Benachrichtigungen in diesem Fall entweder einen Servicetechniker oder des Clients abhängig vom Status der Garantie gesendet. 


