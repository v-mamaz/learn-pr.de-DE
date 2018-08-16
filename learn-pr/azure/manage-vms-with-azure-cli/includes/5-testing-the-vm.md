Wenn Sie einen virtuellen Computer erstellen, ruft er eine öffentliche IP-Adresse, die über das Internet erreichbar ist zugewiesen, und eine private IP-Adresse, die in das Azure-Rechenzentrum verwendet. Wir können schnell testen, ob es sich bei der Linux-VM aktiviert ist und ausgeführt wird, mit der `ssh` Tool. Beachten Sie, wir legen unsere Administratornamen auf `aldis` damit, die angegeben werden.

```azurecli
ssh 168.61.54.62 -l aldis
```

> [!NOTE]
> Wir benötigen ein Kennwort nicht, da wir im Rahmen der Erstellung des virtuellen Computers eine SSH-Schlüsselpaar generiert. Das erste Mal, wenn Sie Shell auf dem virtuellen Computer, es wird erhalten Sie eine Eingabeaufforderung zu die Echtheit des Hosts. 
> 
> Dies ist, da wir eine IP-Adresse direkt anstelle eines Hostnamens erreichen. Antwortenden "Ja" die IP-Adresse als einen gültigen Host für die Verbindung gespeichert und ermöglichen die Verbindung, um den Vorgang fortzusetzen.

```
The authenticity of host '168.61.54.62 (168.61.54.62)' can't be established.
RSA key fingerprint is SHA256:hlFnTCAzgWVFiMxHK194I2ap6+5hZoj9ex8+/hoM7rE.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '168.61.54.62' (RSA) to the list of known hosts.
```

Anschließend wird eine Remoteshell angezeigt werden, können Sie Linux-Befehle eingeben.

```
The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
aldis@SampleVM:~$
```

Versuchen Sie es ein paar Befehlen als Übung, und wenn Sie fertig sind, melden Sie sich Ihr Konto (Typ `logout` oder `exit` in der Shell).