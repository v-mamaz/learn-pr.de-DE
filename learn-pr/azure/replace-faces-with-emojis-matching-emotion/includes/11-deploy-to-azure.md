Bisher in diesem Modul wir gelungen, erhalten eine Slack _Schrägstrich_ Befehl funktioniert jedoch nur während der Ausführung auf "localhost" und Tunneling auf unseren Computer Ngrok verwenden. Dies ist für die Entwicklung in Ordnung, aber zum Freigeben den Code in der Cloud ausgeführt werden soll.

In diesem Vortrag werden wir unsere Azure-Funktion in der Cloud bereitstellen und aktualisieren die slack-Konfiguration, um die neue Version des Codes verwenden.

Am Ende dieser Vorlesung lernen Sie Folgendes:

- Vorgehensweise: Erstellen einer Azure-Funktionen-App in Azure
- Gewusst wie: Bereitstellen in Azure mithilfe von Visual Studio Code
- EMA wie Ihre lokalen Einstellungen für die Produktion

## <a name="create-an-azure-function-app-on-azure"></a>Erstellen Sie eine Azure-Funktions-App in Azure

Wir werden die Azure-Funktion mithilfe von Visual Studio Code und die Erweiterung der Azure-Funktion erstellt werden.

1. Öffnen Sie die befehlspalette mit <kbd>STRG</kbd>+<kbd>P</kbd> , und wählen Sie `Azure Function: Deploy to Function App`.

   ![Für Funktionen-App bereitstellen](/media-drafts/10.deploy-to-function-app.png)

2. Sie werden aufgefordert zu bestätigen, dass Sie verwenden möchten, laden Sie das aktuelle Projekt hoch, fahren fort, und wählen Sie diese.

   ![Aus diesem Ordner bereitstellen](/media-drafts/10.select-folder-to-deploy.png)

3. Wählen Sie das Abonnement aus, die, das Sie mit der app zuordnen möchten.

   Sie sollten über ein Abonnement verfügen, auswählen, die, wenn Sie mit Azure vertraut sind.

4. Wählen Sie neue Funktionen-app erstellen

   ![Erstellen Sie neue Funktionen-App](/media-drafts/10.create-new-function-app.png)

5. Wählen Sie einen Namen für Ihre app

   Sie werden aufgefordert, wählen Sie einen Namen, die sie aufrufen, was Sie möchten. Ich rufe meinen `mojifier-slack-function-app`.

   ![Wählen Sie die App-Name](/media-drafts/10.choose-app-name.png)

6. Erstellen einer neuen Ressourcengruppe

   Ressourcengruppen sind wie wir mehrere Dienste in Azure zu einer Gruppe _app_. Sie können eine neue oder verwenden Sie eine vorhandene bereits erstellt haben, erstellen.

   Wenn Sie ein neues erstellen anschließend hat er-füllt automatisch einen Namen für Sie, können Sie auswählen, oder geben Sie einen anderen.

7. Wählen Sie _neues Speicherkonto erstellen_.

   Eine Funktions-app benötigt ein Speicherkonto, einen dauerhaften Ort zum Speichern von Daten und Dateien. Sie können eine neue oder verwenden Sie eine vorhandene bereits erstellt haben, erstellen.

   Es füllt-automatisch einen Namen für Sie; Sie können auswählen, oder geben Sie einen anderen.

8. Wählen Sie eine region

   Ihre Funktions-app muss an einer beliebigen Stelle live. Ich empfehle, Auswählen eines Speicherorts, das Sie oder Ihre Benutzer am nächsten ist. Ich bin auswählen `West Europe`

   ![Wählen Sie die App-Name](/media-drafts/10.select-region.png)

9. Der Upload abgeschlossen werden, nach Abschluss des Vorgangs zeigt das Fenster "Ausgabe", eine URL wie also warten:

```
Deployment to "mojifier-slack-function-app" completed.
HTTP Trigger Urls:
  MojifyImage: https://mojifier-slack-function-app.azurewebsites.net/api/MojifyImage
```

## <a name="try-it-out"></a>Ausprobieren

An diesem Punkt sollte mindestens voraussichtlich die `RespondToSlackCommand` Funktion, die äußerst hilfreich sein, da es auf alle anderen Abhängigkeiten verlassen nicht.

