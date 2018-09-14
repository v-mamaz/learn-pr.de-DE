Fangen wir zunächst um sicherzustellen, dass Sie mit wenigen Konten eingerichtet sind und den Startcode lokal geklont.

## <a name="create-an-azure-account"></a>Erstellen Sie ein Azure-Konto

Sie benötigen ein Konto in Azure. Wenn diese nicht bereits vorhanden, dann können Sie die Registrierung und rufen Sie ein einjähriges Abonnement als Menge von Diensten, indem Sie über diesen Link:

[Azure-Konto erstellen](https://azure.microsoft.com/free)

## <a name="create-a-slack-workspace"></a>Erstellen eines Slack-Arbeitsbereichs

Um einen slack-Befehl zu erstellen, benötigen Sie Administratorberechtigungen in einem slack-Arbeitsbereich.

Daher müssen Sie entweder um sicherzustellen, dass Sie Administratorberechtigungen auf einem vorhandenen Arbeitsbereich, oder erstellen einen völlig neuen slack-Arbeitsbereich, wie folgt:

[Slack-Arbeitsbereich erstellen](https://slack.com/create)

## <a name="clone-the-starter-code"></a>Klonen des Startcodes

Um optimale Ergebnisse zu erzielen dieses Modul zu abzurufen, empfehle ich Sie den Startcode zu klonen, und befolgen Sie die schrittweisen Anleitungen.

Stellen wir den Code, die für den müssen Sie die Anwendung ausführen sowie einigen anfänglichen bootstrap-Code können Sie sofort loslegen.

Um zu beginnen Klonen dieses _Stater_ Code auf dem lokalen Computer.

```bash
git clone https://github.com/jawache/mojifier-slack.git
```

Installieren Sie dann die erforderlichen Pakete mit:

```bash
npm install
```

Es wird empfohlen, dass Sie dieses Modul schrittweise ausführen. Jedoch wenn Sie unterbrochen werden, und Hilfe benötigen dann finden Sie in den vollständigen Code der `completed` Branch, etwa so:

```bash
git checkout completed
```

Wir werden unsere Anwendung mit schreiben `TypeScript`. NodeJS ist nicht bekannt, wie Sie **ausführen** `TypeScript`, sodass wir bei der Entwicklung wir konvertieren müssen unsere `TypeScript` code zu `JavaScript`. Die erforderlichen Tools für die Konvertierung installiert wurde, im vorherigen Schritt zum Konvertieren der `TypeScript` führen Sie diesen Befehl:

```bash
npm run build
```

Wenn der obige Befehl erfolgreich als Nächstes zu ausgeführt wurde die `*.ts` Dateien jetzt auch sollte `*.js` und `*.map` Dateien.

> **Hinweis**
>
> Behalten Sie diesen Befehl in einem terminal-Shell ausgeführt wird, wird überwacht, ob Änderungen an der TypeScript-Dateien und konvertiert diese in JavaScript-Dateien.
>
> Wenn aus irgendeinem Grund nicht in die Dateien werden erste konvertiert dann die Konsolenausgabe, die Sie im Terminalfenster aktivieren, gibt es möglicherweise Fehler in Ihrem TypeScript-Code.

## <a name="install-visual-studio-code--azure-functions-extention"></a>Installieren Sie Visual Studio-Code und Azure Functions-Erweiterung

Es gibt viele Möglichkeiten, die Sie mit Azure interagieren können, die Interaktion mit Azure mithilfe von Visual Studio Code und die zugehörigen Erweiterung von Azure Functions-Plug-in in diesem Modul.

1. Herunterladen Sie und installieren Sie visual Studio-Code aus https://code.visualstudio.com/

2. Installieren Sie die Azure Functions-Code-Erweiterungen, indem Sie die Anweisungen befolgen: https://code.visualstudio.com/tutorials/functions-extension/getting-started
