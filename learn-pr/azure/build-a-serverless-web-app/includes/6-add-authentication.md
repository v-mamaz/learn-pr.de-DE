Azure App Service-Authentifizierung ermöglicht die Unterstützung von einsetzbare Authentifizierung in einer Azure-Funktions-app. Es kann nahtlos in Facebook, Twitter, Microsoft Account, Google und Azure Active Directory integriert. Fügen Sie App Service-Authentifizierung, um die APIs der Web-app-Back-End zu schützen.

## <a name="enable-app-service-authentication"></a>App Service-Authentifizierung aktivieren

1. Öffnen Sie die Funktions-app im Azure-Portal an.

1. Klicken Sie unter **Plattformfeatures**Option **Authentifizierung/Autorisierung**.

    ![Wählen Sie die Authentifizierung / Autorisierung](../images/6-authorization.jpg)

1. Wählen Sie folgende Werte aus:
    
    | Einstellung      |  Empfohlener Wert   | Beschreibung                                        |
    | --- | --- | ---|
    | **App Service-Authentifizierung** | Andererseits | Aktivieren der Authentifizierung. |
    | **Aktion, wenn die Anforderung nicht authentifiziert ist** | Mit Azure Active Directory anmelden | Wählen Sie eine konfigurierte Authentifizierungsmethode (siehe unten). |
    | **Authentifizierungsanbieter** | Siehe unten | Siehe unten |
    | **Tokenspeicher** | Andererseits | Ermöglichen Sie die App Service zum Speichern und Verwalten von Token. |
    | **Zulässige externe umleitungs-URLs** | Die URL Ihrer Anwendung, z.B.: https://firstserverlessweb.z4.web.core.windows.net/ | URLs, die App Service zulässig ist, um umgeleitet werden soll, nachdem ein Benutzer authentifiziert ist. |

1. Wählen Sie **Azure Active Directory** offengelegt **Azure Active Directory-Einstellungen**.

    1. Wählen Sie **Express** als die **Verwaltungsmodus** und füllen Sie die folgenden Informationen.
    
        | Einstellung      |  Empfohlener Wert   | Beschreibung                                        |
        | --- | --- | ---|
        | **Verwaltungsmodus** | Express, erstellen Sie neue AD-app | Um einen Dienstprinzipal und eine Azure Active Directory-Authentifizierung automatisch festgelegt. |
        | **Erstellen einer App** | my-serverless-webapp | Geben Sie einen eindeutigen Anwendungsnamen ein. |
    
    1. Klicken Sie auf **OK** zum Speichern der Azure Active Directory-Einstellungen.

    ![Authentifizierung/Autorisierung und Azure Active Directory-Einstellungen](../images/6-create-aad.png)

1. Klicken Sie auf **Speichern**.


## <a name="modify-the-web-app-to-enable-authentication"></a>Ändern Sie die Web-app zum Aktivieren der Authentifizierung

1. Stellen Sie sicher, dass das aktuelle Verzeichnis ist, in der Cloud Shell die **Www/Dist** Ordner.

    ```azurecli
    cd ~/functions-first-serverless-web-application/www/dist
    ```

1. Fügen Sie zum Aktivieren der Authentifizierung in Ihrer Funktions-app die folgende Codezeile, **settings.js**.

    `window.authEnabled = true`

    Nehmen Sie die Änderung, und zeigen Sie das Ergebnis mit den folgenden Befehlen oder mithilfe eines Befehlszeile Editors wie z. B. VIM.

    ```azurecli
    echo "window.authEnabled = true" >> settings.js
    ```

    Vergewissern Sie sich, dass die Änderung an der Datei vorgenommen wurde.

    ```azurecli
    cat settings.js
    ```

1. Laden Sie die Datei in Blob Storage hoch.

    ```azurecli
    az storage blob upload -c \$web --account-name <storage account name> -f settings.js -n settings.js
    ```


## <a name="test-the-application"></a>Testen der Anwendung

1. Öffnen Sie die Anwendung in einem Browser. Klicken Sie auf **melden Sie sich bei** und melden Sie sich.

1. Wählen Sie eine Bilddatei, und Laden Sie es hoch.

    ![Anmeldeseite](../images/6-aad-auth.png)
    

## <a name="summary"></a>Zusammenfassung

In dieser Einheit haben Sie gelernt, wie die Verwendung von Azure App Service-Authentifizierung Applcation Authentifizierung hinzufügen.