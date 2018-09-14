Nun, da Sie einen Überblick darüber, wie Azure IoT Hub von IoT-Geräten wie Raspberry Pi werden Daten erfasst haben können Sie jetzt fortfahren andere IoT-Geräte senden ihre Daten auch bereitstellen. Abschluss des Setups von IoT-Geräten in einem kleinen Projekt (1-5-Geräte) kann eine 1: 1 durchgeführt werden. Größere Bereitstellungen benötigt eine bessere Methode für die Bereitstellung.

Azure IoT Hub Device Provisioning-Dienst können Kunden so konfigurieren Sie die Bereitstellung von Zero Touch-Geräten mit Azure IoT Hub, und es wird die Skalierbarkeit der Cloud mit einmal ein lang andauernder eine-at-a-Time-Vorgang. Der Prozess wurde mit den Herausforderungen bei der Erhöhung der lieferkettenkosten er stellt die Infrastruktur zum Bereitstellen von Millionen von Geräten auf sichere und skalierbare Weise entworfen.

Automatische Bereitstellung von Geräten mit dem Device Provisioning-Dienst jetzt unterstützt alle Protokolle, die IoT Hub-Instanz einschließlich HTTP, AMQP, MQTT, AMQP über Websockets und MQTT über Websockets unterstützt. Diese Version bezieht sich auch um erweiterte SDK-sprachunterstützung für das Gerät und die Client-Seite.

## <a name="link-the-device-provisioning-service-to-an-iot-hub"></a>Verknüpfen des Device Provisioning-Diensts mit einer IoT Hub-Instanz

Der nächste Schritt besteht darin, den Device Provisioning-Dienst und IoT Hub zu verknüpfen, damit der IoT Hub Device Provisioning-Dienst bei diesem Hub Geräte registrieren kann. Der Dienst kann nur Geräte mit IoT Hubs bereitstellen, die mit dem Device Provisioning-Dienst verknüpft wurden. Führen Sie folgende Schritte durch:

1.  In der **alle Ressourcen** Seite im Azure-Portal, klicken Sie auf der Device Provisioning-Dienstinstanz, die Sie zuvor erstellt haben.

2.  Klicken Sie auf der Seite „Device Provisioning-Dienst“ auf **Verknüpfte IoT Hubs**.

3.  Klicken Sie auf **Hinzufügen**.

4.  Geben Sie auf der Seite **Verknüpfung zu IoT Hub hinzufügen** die folgenden Informationen ein, und klicken Sie auf **Speichern**:

    - **Abonnement:** Stellen Sie sicher, dass das Abonnement mit der IoT Hub-Instanz ausgewählt ist. Sie können eine Verknüpfung mit einer IoT Hub-Instanz erstellen, die in einem anderen Abonnement enthalten ist.

    - **IoT Hub:** Wählen Sie den Namen der IoT Hub-Instanz aus, die Sie mit dieser Device Provisioning Service-Instanz verknüpfen möchten.

    - **Zugriffsrichtlinie:** Wählen Sie **iothubowner** als Anmeldeinformationen zum Erstellen der Verknüpfung mit der IoT Hub-Instanz aus.

![Verknüpfen des Hubnamens mit dem DPS im Portal](../media-draft/ee6e78754a1d39d86de71fb6872723f3.png)

## <a name="set-the-allocation-policy-on-the-device-provisioning-service"></a>Festlegen der Zuordnungsrichtlinie im Device Provisioning-Dienst

Die Zuordnungsrichtlinie ist eine Einstellung des IoT Hub Device Provisioning-Diensts, die festlegt, wie Geräte einer IoT Hub-Instanz zugewiesen werden. Es gibt drei unterstützte Zuordnungsrichtlinien:

1. **Niedrigste Latenz**: Geräte werden basierend auf dem Hub mit der geringsten Latenz auf dem Gerät für eine IoT Hub-Instanz bereitgestellt.

2. **Gleichmäßig gewichtete Verteilung** (Standard): Bei verknüpften IoT Hubs ist die Wahrscheinlichkeit gleich hoch, dass ihnen Geräte bereitgestellt werden. Dies ist die Standardeinstellung. Wenn Sie nur für eine IoT Hub-Instanz Geräte bereitstellen, können Sie diese Einstellung beibehalten.

3. **Statische Konfiguration über die Registrierungsliste**: Die Angabe der gewünschten IoT Hub-Instanz in der Registrierungsliste hat gegenüber der Zuordnungsrichtlinie auf Ebene des Device Provisioning-Diensts Vorrang.

