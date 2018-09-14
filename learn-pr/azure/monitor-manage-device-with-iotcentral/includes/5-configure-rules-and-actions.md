Sie haben Ihre Kaffeemaschine mit der Azure IoT Central-Anwendung verbunden und so den Austausch von Daten aktiviert, mit deren Hilfe Sie Ihre Kaffeemaschine überwachen und verwalten können. In dieser Übungseinheit erstellen Sie Regeln, die Aktionen auslösen, wenn die Wassertemperatur der Kaffeemaschine außerhalb des normalen Bereichs liegt. Die Aktionen sind entweder E-Mails oder SMS-Benachrichtigungen, je nachdem, ob für die Maschine noch Garantie gilt oder nicht. Um Microsoft Flow als Aktion hinzuzufügen, benötigen Sie ein Azure-Abonnement. Wenn Sie nicht über ein Azure-Abonnement verfügen, ist das Hinzufügen von Microsoft Flow als Aktion optional.

## <a name="create-rules-in-iot-central-with-email-as-the-action"></a>Erstellen von Regeln in IoT Central mit E-Mail als Aktion
Azure IoT Central kann Benachrichtigungen mithilfe seiner nativen E-Mail-Funktion senden. In diesem Szenario wird, wenn die Kaffeemaschine außerhalb des optimalen Temperaturbereichs liegt und nicht durch Garantie geschützt ist, eine E-Mail von IoT Central an die Wartungsabteilung des Kunden gesendet.

Fügen Sie die folgenden zwei Regeln hinzu, wenn die Garantie der Kaffeemaschine abgelaufen ist und die Wassertemperatur außerhalb des optimalen Bereichs liegt. Wählen Sie abschließend **Speichern** aus. 

> [!NOTE]
> Wenn die Bedingungen angewendet werden, müssen alle Aussagen wahr sein, damit die Regeln ausgeführt werden. Wenn Ihre Bedingung eine „Oder“-Aussage ist, wie in diesem Szenario (z. B. die optimale Temperatur ist unterhalb von 90° Celsius oder oberhalb von 98° Celsius bei abgelaufener Garantie), teilen Sie die Aussage in zwei Regeln auf, wie hier dargestellt.

1. Benennen Sie die Regel: Wasser in Kaffeemaschine zu kalt (abgelaufen)

    Fügen Sie die Bedingungen hinzu:      
    * Abgelaufene Gerätegarantie entspricht 1
    * Die Wassertemperatur liegt unterhalb der niedrigsten Temperatur der Kaffeemaschine ![Regel anwenden](../images/5-flow-g.png)

1. Benennen Sie die Regel: Wasser in Kaffeemaschine zu heiß (abgelaufen)

    Fügen Sie die Bedingungen hinzu:      
    * Abgelaufene Gerätegarantie entspricht 1
    * Die Wassertemperatur liegt oberhalb der höchsten Temperatur der Kaffeemaschine ![Regel anwenden](../images/5-flow-k.png)     

1. Scrollen Sie zum Hinzufügen einer Aktion im Bereich Configure Telemetry Rule (Telemetrieregel konfigurieren) nach unten, und klicken Sie neben **Aktionen** auf das Pluszeichen (+) und dann auf **E-Mail**.

1. Um die Aktion zu definieren, fügen Sie die E-Mail-Adresse hinzu, die Sie für die Anmeldung bei der IoT Central-Anwendung verwendet haben. Fügen Sie die Benachrichtigungsmeldung für die zu hohe Wassertemperatur hinzu: „Das Wasser in der Kaffeemaschine ist zu heiß. Wartung erforderlich.  Die Garantie ist abgelaufen.“ Wiederholen Sie die gleichen Schritte für die zu kalte Wassertemperatur. Fügen Sie die Nachricht hinzu: „Das Wasser in der Kaffeemaschine ist zu kalt. Wartung erforderlich.  Die Garantie ist abgelaufen.“

1. Wählen Sie **Speichern** aus. Ihre Regel ist auf der Seite Regeln aufgeführt:

1. Um die Regel auszulösen, können Sie warten, bis die Temperatur den Bereich verlässt, oder Sie können die Temperatur in den Einstellungen außerhalb des optimalen Bereichs einstellen. Sobald Sie beginnen, E-Mail-Benachrichtigungen zu erhalten, denken Sie daran, die Regel zu deaktivieren, um einen Ansturm auf Ihren Posteingang mit E-Mails von Azure IoT Central zu vermeiden. 

> [!NOTE]
> Deaktivieren Sie die Regeln, sobald Sie die Überprüfung abgeschlossen haben, um ein Fluten Ihres Posteingangs mit E-Mails zu vermeiden. 

## <a name="create-rules-in-iot-central-with-microsoft-flow-as-the-action"></a>Erstellen von Regeln in IoT Central mit Microsoft Flow als Aktion

