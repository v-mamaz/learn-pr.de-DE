Stellen Sie sich, dass ein Hacker versucht, den Zugriff auf Ihre Datenbank vor. Anwendungen, die mit der Datenbank herstellen, sind anfällig Spots zum Angriff auf. Diese Anwendungen möglicherweise nicht mit der Datenbank mithilfe von sicheren Methoden verbunden werden.

Datenbanken benötigen, ihre eigene Sicherheit, aber wie die Datenbank zugegriffen wird, kann eine wichtige Rolle in datensicherheit wiedergeben. Datenbank erfolgreich sicherheitsverletzungen sind normalerweise das Ergebnis von SQL-Injection-Angriffen. SQL Injection-Angriffe sind das Ergebnis von Anwendungen, die nicht bevorzugte Methoden für den Zugriff auf eine Datenbank verwenden.

Sehen wir uns auf Techniken, um Ihre Datenbank auf Anwendungsebene zu sichern.

## <a name="sql-injection-attacks"></a>Angriffe mit Einschleusung von SQL-Befehlen

Die [OWASP Foundation](https://owasp.org) ist eine nicht gewinnorientierte Organisation, die entwickelt wurde, erstellen Sie Standards für Anwendungen, die als vertrauenswürdig gelten sollen. Eine Liste mit den Top 10 Sicherheitsrisiken veröffentlicht regelmäßig.

Die am häufigsten verwendete Sicherheitsrisiko gemäß den OWASP handelt es sich um Injection-Angriffen, die normalerweise in Form von SQL-Injection-Angriffen erfolgen. Informationen, die an eine SQL-Anweisung wird geändert, in eine SQL-Injection-Angriff. Diese geänderten Abfragen entweder sensiblen Informationen zurückgeben oder schädliche Vorgänge in der Datenbank ausführen.

Sehen wir uns auf den folgenden ASP.NET Core-Code mithilfe von ADO.NET die Interaktionen mit einem bestimmten Kunden abgerufen.

```csharp
public List<CustomerInteraction> GetCustomerInteractions(string customerId)
{
    var result = new List<CustomerInteraction>();

    using (var conn = new SqlConnection(ConnectionString))
    {
        var sql = "select Id, CustomerId, InteractionDate, Details " +
            "from CustomerInteractions where CustomerId = '" + customerId + "'";

        using (var command = conn.CreateCommand())
        {
            command.CommandText = sql;
            conn.Open();

            using (var reader = command.ExecuteReader())
            {
                if (reader.HasRows)
                {
                    while (reader.Read())
                        result.Add(GetInteractionsFromReader(reader));
                }
            }
        }
        return result.OrderByDescending(i => i.InteractionDate).ToList();
    }
}
```

Die Abfrage selbst wird auf einen Angriff SQL vorbereitet, wie der Parameter "CustomerID" bereinigt wird nicht vor dem Wechsel in die Abfrage, und daher geändert werden kann. Die Website, die die Abfrage aufgerufen wird, wird den Parameter "CustomerID" wie folgt in der URL-Abfragezeichenfolge übergeben:

.../Home/ViewInteractions?customerId=8c69a607-3c09-45ac-9beb-c59ca2de2385

Das Problem mit dieser Strategie ist, dass der Parameter "CustomerID" geändert werden kann. Beispielsweise können Sie die CustomerId-Parameter, um zusätzliche Informationen in die Abfrage einfügen, und wählen Sie die Daten aus einer anderen Tabelle ändern.

```sql
select Id, CustomerId, InteractionDate, Details from CustomerInteractions where CustomerId = '8c69a607-3c09-45ac-9beb-c59ca2de2385'
```

Sie kann jetzt geändert werden, um weitere Informationen über eine UNION-Anweisung, um zusätzliche Informationen, hinzuzufügen, indem Sie Folgendes zur Abfrage hinzufügen hinzuzufügen:

```sql
union select Id, Id as CustomerId, getdate() as InteractionDate, CreditCardNumber + '/' + STR(CreditCardExpiryMonth, 2) + '/' + STR(CreditCardExpiryYear, 4) + ' cvv ' + STR(CreditCardCVV, 3) as Details from Customers --
```

Die SQL-Abfrage ist die URL-codierte so, dass der Wert als eine gültige Webdienst-URL-Teil akzeptiert wird. Auf der Website die URL übergeben wird, und die zusätzliche SQL-Abfrage für die Datenbank ausgeführt.

```sql
%27+union+select+Id%2C+Id+as+CustomerId%2C+getdate%28%29+as+InteractionDate%2C+CreditCardNumber+%2B+%27%2F%27+%2B+STR%28CreditCardExpiryMonth%2C+2%29+%2B+%27%2F%27+%2B+STR%28CreditCardExpiryYear%2C+4%29+%2B+%27+cvv+%27+%2B+STR%28CreditCardCVV%2C+3%29+as+Details+from+Customers+--
```

In diesem Beispiel wird veranschaulicht, wie nicht bereinigen die Informationen auf der Website zu Data-Sicherheitsproblemen führen kann.

![Screenshot des eine Adressfeld des Webbrowsers Leiste zeigt ein Beispiel für eine SQL-Injection-versuchter über eine Web-app.](../media-draft/4-view-web-page-after-sql-injection.png)

> [!Note]
> Weitere Informationen zu Injection-Angriffen finden Sie auf die [OWASP Foundation](https://www.owasp.org/).

## <a name="avoiding-sql-injection-attacks"></a>SQL Injection-Angriffe vermeiden

Um SQL Injection-Angriffe zu vermeiden, sollten Sie immer sicherstellen, dass jede Eingabe der freien Eingabe bereinigt wird. Benutzereingabe, die als Parameter für Abfragen durch Verketten von Zeichenfolgen erstellt, aber als tatsächliche Abfrageparameter übergeben werden sollte nicht verwendet werden.

Im folgenden Beispiel können Sie sehen, wie die CustomerId jetzt als eine Verwendung des Parameters übergeben wird, das @-Symbols. Parameter werden explizit definiert und Werte, die in die Abfrage übergeben.

```csharp
using (var command = conn.CreateCommand())
{
    var sql = "select Id, CustomerId, InteractionDate, Details " +
        "from CustomerInteractions where CustomerId = @CustomerId order by InteractionDate";

    command.CommandText = sql;
    var prmCustomerId = command.Parameters.Add("@CustomerId", SqlDbType.UniqueIdentifier);
    prmCustomerId.Value = Guid.Parse(customerId);

    conn.Open();

    using (var reader = command.ExecuteReader())
    {
        if (reader.HasRows)
        {
            while (reader.Read())
                result.Add(GetInteractionsFromReader(reader));
        }
    }
}
```

Die Core-Codezeilen sind:

```csharp
    var prmCustomerId = command.Parameters.Add("@CustomerId", SqlDbType.UniqueIdentifier);
    prmCustomerId.Value = Guid.Parse(customerId);
```

Sicheres Dateneingabe und parametrisierte Abfragen reduziert die Wahrscheinlichkeit, dass SQL-Injection-Angriffe auf Ihre Datenbank.

In unserem Beispiel verwendet ASP.NET Core, um die Konzepte zu veranschaulichen. Aber Bedenken Sie, dass alle Programmiersprachen Systeme, die Zugriff auf SQL Server unterstützen Mechanismen zum Übergeben von Parametern in die Werte für Abfragen verfügen.

## <a name="dynamic-data-masking"></a>Dynamische Datenmaskierung

Sie haben möglicherweise bemerkt, dass einige der Informationen in der Datenbank ist besonders empfindlich, Vielleicht Kreditkarteninformationen. In einem realen-System würden Sie nie unverschlüsselt Kreditkartendaten speichern. Leider die Kreditkarteninformationen nicht verschlüsselt, und müssen Sie eine weitere Möglichkeit zum Ausblenden der Daten zu suchen.

Nehmen wir an, die Sie Erstellen einer shopping-Websites, und während des Bestellvorgangs enthält Kreditkartendaten angezeigt. Die ersten 12 Ziffern, die der Benutzer, z.B. Xxxx-Xxxx-Xxxx-1234 angezeigt werden blockiert angezeigt werden sollen.

Dieses Verfahren wird die dynamische datenmaskierung bezeichnet. Dynamische datenmaskierung können Sie Masken anhand der Spalten in der Datenbank hinzufügen.

1. Mithilfe des Portals können Sie wählen Sie die Datenbank, die Sie verwenden möchten, wenden die Masken ein, und wählen Sie dann die **dynamische Datenmaskierung** option die **Sicherheit** festlegen.

    Die Maskierung Bildschirm zeigt eine Liste der vorhandenen dynamischen Datenmasken und Empfehlungen für Spalten, die eine dynamischen Datenmaske angewendet haben sollte.

    ![Screenshot des Azure-Portal mit der eine Liste der empfohlenen Masken für die verschiedenen Spalten eine Beispieldatenbank Datenbank.](../media-draft/4-view-recommended-masked-columns.png)

1. Um eine Maske an eine Spalte hinzuzufügen, klicken Sie auf die **hinzufügen Maske** , um die empfohlenen Maske auf die Spalte hinzuzufügen.

    ![Screenshot der Azure-Portal mit maskierte Spalten angewendet empfohlen und Maske-Funktionen, die verwendet werden.](../media-draft/4-recommended-masks-applied.png)

1. Jede neue Maske wird in die Liste der Regeln Maskierungssatz hinzugefügt werden. Klicken Sie auf die **speichern** Schaltfläche, um die Masken anzuwenden.

Wenn Sie die Spalten zu Abfragen, Datenbankadministratoren weiterhin die ursprünglichen Werte angezeigt, aber nicht-Administratoren werden maskierte Werte anzuzeigen.

Sie können andere Benutzer, der nicht maskiert-Versionen sehen, indem sie die SQL-Benutzer, die von der Maskierung der Liste ausgeschlossen hinzugefügt werden.

Hier sehen, wie die maskierten Daten dargestellt, z. B. wenn ein nicht-Administrator abgefragt.

![Screenshot der Abfrage einer Datenbank, die mit der e-Mail-, "PhoneNumber", "socialsecuritynumber", und der CreditCardNumber dazu führen, Spalten, die maskiert werden, wie sie von einem nicht-Administrator angezeigt werden sollen.](../media-draft/4-sql-query-showing-masks.png)

Die Masken für zeigt die sind solche basierend auf Empfehlungen hinzugefügt, aber Sie können eine Maske manuell hinzufügen zu. Wählen Sie die + Maske-Schaltfläche "hinzufügen", und klicken Sie dann der Pop-über können Sie das Schema, Tabelle und Spalte auswählen. Anschließend definieren Sie die Maske, die verwendet wird. Es gibt standard Masken, die z. B. verwendet werden können:

- Der Standardwert, der sondern zeigt stattdessen der Standardwert für diesen Datentyp;
- Kreditkarte-Wert, der nur die letzten vier Ziffern der Zahl, konvertieren alle Zahlen in Kleinbuchstaben x anzeigt;
- E-Mail-Adresse, die die Domäne, die Namen und alle bis auf das erste Zeichen von der e-Mail-Kontoname wird ausgeblendet;
- Zahl, die eine Zufallszahl innerhalb eines Bereichs von Werten angibt. Auf Kreditkarte Ablauf Monat und Jahr, könnten Sie z. B. zufällige Monate von 1 bis 12 auswählen und des Jahresbereichs 2018 auf 3000 festgelegt; oder
- Benutzerdefinierte Zeichenfolge. Dadurch können Sie festlegen, die Anzahl der Zeichen, die über den Anfang der Daten, die Anzahl der Zeichen, die über das Ende der Daten verfügbar gemacht und die Zeichen für den Rest der Daten wiederholen verfügbar gemacht.
