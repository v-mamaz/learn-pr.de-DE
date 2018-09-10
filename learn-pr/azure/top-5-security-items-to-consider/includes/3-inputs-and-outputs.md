The most prevalent security weakness of applications today is to not correctly process input received from external sources, particularly _user input_. You should always take a close look at any input to make sure it has been validated before it is used. Failing to do this can result in data loss or exposure, escalation of privilege, or even execution of malicious code on other users' computers!

The tragic thing is that this is an easy problem to solve. Here we will cover how to treat data; when it’s received, when it’s displayed on the screen, and when it's stored for later use.

## Why do we need to validate our input?

Imagine that you are building an interface to allow a user to create an account on your website. Our profile data includes a name, email, and a nickname that we will display to everyone who visits the site. What if a new user creates a profile and enters a nickname that includes some SQL commands? For example - what if our bad user enters something like:

```output
Eve'); DROP TABLE Users;--
```

If we just blindly insert this value into a database, it could potentially alter the SQL statement to execute commands we absolutely don't want to run! This is referred to as a "SQL Injection" attack and is one of the _many_ types of exploits that can potentially be done when you don't properly handle inputs. So, what can we do to fix this? This unit will teach you when to sanitize input, how to encode output, and how to create parameterized queries (which solves the above exploit!). These are the three main defense techniques against malicious input being entered into your applications.

## When do I need to validate input?

The answer is _always_. You must validate **every** input for your application. This includes parameters in the URL, input from the user, data from the database, data from an API and anything that is passed in the clear that a user could potentially manipulate. Always use a whitelist approach, which means you only accept "known good" input, instead of a blacklist (where you specifically look for bad input) because it's impossible to think of a complete list of potentially dangerous input.  Do this work on the server, not the client-side (or in addition to the client-side), to ensure that your defenses cannot be circumvented. Treat **ALL** data as untrusted and you will protect yourself from most of the common web app vulnerabilities.

If you are using ASP.NET, the framework provides [great support for validating input](https://docs.microsoft.com/aspnet/web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites) on both the client and server side.

If you are using another web framework, there are some great techniques for doing input validation available on the [OWASP Input Validation Cheatsheet](https://www.owasp.org/index.php/Input_Validation_Cheat_Sheet).


## Always use parameterized queries

SQL databases are commonly used to store data - we might be storing our profile information in SQL Server for example.  Never create inline SQL or other database queries "on the fly" in your code and send it directly to the database, this is a recipe for disaster, as we saw above.

For example, **do not do this** (known as inline SQL):

```csharp
string userName = ... // receive input from the user BEWARE!
...
string query = "SELECT *  FROM  [dbo].[users] WHERE userName = '" + userName + "'";
```

Here we concatenate text strings together to create the query, taking the input from the user and generating a dynamic SQL query to lookup the user. Again, if an evil user realized we were doing this, or just _tried_ different input styles to see if there was a vulnerability, we could end up with a major disaster. Instead, prefer to use parameterized SQL statements, or even better - stored procedures:

```sql
-- Lookup a user
CREATE PROCEDURE sp_findUser
(
@UserName varchar(50)
)

SELECT *  FROM  [dbo].[users] WHERE userName = @UserName
```

Then you can invoke the procedure from your code safely, passing it the `userName` string without worrying about it being treated as part of the SQL statement.

## Always encode your output

Any output you present visually or in files should always be encoded and escaped. This can protect you in case something was missed in the sanitization pass, or the code accidentally generates something that can be used maliciously. This will make sure that everything is displayed as _output_ and not inadvertently interpreted as something that should be executed. This is another very common attack technique referred to as "Cross-Site Scripting" (XSS).

Since this is such as common requirement, this is another areas where ASP.NET will do the work for you. By default, [all output is already encoded](https://docs.microsoft.com/en-us/aspnet/core/security/cross-site-scripting?view=aspnetcore-2.1). If you are using another web framework, you can verify your options for output encoding on websites with the [OWASP XSS Prevention Cheatsheet](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet).

## Summary

Santizing and validating your input is a necessary requirement to ensure your input is valid and safe to use and store. Most modern web frameworks offer built-in features which can automate some of this work - make sure to check your preferred framework's documentation and see what features it offers. Also, keep in mind that while the most common place this occurs is in web applications, other types of applications can have similar issues - so don't think you're safe if you are writing that cool desktop app! You still need to properly handle user input to ensure someone doesn't use your app to corrupt your data, or damage your company's reputation.


## Knowledge Check

Which of the following data sources need to be sanitized?
* Data from a 3rd party API
* Data from the URL parameter
* Data collected from the user via an input field
* All the above (correct answer)

Which of the following data needs to be output encoded?
* Data saved to the database
* Date to be output to the screen (correct answer)
* Data sent to a 3rd party API
* Data in the URL parameters

Parameterized queries (stored procedures in SQL) are always a more secure choice for talking to the database because:
* They are more organized than inline database commands, and therefore less confusing for users.
* There is a clear outline of the script in the stored procedure, ensuring better visibility.
* Hackers don’t understand how to program in SQL.
* Parameterized queries substitute variables before running queries, meaning it avoids the opportunity for code to be submitted in place of a variable. (correct answer)