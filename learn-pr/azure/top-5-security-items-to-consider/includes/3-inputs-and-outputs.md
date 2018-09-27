Das vorherrschende Sicherheitsrisiko für Anwendungen besteht heute darin, dass aus externen Quellen empfangene Eingaben, insbesondere _Benutzereingaben_, nicht ordnungsgemäß verarbeitet werden. Sie sollten sich Eingaben immer genau ansehen, um sicherzustellen, dass sie vor der Verwendung überprüft wurden. Andernfalls kann das Ergebnis der Verlust oder die Offenlegung von Daten, die Ausweitung von Rechten oder sogar die Ausführung von schädlichem Code auf den Computern anderer Benutzer sein.

Dabei kann dieses Problem einfach gelöst werden. Hier wird der Umgang mit Daten behandelt: wenn sie empfangen werden, wenn sie auf dem Bildschirm angezeigt werden und wenn sie für die spätere Verwendung gespeichert werden.

## <a name="why-do-we-need-to-validate-our-input"></a>Warum müssen wir unsere Eingaben überprüfen?

Angenommen, Sie erstellen eine Schnittstelle, damit ein Benutzer auf Ihrer Website ein Konto erstellen kann. Unsere Profildaten umfassen einen Namen, eine E-Mail-Adresse und einen Spitznamen, der allen Benutzern angezeigt wird, die die Website besuchen. Was geschieht, wenn ein neuer Benutzer ein Profil erstellt und einen Spitznamen eingibt, der einige SQL‑Befehle enthält? Dieser Benutzer könnte beispielsweise Folgendes eingeben:

```sql
Eve'); DROP TABLE Users;--
```

Wenn wir diesen Wert blind in eine Datenbank aufnehmen, könnte er die SQL-Anweisung ändern und Befehle ausführen, die wir unbedingt vermeiden möchten. Dies wird auch als „Angriff durch Einschleusung von SQL-Befehlen“ bezeichnet und ist einer von _vielen_ Exploits, die ausgeführt werden können, wenn Eingaben nicht ordnungsgemäß verarbeitet werden. Wie lässt sich dieses Problem beheben? In dieser Einheit wird vermittelt, wann Eingaben überprüft werden müssen, wie Ausgaben codiert werden und wie parametrisierte Abfragen erstellt werden (um den oben genannten Exploit zu verhindern). Dies sind die drei wichtigsten Verteidigungstechniken gegen schädliche Eingaben in Ihre Anwendungen.

## <a name="when-do-i-need-to-validate-input"></a>Wann muss ich Eingaben überprüfen?

Die Antwort ist _immer_. Sie müssen **jede** Eingabe in Ihre Anwendung überprüfen. Dazu gehören Parameter in der URL, Eingaben des Benutzers, Daten aus der Datenbank, Daten von einer API und alle Eingaben, die ein Benutzer bearbeiten könnte. Folgen Sie immer einem Whitelistansatz. Dies bedeutet, dass Sie nur „bekannte gute“ Eingaben akzeptieren, statt eine Blacklist zu verwenden (mit der Sie speziell nach ungültigen Eingaben suchen). Denn es ist nicht möglich, eine vollständige Liste der potenziell gefährlichen Eingaben zu erstellen.  Erledigen Sie diese Aufgabe auf dem Server und nicht auf dem Client (oder zusätzlich zum Client), um sicherzustellen, dass Ihre Verteidigung nicht umgangen werden kann. Behandeln Sie **alle** Daten als nicht vertrauenswürdig. Dadurch schützen Sie sich von den meisten gängigen Sicherheitslücken von Web-Apps.