Klicken Sie zum Festlegen der Zuordnungsrichtlinie auf der Seite „Device Provisioning-Dienst“ auf **Zuordnungsrichtlinie verwalten**. Stellen Sie sicher, dass die Zuordnungsrichtlinie auf **Gleichmäßig gewichtete Verteilung** (Standard) festgelegt ist. Wenn Sie Änderungen vornehmen, klicken Sie danach auf **Speichern**.

![Verwalten von Zuordnungsrichtlinien](../media-draft/0c5fa5193156f17b4f5d64aab65a414d.png)

## <a name="enroll-the-device"></a>Registrieren des Geräts

Bei diesem Schritt werden die einzigartigen Sicherheitsartefakte des Geräts zum Device Provisioning-Dienst hinzugefügt. Diese Sicherheitsartefakte basieren auf dem [Nachweismechanismus](https://docs.microsoft.com/azure/iot-dps/concepts-device#attestation-mechanism) des Geräts:

Für TPM-basierte Geräte benötigen Sie Folgendes:

- Der *Endorsement Key* ist für jeden TPM-Chip bzw. jede Simulation eindeutig, und Sie erhalten ihn vom Hersteller des TPM-Chips. Weitere Informationen finden Sie im Artikel [Grundlegendes zum TPM Endorsement Key](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation#terminology).

- Die *Registrierungs-ID*, die zur eindeutigen Identifizierung eines Geräts im Namespace/Bereich verwendet wird. Diese ID ist eventuell mit der Geräte-ID identisch. Die ID ist für jedes Gerät erforderlich. Bei TPM-basierten Geräten kann die Registrierungs-ID vom TMP selbst abgeleitet werden, z.B. ein SHA-256-Hash des TPM Endorsement Key.

![Registrierungsinformationen für das TPM im Portal](../media-draft/11db90b7128e1cf222a4da45de7cbac8.png)

Für X.509-basierte Geräte benötigen Sie Folgendes:

- Das [für den X.509-Chip oder die X.509-Simulation ausgestellte Zertifikat](https://docs.microsoft.com/windows/desktop/SecCertEnroll/about-x-509-public-key-certificates) in Form einer *PEM*- oder *CER*-Datei. Für die individuelle Registrierung müssen Sie die pro-Gerät verwenden *Signaturzertifikat* für Ihr x. 509-System, für Registrierungsgruppen, dagegen müssen Sie verwenden die *Stammzertifikat*.

   ![Hinzufügen einer individuellen Registrierung für den x. 509-Nachweis im portal](../media-draft/8d56752f453f27e55dd15b7c894ae406.png)

Es gibt zwei Möglichkeiten zum Registrieren des Geräts beim Device Provisioning-Dienst:

- **Registrierungsgruppen** Diese stellen Gruppen von Geräten dar, die einen bestimmten Nachweismechanismus gemeinsam nutzen. Es wird empfohlen, eine Registrierungsgruppe für eine große Anzahl von Geräten, die eine gewünschte Erstkonfiguration gemeinsam nutzen, oder für Geräte zu verwenden, die alle demselben Mandanten zugeordnet sind. Weitere Informationen zum Identitätsnachweis für Registrierungsgruppen finden Sie unter [Sicherheit](https://docs.microsoft.com/azure/iot-dps/concepts-security#controlling-device-access-to-the-provisioning-service-with-x509-certificates).

   ![Hinzufügen einer gruppenregistrierung für x. 509-Nachweis im portal](../media-draft/4a9d9ea822887c70f1ff1e4b64b138f1.png)

- **Individuelle Registrierungen** Diese stellen Einträge für ein einzelnes Gerät dar, das beim Device Provisioning-Dienst registriert werden kann. Individuelle Registrierungen verwenden entweder X.509-Zertifikate oder SAS-Token (in einem physischen oder virtuellen TPM) als Nachweismechanismen. Individuelle Registrierungen sollten für Geräte, die besondere Erstkonfigurationen erfordern, und für Geräte verwendet werden, die nur SAS-Token über das TPM oder das virtuelle TPM als Nachweismechanismus verwenden können. Bei individuellen Registrierungen ist möglicherweise die gewünschte IoT Hub-Geräte-ID angegeben.

Nun registrieren Sie das Gerät mithilfe der erforderlichen Sicherheitsartefakte basierend auf dem Nachweismechanismus des Geräts bei der Device Provisioning-Dienstinstanz:

1. Melden Sie sich beim Azure-Portal an, klicken Sie im Menü auf der linken Seite auf die Schaltfläche **Alle Ressourcen**, und öffnen Sie Ihren Device Provisioning-Dienst.

2. Wählen Sie auf dem Zusammenfassungsblatt des Device Provisioning-Diensts die Option **Registrierungen verwalten** aus. Wählen Sie je nach Ihrer Geräteinstallation entweder die Registerkarte **Individuelle Registrierungen** oder **Registrierungsgruppen**. Klicken Sie ganz oben auf die Schaltfläche **Hinzufügen**. Wählen Sie **TPM** oder **x. 509** als Nachweis der Identität *Mechanismus*, und geben Sie die entsprechenden sicherheitsartefakte, wie oben beschrieben. Sie können eine neue **IoT Hub-Geräte-ID** eingeben. Klicken Sie abschließend auf die Schaltfläche **Speichern**.

3. Wenn das Gerät erfolgreich registriert ist, sollte es wie folgt im Portal angezeigt werden:

![Erfolgreiche TPM-Registrierung im Portal](../media-draft/cb277b2e5bc21cd02669775d536e89c0.png)

Nach der Registrierung wartet der Bereitstellungsdienst, bis das Gerät gestartet und zu einem beliebigen Zeitpunkt eine Verbindung mit diesem hergestellt wird. Wenn Ihr Gerät zum ersten Mal gestartet wird, interagiert die Client-SDK-Bibliothek zur Extraktion der Sicherheitsartefakte vom Gerät mit Ihrem Chip und überprüft die Registrierung bei Ihrem Device Provisioning-Dienst.

## <a name="start-the-iot-device"></a>Starten des IoT-Geräts

Bei Ihrem IoT-Gerät kann es sich um ein echtes Gerät oder ein simuliertes Gerät handeln. Da das IoT-Gerät jetzt bei einer Device Provisioning Service-Instanz registriert ist, kann es nun gestartet werden und zur Erkennung mithilfe des Nachweismechanismus den Bereitstellungsdienst aufrufen. Nach der Erkennung des Geräts durch den Bereitstellungsdienst wird es einem IoT-Hub hinzugefügt.

Simuliertes Gerät Beispiele, die sowohl "TPM" und "x. 509-Nachweis für C, Java, C enthalten sind\#, Node.js und Python. Für ein simuliertes Gerät, das TPM und das [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c) verwendet, wird beispielsweise der im Abschnitt [Simulieren der ersten Startsequenz für das Gerät](https://docs.microsoft.com/azure/iot-dps/quick-create-simulated-device#simulate-first-boot-sequence-for-the-device) erläuterte Prozess ausgeführt. Das gleiche Gerät bezieht sich bei Verwendung des X.509-Zertifikats auf diesen Abschnitt zur [Startsequenz](https://docs.microsoft.com/azure/iot-dps/quick-create-simulated-device-x509#simulate-first-boot-sequence-for-the-device).

Ein Beispiel für ein echtes Gerät finden Sie unter [Verwenden der automatischen Bereitstellung des Azure IoT Hub Device Provisioning Service zum Registrieren des MXChip IoT DevKit bei IoT Hub](https://docs.microsoft.com/azure/iot-dps/how-to-connect-mxchip-iot-devkit).

Starten Sie das Gerät, damit die Clientanwendung Ihres Geräts mit der Registrierung bei Ihrer Device Provisioning Service-Instanz beginnen kann.

## <a name="verify-the-device-is-registered"></a>Sicherstellen, dass das Gerät registriert ist

Nach dem Starten Ihres Geräts sollten die folgenden Aktionen ausgeführt werden:

1. Das Gerät sendet eine Registrierungsanforderung an Ihren Device Provisioning-Dienst.

2. Bei TPM-Geräten sendet der Device Provisioning-Dienst eine Registrierungsherausforderung zurück, auf die Ihr Gerät antwortet.

3. Nach erfolgreicher Registrierung sendet der Device Provisioning-Dienst den IoT Hub-URI, die Geräte-ID und den verschlüsselten Schlüssel an das Gerät zurück.

4. Die IoT Hub-Clientanwendung auf dem Gerät stellt dann eine Verbindung mit Ihrem Hub her.

5. Nachdem eine Verbindung mit dem Hub hergestellt wurde, sollte das Gerät im IoT Hub-Explorer für **IoT-Geräte** angezeigt werden.

![Erfolgreiche Herstellung einer Verbindung mit dem Hub im Portal](../media-draft/12ea6da6eef9bf96be6bd80aa1721173.png)

<!--Reference links

-   <https://docs.microsoft.com/en-us/azure/iot-dps/tutorial-set-up-cloud>

-   <https://docs.microsoft.com/en-us/azure/iot-dps/tutorial-provision-device-to-hub>-->