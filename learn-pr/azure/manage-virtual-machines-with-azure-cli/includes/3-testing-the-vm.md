<span data-ttu-id="35057-101">Wenn Sie einen virtuellen Computer erstellen, wird diesem eine öffentliche IP-Adresse zugewiesen, auf die über das Internet zugegriffen werden kann. Dem Computer wird auch eine private IP-Adresse zugewiesen, die innerhalb des Azure-Datencenters verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="35057-101">When you create a virtual machine, it gets assigned a public IP address that is reachable over the Internet, and a private IP address used within the Azure data center.</span></span> <span data-ttu-id="35057-102">Sie erhalten diese beiden Werte im JSON-Block, der aus dem `create`-Befehl zurückgegeben wird:</span><span class="sxs-lookup"><span data-stu-id="35057-102">You get both of those values in the returning JSON block from the `create` command:</span></span>

```json
{
   ...
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.83.165.85",
   ...
}
```

## <a name="connecting-to-the-vm-with-ssh"></a><span data-ttu-id="35057-103">Herstellen einer Verbindung mit dem virtuellen Computer mit SSH</span><span class="sxs-lookup"><span data-stu-id="35057-103">Connecting to the VM with SSH</span></span>

<span data-ttu-id="35057-104">Mit der öffentlichen IP-Adresse können wir mithilfe des Tools Secure Shell (`ssh`) schnell testen, ob der virtuelle Linux-Computer betriebsbereit ist und ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="35057-104">With the public IP address we can quickly test that the Linux VM is up and running using the Secure Shell (`ssh`) tool.</span></span> <span data-ttu-id="35057-105">Denken Sie daran, dass der Administratorname auf „`aldis`“ festgelegt wurde, und verwenden Sie diesen.</span><span class="sxs-lookup"><span data-stu-id="35057-105">Remember that we set our admin name to `aldis`, so we have to specify that.</span></span> <span data-ttu-id="35057-106">Stellen Sie sicher, dass die öffentliche IP-Adresse von _Ihrer_ ausgeführten Instanz verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="35057-106">Make sure to use the public IP address from _your_ running instance.</span></span>

```azurecli
ssh <public-ip-address> -l aldis
```

> [!NOTE]
> <span data-ttu-id="35057-107">Ein Kennwort ist nicht notwendig, weil wir das SSH-Schlüsselpaar während der Erstellung des virtuellen Computers generiert haben.</span><span class="sxs-lookup"><span data-stu-id="35057-107">We don't need a password because we generated an SSH key pair as part of the VM creation.</span></span> <span data-ttu-id="35057-108">Wenn Sie zum ersten Mal über eine Shell auf den virtuellen Computer zugreifen, werden Sie aufgefordert, die Echtheit des Hosts zu bestätigen.</span><span class="sxs-lookup"><span data-stu-id="35057-108">The first time you shell into the VM, it will give you a prompt about the authenticity of the host.</span></span> 
> 
> <span data-ttu-id="35057-109">Dies liegt daran, dass wir direkt auf eine IP-Adresse anstatt auf einen Hostnamen zugreifen.</span><span class="sxs-lookup"><span data-stu-id="35057-109">This is because we are hitting an IP address directly instead of a host name.</span></span> <span data-ttu-id="35057-110">Wenn Sie mit „Ja“ antworten, wird die IP-Adresse als gültiger Host für die Verbindung gespeichert und die Verbindung wird hergestellt.</span><span class="sxs-lookup"><span data-stu-id="35057-110">Answering "yes" will save the IP as a valid host for connection and allow the connection to proceed.</span></span>

```output
The authenticity of host '40.83.165.85 (40.83.165.85)' can't be established.
RSA key fingerprint is SHA256:hlFnTCAzgWVFiMxHK194I2ap6+5hZoj9ex8+/hoM7rE.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '40.83.165.85' (RSA) to the list of known hosts.
```

<span data-ttu-id="35057-111">Anschließend wird eine Remoteshell angezeigt, in der Sie Linux-Befehle eingeben können.</span><span class="sxs-lookup"><span data-stu-id="35057-111">Then you'll be presented with a remote shell where you can enter Linux commands.</span></span>

```output
The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
aldis@SampleVM:~$
```

<span data-ttu-id="35057-112">Probieren Sie zur Übung ein paar Befehle aus, und melden Sie sich von der Shell ab, wenn Sie fertig sind (geben Sie „`logout`“ oder „`exit`“ in der Shell ein).</span><span class="sxs-lookup"><span data-stu-id="35057-112">Try a few commands as practice and when you are finished, sign out of the shell (type `logout` or `exit` in the shell).</span></span>