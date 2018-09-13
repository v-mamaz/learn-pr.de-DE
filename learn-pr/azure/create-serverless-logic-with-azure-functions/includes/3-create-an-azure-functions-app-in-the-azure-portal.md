Sie können nun damit beginnen, den Temperaturdienst zu implementieren. In der vorherigen Einheit haben Sie festgestellt, dass eine serverlose Lösung Ihren Anforderungen am besten entsprechen würde. Deshalb erstellen wir nun für unsere Azure-Funktion eine Funktions-App.

## <a name="what-is-a-function-app"></a>Was ist eine Funktions-App?
Funktionen werden in einem Ausführungskontext gehostet, der als **Funktions-App** bezeichnet wird. Sie definieren Funktions-Apps in Azure, um Ihre Funktionen und eine Computeressource logisch in Azure zu gruppieren und zu strukturieren. In unserem Aufzugsbeispiel würden Sie eine Funktions-App zum Hosten des Temperaturdiensts der Aufzugsantriebseinheit erstellen. Vor dem Erstellen der Funktions-App müssen verschiedene Entscheidungen getroffen werden: Sie müssen einen Serviceplan und ein kompatibles Speicherkonto auswählen.

### <a name="choosing-a-service-plan"></a>Auswählen eines Serviceplans
Funktions-Apps können eine von zwei Arten von Serviceplänen nutzen. Der erste Serviceplan ist der **verbrauchsbasierte Serviceplan**. Dies ist der Plan, den Sie auswählen, wenn Sie die serverlose Azure-Anwendungsplattform verwenden. Der verbrauchsbasierte Serviceplan bietet automatische Skalierung und stellt Ihnen die Ausführung Ihrer Funktionen in Rechnung. Der verbrauchsbasierte Serviceplan ermöglicht die Konfiguration eines Zeitlimits für die Ausführung einer Funktion. Standardmäßig beträgt dessen Dauer 5 Minuten, Sie können jedoch ein Timeout von bis zu 10 Minuten konfigurieren. 

Der zweite Plan wird als **Azure App Service-Plan** bezeichnet. Dieser Plan ermöglicht Ihnen, Zeitüberschreitungen zu vermeiden, indem Sie Ihre Funktion kontinuierlich auf einer von Ihnen definierten VM ausführen lassen. Bei Verwendung eines App Service-Plans sind Sie für die Verwaltung der App-Ressourcen zuständig, auf denen die Funktion ausgeführt wird, sodass es sich hierbei technisch gesehen nicht um einen serverlosen Plan handelt. Allerdings kann es eine bessere Wahl sein, wenn Ihre Funktionen kontinuierlich genutzt werden oder Funktionen mehr Verarbeitungsleistung oder Ausführungszeit benötigen als im verbrauchsbasierten Serviceplan vorgesehen. 

### <a name="storage-account-requirements"></a>Anforderungen an das Speicherkonto
Erstellen Sie eine Funktions-App, und verbinden Sie sie mit einem Speicherkonto. Sie können ein vorhandenes Konto auswählen oder ein neues erstellen. Die Funktions-App verwendet dieses Speicherkonto für interne Vorgänge wie z.B. das Protokollieren von Funktionsausführungen und Verwalten von Ausführungstriggern. Im verbrauchsbasierten Serviceplan werden auch der Funktionscode und die Konfigurationsdateien gespeichert.

## <a name="create-a-function-app"></a>Erstellen einer Funktions-App
Lassen Sie uns eine Funktions-App im Azure-Portal erstellen.

1. Melden Sie sich mit Ihrem Azure-Konto beim [Azure-Portal](https://portal.azure.com?azure-portal=true) an.

1. Klicken Sie links oben im Azure-Portal auf die Schaltfläche **Ressource erstellen** und dann auf **Erste Schritte > Serverlose Funktions-App** aus, um das Blatt *Erstellen* der Funktions-App zu öffnen. Alternativ können Sie auch die Option **Compute-> Funktions-App** wählen, um das gleiche Blatt zu öffnen.
  
  ![Azure-Portal, in dem „Ressource erstellen“ gefolgt von „Compute“ und „Funktions-App“ ausgewählt ist](../media-draft/3-create-function-app-blade.png)

1. Wählen Sie einen global eindeutigen App-Namen aus. Dieser dient als Basis-URL Ihres Dienstes. Sie können beispielsweise den Namen **escalator-functions-xxxxxxx** wählen, wobei „xxxxxxx“ durch Ihre Initialen und Ihr Geburtsjahr ersetzt werden kann. Wenn dies nicht global eindeutig ist, können Sie eine beliebige andere Kombination versuchen. Gültige Zeichen sind „a-z“, „0-9“ und „-“.

1. Wählen Sie das Azure-Abonnement aus, in dem die Funktions-App gehostet werden soll.

1. Erstellen Sie eine neue Ressourcengruppe namens **escalator-functions-group**. Das Verwenden eine Ressourcengruppe zum Speichern aller Ressourcen, die in diesem Modul verwendet werden, erleichtert das spätere Bereinigen.

1. Wählen Sie **Windows** als Betriebssystem aus.

1. Wählen Sie für **Hostingplan** die Option **Verbrauchsplan**, die die serverbasierte Hostingoption darstellt.

1. Wählen Sie den für Sie (oder Ihre Kunden) nächstgelegenen geografischen Standort aus.

1. Erstellen Sie ein neues Speicherkonto. Azure benennt es basierend auf dem App-Namen. Sie können ihn nach Belieben ändern, er muss aber auf jeden Fall eindeutig sein.

1. Vergewissern Sie sich, das Azure Application Insights auf **Ein** festgelegt ist, und wählen Sie die Ihnen (oder Ihren Kunden) nächstgelegene Region aus.
Wenn Sie fertig sind, sollte Ihre Konfiguration wie die im folgenden Screenshot aussehen.

  ![Konfigurationsbildschirm der Funktions-App „Erstellen“ mit allen gemäß den obigen Anweisungen konfigurierten Feldern.](../media-draft/3-create-function-app-settings.png)

1. Wählen Sie **Erstellen** aus. Die Bereitstellung dauert einige Minuten. Sie erhalten eine Benachrichtigung, sobald sie abgeschlossen ist.

## <a name="verify-your-azure-function-app"></a>Überprüfen Ihrer Azure-Funktions-App

1. Wählen Sie im linken Menü des Azure-Portals **Ressourcengruppen** aus. Dann sollten in der Liste **escalator-functions-group** die verfügbaren Gruppen angezeigt werden.

  ![Bildschirm mit Ressourcengruppen im Azure-Portal mit angezeigter Ressourcengruppe „escalator-functions-group“.](../media-draft/3-resource-group.png)

1. Wählen Sie **escalator-functions-group** aus. Es sollte dann eine Ressourcenliste ähnlich der folgenden angezeigt werden.
  
  ![Aller Ressourcen in der Gruppe „escalator-functions-group“, einschließlich der Einträge für App Service-Plan, Speicherkonto, Application Insights und App Service](../media-draft/3-resource-list.png)

Das als App Service aufgelistete Element mit dem Blitzsymbol ist Ihre neue Funktions-App. Sie können auf sie klicken, um die Details zur neuen Funktion zu öffnen, der eine öffentliche URL zugewiesen ist. Wenn Sie sie in einem Browser öffnen, sollte eine Standardwebseite angezeigt werden, die angibt, dass Ihre Funktions-App ausgeführt wird!
