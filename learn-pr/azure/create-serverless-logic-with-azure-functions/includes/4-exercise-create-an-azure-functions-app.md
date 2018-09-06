In dieser Übung erstellen wir eine Azure-Funktions-App.

1. Melden Sie sich mit Ihrem Azure-Konto beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an.
1. Wählen Sie in der linken oberen Ecke des Azure-Portals die Schaltfläche **Ressource erstellen** und dann **Compute > Funktions-App** aus, um das Blatt *Erstellen* der Funktions-App zu öffnen.
  ![Screenshot des Azure-Portals, in dem *Ressource erstellen* gefolgt von *Compute* und *Funktions-App* ausgewählt ist](../images/4-create-function-app-blade.png)
1. Wählen Sie einen global eindeutigen App-Namen aus. Dieser dient als Basis-URL Ihres Dienstes. Sie können beispielsweise den Namen **escalator-functions-xxxxxxx** auswählen, wobei „xxxxxxx“ durch Ihre Initialen und Ihr Geburtsjahr ersetzt werden kann. Wenn dies nicht global eindeutig ist, können Sie eine beliebige andere Kombination versuchen. Gültige Zeichen sind „a-z“, „0-9“ und „-“.
1. Wählen Sie das Azure-Abonnement aus, in dem die Funktions-App gehostet werden soll.
1. Erstellen Sie eine neue Ressourcengruppe namens **escalator-functions-group**. Das Verwenden eine Ressourcengruppe zum Speichern aller Ressourcen, die in diesem Modul verwendet werden, erleichtert das spätere Bereinigen.
1. Wählen Sie **Windows** als Betriebssystem aus.
1. Wählen Sie für **Hostingplan** die Option **Verbrauchstarif** aus, sodass wir die serverlosen Features von Azure nutzen können.
1. Wählen Sie den für Sie (oder Ihre Kunden) nächstgelegenen geografischen Standort aus.
1. Erstellen Sie ein neues Speicherkonto, und nennen Sie es **escalator functions**.
1. Vergewissern Sie sich, das Azure Application Insights auf **Ein** gesetzt ist, und wählen Sie die Ihnen (oder Ihren Kunden) nächstgelegene Region aus.
Wenn Sie fertig sind, sollte Ihre Konfiguration wie die Konfiguration im folgenden Screenshot aussehen.

  ![Screenshot des Konfigurationsbildschirms der Funktions-App *Erstellen* mit allen gemäß den obigen Anweisungen konfigurierten Feldern.](../images/4-create-function-app-settings.png)

1. Wählen Sie **Erstellen** aus; die Bereitstellung dauert einige Minuten. Sie erhalten eine Benachrichtigung, sobald sie abgeschlossen ist.

## <a name="verify-your-azure-function-app"></a>Überprüfen Ihrer Azure-Funktions-App

1. Wählen Sie im linken Menü des Azure-Portals **Ressourcengruppen** aus. Dann sollten in der Liste **escalator-functions-group** die verfügbaren Gruppen angezeigt werden.
  ![Screenshot des Ressourcengruppenbildschirms im Azure-Portal mit angezeigter Ressourcengruppe **escalator-functions-group**.](../images/4-resource-group.png)
1. Wählen Sie die **escalator-functions-group** aus. Es sollte dann eine Ressourcenliste ähnlich der folgenden Liste angezeigt werden.
  ![Screenshot aller Ressourcen in der Gruppe **escalator-functions-group**, einschließlich der Einträge für App Service-Plan, Speicherkonto, Application Insights und App Service](../images/4-resource-list.png)

Das als App Service aufgelistete Element mit dem Blitzsymbol ist Ihre neue Funktions-App. 