Das ASP.NET-Framework bietet [hervorragende Unterstützung für das Überprüfen von Eingaben](https://docs.microsoft.com/aspnet/web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites) auf dem Client und dem Server.

Wenn Sie ein anderes Webframework verwenden, stehen Ihnen im [OWASP-Spickzettel für die Überprüfung von Eingaben](https://www.owasp.org/index.php/Input_Validation_Cheat_Sheet) einige großartige Techniken für die Überprüfung von Eingaben zur Verfügung.


## <a name="always-use-parameterized-queries"></a>Ausschließliches Verwenden von parametrisierten Abfragen

SQL-Datenbanken werden häufig zum Speichern von Daten verwendet, z.B. von Profilinformationen.  Erstellen Sie keine Inline-SQL- oder sonstigen Datenbankabfragen unmittelbar in Ihrem Code, um sie direkt an die Datenbank zu senden. Wie bereits dargestellt, führt dies garantiert in eine Katastrophe.

Machen Sie z.B. **Folgendes nicht** (bekannt als Inline-SQL):

```csharp
string userName = ... // receive input from the user BEWARE!
...
string query = "SELECT *  FROM  [dbo].[users] WHERE userName = '" + userName + "'";
```

Hier verketten wir Textzeichenfolgen, um die Abfrage zu erstellen, übernehmen die Eingabe des Benutzers und generieren eine dynamische SQL-Abfrage, um den Benutzer zu suchen. Wenn ein böswilliger Benutzer dies erkennen würde oder nur verschiedene Eingabeformate _ausprobieren_ würde, um eine Schwachstelle zu finden, könnte das Ergebnis ein schwerwiegender Zwischenfall sein. Verwenden Sie stattdessen parametrisierte SQL-Anweisungen oder gespeicherte Prozeduren, z.B.:

```sql
-- Lookup a user
CREATE PROCEDURE sp_findUser
(
@UserName varchar(50)
)

SELECT *  FROM  [dbo].[users] WHERE userName = @UserName
```

Mit dieser Methode können Sie dann die Prozedur sicher über den Code aufrufen und die Zeichenfolge `userName` übergeben, ohne befürchten zu müssen, dass sie als Teil der SQL-Anweisung behandelt wird.

## <a name="always-encode-your-output"></a>Codieren aller Ausgaben

Alle Ausgaben, die Sie entweder visuell oder in einem Dokument bereitstellen, sollten immer codiert und mit Escapezeichen versehen werden. So werden Sie geschützt, falls etwas bei der Bereinigung übersehen wurde oder der Code versehentlich etwas generiert, was in böswilliger Absicht verwendet werden könnte. Auf diese Weise wird sichergestellt, dass alles als _Ausgabe_ angezeigt wird und nicht versehentlich als etwas interpretiert wird, das ausgeführt werden soll. Dies ist eine weitere sehr häufige Angriffstechnik, die als „Cross-Site Scripting“ (XSS) bezeichnet wird.

Da es sich um eine sehr häufige Anforderung handelt, ist dies ein weiterer Bereich, in dem ASP.NET Ihnen die Arbeit abnimmt. Standardmäßig sind alle Ausgaben bereits codiert. Wenn Sie ein anderes Webframework verwenden, können Sie Ihre Optionen für die Ausgabecodierung auf der Website mit den Informationen unter [OWASP XSS Prevention Cheatsheet](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet) überprüfen.

## <a name="summary"></a>Zusammenfassung

Das Bereinigen und Überprüfen Ihrer Eingaben ist eine unerlässliche Anforderung, um sicherzustellen, dass die Eingaben gültig sind und sicher verwendet und gespeichert werden können. Die meisten modernen Webframeworks verfügen über integrierte Features, mit denen einige dieser Arbeitsschritte automatisiert werden können. Sie können in der Dokumentation Ihres bevorzugten Frameworks nachsehen, welche Features vorhanden sind. Für Webanwendungen passiert dies zwar am häufigsten, aber bedenken Sie, dass auch andere Arten von Anwendungen genauso anfällig sein können. Sie sollten nicht glauben, dass Sie sicher sind, weil es sich bei Ihrer neuen Anwendung um eine Desktop-App handelt. Sie müssen dennoch Benutzereingaben richtig verarbeiten, um sicherzustellen, dass niemand über die App Ihre Daten oder den Ruf Ihres Unternehmens beschädigt.