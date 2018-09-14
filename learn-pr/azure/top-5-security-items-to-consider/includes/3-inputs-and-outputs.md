Die am weitesten verbreitete Sicherheitsrisiko Anwendungen besteht darin, vor allem aus externen Quellen empfangen Eingaben nicht ordnungsgemäß verarbeiten _Benutzereingaben_. Sie sollten immer erstellen einen längeren Blick in eine Eingabe, um sicherzustellen, dass sie vor der Verwendung überprüft wurde. Wenn diese Änderung kann dazu führen Daten verloren gehen oder Offenlegung, Ausweitung von Berechtigungen oder sogar Ausführung von bösartigem Code auf die Computer anderer Benutzer beschädigen.

Die tragischen ist, dass dies ein einfaches Problem zu lösen ist. Hier wird das behandelt, wie Daten behandelt werden; Wenn sie empfangen wird, wenn sie auf dem Bildschirm angezeigt wird, und wenn sie für die spätere Verwendung gespeichert werden.

## <a name="why-do-we-need-to-validate-our-input"></a>Warum brauchen wir unsere Eingabe überprüfen?

Angenommen Sie, Sie eine Schnittstelle erstellen, damit ein Benutzer auf Ihrer Website ein Konto erstellen kann. Unsere Profildaten umfasst einen Namen, e-Mail-Adresse und einen Spitznamen, den wir für alle Benutzer Besucher die Website angezeigt werden. Was geschieht, wenn ein neuer Benutzer erstellt ein Profil, und gibt einen Spitznamen, der einige SQL‑Befehle enthält? Beispiel: Benutzer eingibt, was geschieht, wenn unsere ungültige etwa:

```output
Eve'); DROP TABLE Users;--
```

Wenn wir diesen Wert nur Blind in eine Datenbank einfügen, können sie potenziell ändern die SQL-Anweisung zum Ausführen von Befehlen, die wir nicht unbedingt ausführen möchten! Dies wird als "SQL Injection-Angriff bezeichnet und ist eines der der _viele_ Arten von Angriffen, die möglicherweise ausgeführt werden können, wenn Eingaben nicht ordnungsgemäß verarbeitet. Daher können was wir tun, um dieses Problem zu beheben? Diese Einheit vermittelt, dass Sie, wenn Sie zum Überprüfen der Eingabe, Ausgabe codieren und Gewusst wie: Erstellen Sie parametrisierte Abfragen (die löst der oben genannten Exploit-Malware). Hierbei handelt es sich um die drei wichtigsten Defense Techniken gegen böswillige Eingaben in Ihre Anwendungen eingegeben wird.

## <a name="when-do-i-need-to-validate-input"></a>Wann benötige ich zum Überprüfen der Eingabe?

Die Antwort ist _immer_. Sie müssen überprüfen, **jeder** Geben Sie für Ihre Anwendung. Dazu gehören Parameter in der URL, die Eingabe der Benutzer, die Daten aus der Datenbank, die Daten aus einer API und etwas, die als Klartext übergeben wird, die ein Benutzer potenziell ändern kann. Verwenden Sie immer einen weißen Liste-Ansatz, was, dass Sie nur bedeutet "als funktionierend bekannte" Eingabe, statt eine Blacklist (, wo Sie insbesondere nach ungültigen Eingabe suchen) akzeptiert, da es nicht möglich ist, eine vollständige Liste der potenziell gefährliche Eingabe zu betrachten.  Diese Aufgabe auf dem Server nicht die clientseitige (oder zusätzlich zu den Clients), um sicherzustellen, dass die Sicherheit können nicht umgangen werden. Behandeln Sie **alle** Daten als nicht vertrauenswürdig, und Sie werden schützen Sie sich von den meisten gängigen Sicherheitslücken im Web-app.