Microsoft Flow automatisiert Workflows übergreifend über viele Anwendungen hinweg. Es ist eine der Aktionen, die durch Auslösen einer Regel in IoT Central eingeleitet werden können. In diesem Szenario sendet Microsoft Flow eine SMS-Benachrichtigung an einen lokalen Techniker, wenn die Kaffeemaschine einen bestimmten Temperaturschwellenwert erreicht und noch der Garantie unterliegt. Navigieren Sie zu **Regeln**, um Bedingungen zu konfigurieren und einen Flow als Aktion hinzuzufügen, wenn die Regel ausgelöst wird. 
 
> [!NOTE]
> Diese Übung ist optional, wenn Sie nicht über ein Azure-Abonnement verfügen, mit dem Sie Microsoft Flow aktivieren können.

Fügen Sie die folgenden Regeln hinzu, wenn für die Kaffeemaschine noch Garantie gilt. 

1. Benennen Sie die Regel: Wasser in Kaffeemaschine zu kalt (Garantie)

    Fügen Sie die Bedingungen hinzu:      
    * Abgelaufene Gerätegarantie entspricht 0
    * Die Wassertemperatur liegt unterhalb der niedrigsten Temperatur der Kaffeemaschine ![Regel anwenden](../images/5-flow-l.png)

1. Benennen Sie die Regel: Wasser in Kaffeemaschine zu heiß (Garantie)

    Fügen Sie die Bedingungen hinzu:      
    * Abgelaufene Gerätegarantie entspricht 0
    * Die Wassertemperatur liegt oberhalb der höchsten Temperatur der Kaffeemaschine ![Regel anwenden](../images/5-flow-h.png)

1. Nachdem Sie die Regelbedingungen gespeichert haben, wählen Sie Microsoft Flow als neue Aktion aus, wenn für die Kaffeemaschine noch Garantie gilt. In Ihrem Browser sollte eine neue Registerkarte oder ein neues Fenster geöffnet werden, um Ihnen den Zugang zu Microsoft Flow zu ermöglichen. Sie gelangen auf eine Übersichtsseite, auf der ein IoT Central-Connector angezeigt wird, der eine Verbindung mit einer benutzerdefinierten Aktion herstellt. Klicken Sie auf **Weiter**. 

    Sie werden an den Microsoft Flow-Designer weitergeleitet, um Ihren Workflow zu erstellen. Der Workflow verfügt über einen IoT Central-Auslöser, in den Ihre Anwendung und Regel bereits eingetragen sind.

    An diesem Punkt können Sie Ihrem Workflow eine beliebige Aktion hinzufügen. Als Beispiel senden wir eine Mobiltelefonbenachrichtigung. Suchen Sie nach „Benachrichtigung“, und wählen Sie „Benachrichtigungen – Mobiltelefonbenachrichtigung an mich senden“ aus.

    Füllen Sie in der Aktion das Feld „Text“ mit dem Inhalt der Benachrichtigung aus. Sie können dynamische Inhalte aus Ihrer IoT Central-Regel einschließen, um wichtige Informationen wie die Geräte-ID und den Namen des Geräts zu übergeben.
    ![Verwenden von Microsoft Flow als Aktion](../images/5-flow-f.png)

1. Sobald Sie den Workflow in Microsoft Flow eingerichtet haben, laden Sie die [Flow-App](https://www.microsoft.com/en-us/p/microsoft-flow/9nkn0p5l9n84?activetab=pivot%3aoverviewtab) aus dem Microsoft Store auf Ihr mobiles Gerät herunter. Melden Sie sich mit dem gleichen Konto an, das Sie verwendet haben, um den Flow in der Flow-Web-App einzurichten. Legen Sie für Testzwecke die optimale Temperatur außerhalb des Bereichs fest, um die Regel auszulösen. 

    > [!NOTE]
    > Geräteeigenschaft: Gerätegarantie abgelaufen (1 für abgelaufen oder 0 für unter Garantie im Gerätecode) wird vom Gerät nach dem Zufallsprinzip generiert und dann vom Gerät an die Azure IoT Central-Anwendung gesendet. Wenn Sie für Testzwecke den Ablauf der Gerätegarantie steuern möchten (1 oder 0), starten Sie den Simulator erneut, bis Sie den gewünschten Garantiestatus erhalten, um die zu testende Aktion auszulösen. Um eine Benachrichtigung auf Ihrem mobilen Gerät zu erhalten, starten Sie den Simulator neu, bis Sie sehen, dass der Ablauf der Gerätegarantie im Protokoll der Konsole „0“ ist. 

    Nach einigen Minuten wird die Benachrichtigung in der mobilen Flow-App angezeigt.

    ![Verwenden von Microsoft Flow als Aktion](../images/5-flow-a.png)

## <a name="summary"></a>Zusammenfassung
Sie haben das Erstellen von Regeln in IoT Central gelernt und Aktionen wie das Senden einer E-Mail oder einer SMS-Benachrichtigung mithilfe von Microsoft Flow beim Auslösen der Regel ausgelöst. In diesem Fall werden, wenn die Wassertemperatur der Kaffeemaschine außerhalb des optimalen Bereichs liegt, Benachrichtigungen entweder an einen Reparaturtechniker oder den Kunden gesendet, abhängig vom Garantiestatus des Geräts. 


