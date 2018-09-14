Ihr im Bankensektor tätiges Unternehmen arbeitet mit äußerst sensiblen Kundeninformationen und möchte sicherstellen, dass die VM-Datenträger jederzeit (also auch bei der Bereitstellung) verschlüsselt sind. Sie wurden damit beauftragt, eine sichere VM-Bereitstellung zu automatisieren, um die Daten Ihres Unternehmens zu schützen.

In dieser Einheit verwenden Sie eine Azure Resource Manager-Vorlage automatisch Aktivieren der Verschlüsselung für neue Windows-VMs.

## <a name="configure-and-deploy-a-new-vm-using-an-azure-resource-manager-template"></a>Konfigurieren und Bereitstellen eines neuen virtuellen Computers mit einer Azure Resource Manager-Vorlage

1. Navigieren Sie zur [Resource Manager-Vorlage auf GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image), und klicken Sie auf **Deploy to Azure** (In Azure bereitstellen).
1. Im Azure-Portal auf der **Azure-schnellstartvorlage** Blatt unter **Ressourcengruppe**Option **vorhandene**. Wählen Sie in der Liste **Moneyapprg**.
1. Geben Sie im Abschnitt **EINSTELLUNGEN** folgende Informationen ein:

   - VM-Name: **moneyappsvr02**
   - **Admin Username**: identisch mit der Sie in der vorherigen Übung verwendet.
   - **Administratorkennwort**: identisch mit der Sie in der vorherigen Übung verwendet.
   - **Name des neuen Speicherkontos**: Geben Sie einen eindeutigen Namen.
   - **Größe des virtuellen Computers**: Ersetzen Sie dies durch die gleiche Größe, die Sie in der vorherigen Übung, z. B. verwendet **Standard_B1s** (wie Sie die gleiche Azure-Region verwenden, sicherzustellen, dass Größe in Ihrer aktuellen Region verfügbar ist).
   - **Name des virtuellen Netzwerks**: **moneyapprg-vnet**
   - **Subnetzname**: **default**
   - **AAD-Client-ID**: Kopieren aus den Informationen, die Sie in den Editor eingefügt haben.
   - **AAD-Client-Geheimnis**: Kopieren aus den Informationen, die Sie in den Editor eingefügt haben.
   - **Schlüsseltresorname**: **moneyappkv**
   - **Key Vault-Ressourcengruppe**: **moneyapprg**
   - **Key Encryption Key-URL**: Kopieren aus den Informationen, die Sie in den Editor eingefügt haben.
1. Aktivieren Sie das Kontrollkästchen **Ich stimme den oben genannten Geschäftsbedingungen zu**, und klicken Sie anschließend auf **Kaufen**.

Die Bereitstellung dauert 5 bis 10 Minuten in Anspruch.

## <a name="verify-encryption-status-of-new-vm"></a>Überprüfen des Verschlüsselungsstatus des neuen virtuellen Computers

1. Klicken Sie im Azure-Portal auf der Seitenleiste auf **Virtuelle Computer**.

1. Klicken Sie auf dem Blatt **Virtuelle Computer** auf **moneyappsvr02**.

1. Klicken Sie auf dem Blatt **Virtueller Computer** unter **EINSTELLUNGEN** auf **Datenträger**.

1. Wie Sie auf dem Blatt **Datenträger** sehen, hat der Betriebssystemdatenträger den Verschlüsselungsstatus **Aktiviert**.