Wenn Sie ASP.NET verwenden, um das Framework bietet [hervorragende Unterstützung für das Überprüfen von Eingaben](https://docs.microsoft.com/aspnet/web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites) auf dem Client und Server-Seite.

Wenn Sie eine andere Web-Framework verwenden, stehen Ihnen einige großartigen Techniken für die eingabeüberprüfung zur Verfügung, auf die [OWASP Eingabe Validierung Spickzettel](https://www.owasp.org/index.php/Input_Validation_Cheat_Sheet).


## <a name="always-use-parameterized-queries"></a>Verwenden Sie immer parametrisierte Abfragen

SQL-Datenbanken werden häufig zum Speichern von Daten, z. B. Informationen zum Profil verwendet.  Erstellen Sie nie Inline SQL oder andere Datenbankabfragen das "spontane" in Ihrem Code, und senden Sie es direkt an die Datenbank, dies ist eine katastrophengarantie, wie wir oben gesehen haben.

Z. B. **verwenden Sie keine** (bekannt als Inline-SQL):

```csharp
string userName = ... // receive input from the user BEWARE!
...
string query = "SELECT *  FROM  [dbo].[users] WHERE userName = '" + userName + "'";
```

Hier verketten wir die Textzeichenfolgen zusammengeführt, um die Abfrage zu erstellen, nehmen die Eingabe des Benutzers und das Generieren einer dynamischen SQL-Abfrage, um den Benutzer zu suchen. Erneut, wenn ein böswilliger Benutzer realisiert wir wurden auf diese Weise oder gerade _versucht_ verschiedene Eingabe Formate angezeigt, wenn es ein Sicherheitsrisiko war, wir könnten am Ende eines schwerwiegenden Zwischenfalls. Verwenden Sie stattdessen die parametrisierte SQL-Anweisungen oder gespeicherte Prozeduren, wie diese:

```sql
-- Lookup a user
CREATE PROCEDURE sp_findUser
(
@UserName varchar(50)
)

SELECT *  FROM  [dbo].[users] WHERE userName = @UserName
```

Mit dieser Methode können Sie aufrufen die Prozedur aus dem Code sicher sind, und übergeben sie die `userName` Zeichenfolge ohne sich Gedanken, dass es als Teil der SQL-Anweisung behandelt werden.

## <a name="always-encode-your-output"></a>Die Ausgabe immer codieren

Keine Ausgabe, die Sie entweder visuell oder innerhalb eines Dokuments darstellen sollte immer codiert und mit Escapezeichen versehen werden. Dies können Sie schützen, falls etwas in der Bereinigung Pass übersehen wurde, oder der Code generiert versehentlich in böswilliger Absicht verwendet werden können. Dies stellt sicher, dass alles, was, als angezeigt wird _Ausgabe_ und interpretiert Sie nicht versehentlich als etwas, das ausgeführt werden soll. Dies ist ein weiteres sehr häufig Angriff-Verfahren, die als "Cross-Site Scripting" (XSS) bezeichnet.

Da es sich z. B. gängige Anforderung handelt, ist dies ein weiterer Bereich, in denen ASP.NET die Arbeit für Sie tun. In der Standardeinstellung [Ausgabewerte ist bereits codiert](https://docs.microsoft.com/aspnet/core/security/cross-site-scripting?view=aspnetcore-2.1). Wenn Sie eine andere Web-Framework verwenden, können Sie überprüfen, dass die Optionen für die ausgabecodierung auf Websites mit der [OWASP XSS zur Verhinderung von Spickzettel](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet).

## <a name="summary"></a>Zusammenfassung

Santizing und überprüfen Ihre Eingabe ist eine unerlässliche Anforderung, um sicherzustellen, dass die Eingabe gültig ist und sicher ist, verwenden und zu speichern. Die meisten modernen webframeworks bieten integrierte Funktionen, die einige dieser Aufgaben automatisiert werden können. Sie können finden Sie in Ihrem bevorzugten Framework Dokumentation und sehen, welche features bietet. Webanwendungen am ehesten sind, in dem in diesem Fall, sollten Sie bedenken, dass andere Arten von Anwendungen genauso anfällig sein können. Glaube nicht, dass Sie sicher sind, nur weil Ihre neue Anwendung mit einer desktop-app ist. Sie müssen immer noch auf Benutzereingaben, um sicherzustellen, dass eine Person nicht die app verwenden, um Ihre Daten beschädigen oder beschädigen Ruf Ihres Unternehmens ordnungsgemäß zu behandeln.