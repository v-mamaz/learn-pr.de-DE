Ihr im Bankensektor tätiges Unternehmen arbeitet mit äußerst sensiblen Kundeninformationen und möchte sicherstellen, dass die VM-Datenträger jederzeit (also auch bei der Bereitstellung) verschlüsselt sind. Sie wurden damit beauftragt, eine sichere VM-Bereitstellung zu automatisieren, um die Daten Ihres Unternehmens zu schützen.

In dieser Einheit verwenden Sie eine Azure Resource Manager-Vorlage, um die Verschlüsselung für neue virtuelle Windows-Computer automatisch zu aktivieren.

## <a name="configure-and-deploy-a-new-vm-using-an-azure-resource-manager-template"></a>Konfigurieren und Bereitstellen eines neuen virtuellen Computers mithilfe einer Azure Resource Manager-Vorlage

1. Navigieren Sie zur [Resource Manager-Vorlage auf GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image), und klicken Sie auf **Deploy to Azure** (In Azure bereitstellen).
1. Klicken Sie im Azure-Portal auf dem Blatt **Azure-Schnellstartvorlage** unter **Ressourcengruppe** auf **Vorhandene verwenden**. Wählen Sie in der Liste **moneyapprg** aus.
1. Geben Sie im Abschnitt **EINSTELLUNGEN** folgende Informationen ein:

   - VM-Name: **moneyappsvr02**
   - **Administratorbenutzername:** Verwenden Sie den gleichen Wert wie in der vorherigen Übung.
   - **Administratorkennwort:** Verwenden Sie den gleichen Wert wie in der vorherigen Übung.
   - **Neuer Speicherkontoname:** Geben Sie einen eindeutigen Namen ein.
   - **VM-Größe:** Ersetzen Sie diesen Wert durch die Größe aus der vorherigen Übung – also beispielsweise durch **Standard_B1s**. (Da Sie die gleiche Azure-Region verwenden, vergewissern Sie sich, dass die Größe in Ihrer aktuellen Region verfügbar ist.)
   - **Name des virtuellen Netzwerks:** **moneyapprg-vnet**
   - **Subnetzname:** **Standard**
   - **AAD-Client-ID:** Kopieren Sie die entsprechende Angabe aus den Informationen, die Sie in den Editor eingefügt haben.
   - **AAD-Clientgeheimnis**: Kopieren Sie die entsprechende Angabe aus den Informationen, die Sie in den Editor eingefügt haben.
   - **Schlüsseltresorname**: **moneyappkv**
   - **Key Vault-Ressourcengruppe**: **moneyapprg**
   - **Key Encryption Key URL** (URL des Schlüssels zur Schlüsselverschlüsselung): Kopieren Sie die entsprechende Angabe aus den Informationen, die Sie in den Editor eingefügt haben.
1. Aktivieren Sie das Kontrollkästchen **Ich stimme den oben genannten Geschäftsbedingungen zu**, und klicken Sie anschließend auf **Kaufen**.

Die Bereitstellung kann fünf bis zehn Minuten dauern.

## <a name="verify-encryption-status-of-new-vm"></a>Überprüfen des Verschlüsselungsstatus des neuen virtuellen Computers

1. Klicken Sie im Azure-Portal auf der Seitenleiste auf **Virtuelle Computer**.

1. Klicken Sie auf dem Blatt **Virtuelle Computer** auf **moneyappsvr02**.

1. Klicken Sie auf dem Blatt **Virtueller Computer** unter **EINSTELLUNGEN** auf **Datenträger**.

1. Wie Sie auf dem Blatt **Datenträger** sehen, hat der Betriebssystemdatenträger den Verschlüsselungsstatus **Aktiviert**.
