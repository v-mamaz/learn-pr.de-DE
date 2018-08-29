In dieser Übung erstellen wir eine Azure-Funktions-App.

1. Melden Sie sich mit Ihrem Azure-Konto beim [Azure-Portal](https://portal.azure.com) an.
1. Wählen Sie in der linken oberen Ecke des Azure-Portals die Schaltfläche **Ressource erstellen** und dann **Compute > Funktions-App** aus.
  ![Funktions-App-Ressource erstellen](../images/4-create-function-app-blade.png)
1. Wählen Sie einen global eindeutigen App-Namen aus. Dieser dient als Basis-URL des Diensts. Sie können den Namen **escalator-functions-xxxxxxx** auswählen, wobei „xxxxxxx“ durch Ihre Initialen und Ihr Geburtsjahr ersetzt werden kann. Wenn dies nicht global eindeutig ist, können Sie eine beliebige andere Kombination versuchen. Gültige Zeichen sind „a-z“, „0-9“ und „-“.
1. Wählen Sie das Azure-Abonnement aus, in dem die Funktions-App gehostet werden soll.
1. Erstellen Sie eine neue Ressourcengruppe namens **escalator-functions-group**. Diese hilft bei der späteren Bereinigung.
1. Wählen Sie **Windows** als Betriebssystem aus.
1. Wählen Sie für **Hostingplan** die Option **Verbrauchstarif** aus, sodass wir die serverlosen Features von Azure nutzen können.
1. Wählen Sie den für Sie (oder Ihre Kunden) nächstgelegenen geografischen Standort aus.
1. Erstellen Sie ein neues Speicherkonto, und nennen Sie es **escalatorfunctions**.
1. Stellen Sie sicher, das Azure Application Insights auf **Ein** gesetzt ist, und wählen Sie die Ihnen am nächsten gelegene Region aus.
1. Wählen Sie **Erstellen** aus; die Bereitstellung dauert einige Minuten. Sie erhalten eine Benachrichtigung, sobald sie abgeschlossen ist.
  ![Einstellungen für Funktions-Apps](../images/4-create-function-app-settings.png)

## <a name="verify-your-azure-function-app"></a>Überprüfen Ihrer Azure-Funktions-App

1. Wählen Sie im linken Menü des Azure-Portals **Ressourcengruppen** aus. Dann sollten in der Liste **escalator-functions-group** die verfügbaren Gruppen angezeigt werden.
  ![Ressourcengruppe](../images/4-resource-group.png)
1. Wählen Sie die **escalator-functions-group** aus. Es sollte dann eine Ressourcenliste ähnlich der folgenden angezeigt werden: ![Ressourcenliste](../images/4-resource-list.png)
