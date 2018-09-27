> [!TIP]
> Der Benutzername und das Kennwort, die Sie für die Anmeldung bei der VM benötigen, müssen sich auf der Registerkarte **Ressourcen** befinden.

> [!NOTE]
> Wenn Sie einen Mac verwenden, müssen Sie nach dem Starten der VM entweder das Blitzsymbol auf der Symbolleiste oder die Option **STRG+ALT+ENTF** von der Registerkarte **Ressourcen** neben den Anweisungen verwenden, um die VM zu entsperren.


In diesem Modul erstellen Sie eine plattformübergreifende Xamarin.Forms-App mit serverlosem Back-End. Diese App ruft den Standort der Benutzer von deren Gerät ab und sendet ihn mit einer Liste von Telefonnummern an eine Azure-Funktion. Die Funktion verwendet dann eine Bindung an einen Drittanbieterdienst (Twilio), um Ihren Standort als SMS an alle angegebenen Telefonnummern zu senden.

Dieser Vorgang umfasst die folgenden Schritte:

1. Die App erfasst Ihren Standort mithilfe von Xamarin.Essentials als eine Abstraktion über gerätespezifische Standort-APIs.

1. Der Standort und die Telefonnummern werden in eine JSON-Nutzlast verpackt und an eine Azure-Funktion gesendet.

1. Die Azure-Funktion decodiert die JSON-Nutzlast und erstellt SMS-Nachrichten.

1. Die SMS-Nachrichten werden über [Twilio](https://www.twilio.com/?azure-portal=true) gesendet.

Die folgende Abbildung zeigt eine Übersicht dieses Prozesses.

![Abbildung, die die allgemeine Architektur des Prozesses des Teilens des Standorts mithilfe von Textnachrichten darstellt.](../media/1-architecture.png)

## <a name="create-a-twilio-account"></a>Erstellen von Twilio-Konten

Um SMS-Nachrichten von einer Azure-Funktion senden können, benötigen Sie ein Twilio-Konto. Das kostenlose Konto ist für den Beginn völlig ausreichend.

1. Besuchen Sie [twilio.com](https://www.twilio.com?azure-portal=true).

1. Klicken Sie auf die rote Schaltfläche **Sign up** (Registrieren) in der oberen rechten Ecke.

1. Geben Sie Ihre Informationen ein, und klicken Sie auf **Get Started** (Erste Schritte).

1. Sie müssen Ihre Telefonnummer bestätigen. Mit kostenlosen Twilio-Konten können Sie Nachrichten nur an verifizierte Telefonnummern senden, um zu verhindern, dass diese für Spam-Mails verwendet werden. Twilio sendet Ihnen einen Prüfcode, den Sie eingeben müssen, um Ihre Telefonnummer zu bestätigen.

1. Klicken Sie auf die Registerkarte **Produkte** > **Programmable SMS** (Programmierbare SMS), und klicken Sie dann auf **Weiter**.

1. Geben Sie einen Namen für Ihr erstes Projekt ein, z.B. „Ich bin hier“, und klicken Sie auf **Weiter**.

1. Überspringen Sie den Schritt, um ein Teammitglied einzuladen.

1. Erweitern Sie im Twilio-Nachrichtendashboard das Panel **Project Info** (Projektinformationen).

1. Notieren Sie sich Ihre **KONTO-SID** und Ihr **AUTHENTIFIZIERUNGSTOKEN**, da Sie diese Werte später benötigen.

    Wenn Sie ein Twilio-Konto erstellen, wird Ihnen eine Telefonnummer zugewiesen, über die Sie Nachrichten senden können. Sie finden diese Telefonnummer im Twilio-Dashboard **Phone Numbers** (Telefonnummern).

1. Wählen Sie auf der Twilio-Website die Auslassungspunkte im unteren Bereich des links angezeigten Menüs aus. Wählen Sie dann *SUPER NETWORK > Phone Numbers* (SUPERNETZWERK > Telefonnummern) aus. Sie können dieses Dashboard mithilfe des Stecknadelsymbols an das Menü im linken Bereich anheften. Ihre Twilio-Nummer finden Sie unter *Manage Numbers > Active Numbers* (Nummern verwalten > Aktive Nummern).

    ![Ermitteln Ihrer Twilio-Nummer](../media/7-twilio-find-number.png)

    > [!TIP]
    > Wenn Sie noch nicht über eine aktive Nummer verfügen, wählen Sie **Erste Schritte** auf der Seite „Aktive Nummern“ aus, um die Erstellung einer Zahl anzustoßen.

1. Notieren Sie sich Ihre aktive Telefonnummer. Sie wird später in diesem Modul verwendet werden.


> [!NOTE]
> Wenn Sie sich anmelden, wird Ihnen eine Twilio-Telefonnummer zum Senden von SMS-Nachrichten zugewiesen. In einigen Ländern ist das Senden von Nachrichten über diese Nummern jedoch möglicherweise nicht möglich. In der Twilio-Dokumentation ist aufgelistet, [in welchen Ländern Einschränkungen gelten](https://support.twilio.com/hc/articles/223183068-Twilio-international-phone-number-availability-and-their-capabilities?azure-portal=true). Außerdem wird gezeigt, wie Sie SMS-Nachrichten mithilfe einer [gebührenpflichtigen Nummer oder einer alphanumerischen Absender-ID](https://support.twilio.com/hc/articles/226690868-Using-Twilio-when-SMS-numbers-are-unavailable-in-your-country?azure-portal=true) senden.

## <a name="launch-visual-studio"></a>Starten von Visual Studio

Für dieses Modul entwickeln Sie die mobile App und die Azure Functions-App mit Visual Studio 2017, das über einen virtuellen Computer verfügbar ist. Obwohl Xamarin.Forms-Apps so erstellt werden können, dass sie unter iOS, Android und Universelle Windows-Plattform (UWP) verwendet werden können, konzentriert sich dieses Modul nur auf UWP und darauf, dass die App innerhalb des virtuellen Lab-Computers funktioniert.

Starten Sie Visual Studio 2017 über das Startmenü der VM oder über die Desktopverknüpfung.

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie ein Twilio-Konto zum Senden von SMS-Nachrichten erstellt und Visual Studio gestartet. Als Nächstes erfahren Sie, wie Sie eine Xamarin.Forms-App erstellen und das NuGet-Paket „Xamarin.Essentials“ hinzufügen.

> [!IMPORTANT]
> Notieren Sie sich die Werte für Ihre Twilio-**Konto-SID**, das Twilio-**AUTHENTIFIZIERUNGSTOKEN** und die **aktive Twilio-Telefonnummer**, die Sie in dieser Einheit gesammelt haben. Sie werden sie später noch einmal benötigen.
