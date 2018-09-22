Wenn Sie einen virtuellen Computer erstellen, wird diesem eine öffentliche IP-Adresse zugewiesen, auf die über das Internet zugegriffen werden kann. Dem Computer wird auch eine private IP-Adresse zugewiesen, die innerhalb des Azure-Datencenters verwendet wird. Sie erhalten diese beiden Werte im JSON-Block, der aus dem `create`-Befehl zurückgegeben wird:

```json
{
   ...
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.83.165.85",
   ...
}
```

## <a name="connecting-to-the-vm-with-ssh"></a>Herstellen einer Verbindung mit dem virtuellen Computer mit SSH

Mit der öffentlichen IP-Adresse können wir mithilfe des Tools Secure Shell (`ssh`) schnell testen, ob der virtuelle Linux-Computer betriebsbereit ist und ausgeführt wird. Denken Sie daran, dass der Administratorname auf „`aldis`“ festgelegt wurde, und verwenden Sie diesen. Stellen Sie sicher, dass die öffentliche IP-Adresse von _Ihrer_ ausgeführten Instanz verwendet wird.

```azurecli
ssh <public-ip-address> -l aldis
```

> [!NOTE]
> Ein Kennwort ist nicht notwendig, weil wir das SSH-Schlüsselpaar während der Erstellung des virtuellen Computers generiert haben. Wenn Sie zum ersten Mal über eine Shell auf den virtuellen Computer zugreifen, werden Sie aufgefordert, die Echtheit des Hosts zu bestätigen. 
> 
> Dies liegt daran, dass wir direkt auf eine IP-Adresse anstatt auf einen Hostnamen zugreifen. Wenn Sie mit „Ja“ antworten, wird die IP-Adresse als gültiger Host für die Verbindung gespeichert und die Verbindung wird hergestellt.

```output
The authenticity of host '40.83.165.85 (40.83.165.85)' can't be established.
RSA key fingerprint is SHA256:hlFnTCAzgWVFiMxHK194I2ap6+5hZoj9ex8+/hoM7rE.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '40.83.165.85' (RSA) to the list of known hosts.
```

Anschließend wird eine Remoteshell angezeigt, in der Sie Linux-Befehle eingeben können.

```output
The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
aldis@SampleVM:~$
```

Probieren Sie zur Übung ein paar Befehle aus, und melden Sie sich von der Shell ab, wenn Sie fertig sind (geben Sie „`logout`“ oder „`exit`“ in der Shell ein).