Besuchen Sie `[deployed-app-name].azurefunctions.com/api/RespondToSlashCommand?text=[image-url]`

Wenn alles funktioniert auch dann Sie sollte im Browserfenster zurückgegebenen JSON-Code wie folgt:

```json
{
  "response_type": "in_channel",
  "text": "You must provide an image to mojify",
  "attachments": [
    {
      "image_url": "https://mojifier-slack.azurewebsites.net/api/MojifyImage?imageUrl=undefined"
    }
  ]
}
```

## <a name="upload-settings"></a>Einstellungen für das Hochladen

Beachten Sie, wir haben einige Einstellungen, die wir in ein `local.settings.json` Dies waren die Schlüssel und die URL für cognitive Services.

`local.settings.json` ist genau das, dass lokal, es nie für die Produktion kopiert wird bei der Bereitstellung.

In der Regel müssen Sie zum Portal wechseln und z. B. in den Einstellungen über die Benutzeroberfläche oder mit manuell hinzufügen der `func` CLI verwenden müssen.

Da wir Visual Studio Code verwenden, können wir der Funktion von Azure-Erweiterung und die befehlspalette jedoch zum Hochladen von der lokalen Einstellungen für uns.

1.  Öffnen Sie die befehlspalette mit <kbd>STRG</kbd>+<kbd>P</kbd> , und wählen Sie `Azure Functions: Upload Local Settings`.

    ![Lokale Einstellungen für das Hochladen](/media-drafts/10.upload-local-settings.png)

2.  Wählen Sie `local.settings.json`

    ![Wählen Sie die lokale Einstellungen](/media-drafts/10.choose-localsettings.png)

3.  Wählen Sie das Abonnement aus, die, dem Ihre Funktions-app zugeordnet ist.

4.  Wählen Sie die Funktions-app, die, der Sie zum hochladen möchten, mir wird aufgerufen `mojifier-slack-function-app`

5.  Wenn sie Sie überschreiben alle Einstellungen aufgefordert werden, wählen Sie `No To All`

    Dies nur hochlädt neue Einstellungen für die ist so gewünscht, andernfalls besteht die Gefahr Produktionseinstellungen mit Einstellungen, die von der Entwicklung zu überschreiben.

    ![Wählen Sie die lokale Einstellungen](/media-drafts/10.choose-no-to-all.png)

## <a name="try-it-out"></a>Ausprobieren

Nun, wenn alles wie erwartet funktioniert sollte dann jetzt der MojifyImage-Endpunkt funktionieren.

Besuchen Sie `[deployed-app-name].azurefunctions.com/api/MojifyImage?imageUrl=[image-url]`

Wenn alles funktioniert gut, sollte das Image Mojified im Fenster angezeigt werden.

Wenn dies nicht funktioniert, versuchen Sie dann, die Problembehandlung hier.

## <a name="update-slack"></a>Aktualisieren Sie Slack

Nachdem wir unsere Funktionen, in der Cloud bereitgestellt haben können wir aktualisieren Sie die Einstellungen in Slack, zeigen Sie auf das neue _öffentliche_ URL.

1. Slack, zu aktualisieren, damit die öffentliche URL des verwendet Ihre `RespondToSlackCommand`.

![Aktualisieren Sie Slack mit Prod-URL](/media-drafts/10.deploy-update-url.png)

> **HINWEIS**
>
> Bin ich den Befehl an der Produktion verwenden aktualisieren _öffentliche_, Version der `RespondToSlackCommand` auf gehostet `*.azurewebsites.net`

## <a name="try-it-out"></a>Ausprobieren

Um zu überprüfen, dass alles richtig konfiguriert ist und dass es sich bei Slack Daten aus der bereitgestellten app anstelle der lokalen app anfordert, können abschalten `ngrok` jetzt.

Navigieren Sie dann slack-Fenster, und geben Sie Ihre bevorzugten slack Schrägstrich-Befehl.

`/mojify <image>`

Wenn sie alles funktioniert wie erwartet dann sehen Sie ein Bild im slack-Fenster angezeigt werden wie folgt:

![Windows-Taste](/media-drafts/10.publish-success.png)
