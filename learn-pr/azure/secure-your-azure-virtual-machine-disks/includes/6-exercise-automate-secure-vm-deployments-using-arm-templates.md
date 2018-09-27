In dieser Einheit verwenden Sie eine Azure Resource Manager-Vorlage, um den virtuellen Windows-Computer zu entschlüsseln, den Sie zuvor erstellt haben. Sie haben das Betriebssystemlaufwerk Ihres virtuellen Windows-Computers verschlüsselt. Da sich auf dem Betriebssystemlaufwerk allerdings keine vertraulichen Informationen befinden, können Sie es eigentlich auch unverschlüsselt lassen. Sie verwenden daher eine Vorlage, um lediglich das Betriebssystemlaufwerk zu entschlüsseln.

## <a name="configure-and-deploy-a-new-vm-using-an-azure-resource-manager-template"></a>Konfigurieren und Bereitstellen eines neuen virtuellen Computers mithilfe einer Azure Resource Manager-Vorlage

Mithilfe einer Vorlage, die Microsoft auf Github veröffentlicht hat, erstellen wir einen neuen virtuellen Computer mit standardmäßig aktivierter Verschlüsselung.

1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) mit dem Konto an, mit dem Sie die Sandbox aktiviert haben.

1. Klicken Sie auf der linken Seitenleiste auf **Ressource erstellen**.

1. Geben Sie **Vorlage** in das Suchfeld ein.

1. Wählen Sie in der Liste mit den Ergebnissen die Option **Vorlagenbereitstellung** aus, und klicken Sie anschließend auf **Erstellen**.

    ![Screenshot, auf dem das Element „Vorlagenbereitstellung“ ausgewählt und die Schaltfläche „Erstellen“ hervorgehoben ist.](../media/6-create-template.png)

1. Geben Sie „201-decrypt“ in das **Vorlagenauswahlfeld**ein, und wählen Sie die Vorlage „201-decrypt-running-windows-vm-without-aad“ aus.

    ![Screenshot des Vorlagenauswahlfelds mit automatischer Vervollständigung.](../media/6-custom-deployment.png)

1. Klicken Sie auf **Vorlage auswählen**, um die Vorlagenausführung zu starten.

1. Geben Sie in der Einstellungsansicht folgende Informationen ein:
    - Wählen Sie unter **Abonnement** die Option _Concierge-Abonnement_ aus.
    - Wählen Sie Ihre in der Sandbox erstellte Ressourcengruppe aus.
    - Wählen Sie den Standort aus, an dem Sie den virtuellen Computer erstellt haben.
    - Geben Sie „fmdata-vm01“ als **VM-Namen** ein.
    - Übernehmen Sie für den **Volumetyp** die Einstellung _Alle_.

1. Aktivieren Sie das Kontrollkästchen **I agree to the terms and conditions** (Ich stimme den oben genannten Geschäftsbedingungen zu).
1. Klicken Sie auf **Kaufen**, um die Vorlage auszuführen. Hinweis: Dadurch entstehen Ihnen keine Kosten. Es handelt sich lediglich um eine Standardschaltfläche.

Die Bereitstellung kann einige Minuten dauern.

## <a name="verify-the-encryption-status-of-the-vm"></a>Überprüfen des Verschlüsselungsstatus des virtuellen Computers

1. Klicken Sie auf der Seitenleiste im Azure-Portal auf **Virtuelle Computer**, und wählen Sie Ihre VM **fmdata-vm01** aus. Alternativ können Sie nach Ihrer VM anhand des Namens in **Alle Ressourcen** suchen.

1. Klicken Sie auf dem Blatt **Virtueller Computer** unter **EINSTELLUNGEN** auf **Datenträger**.

1. Wie Sie auf dem Blatt **Datenträger** sehen, hat der Betriebssystemdatenträger nun den Verschlüsselungsstatus **Deaktiviert**.
