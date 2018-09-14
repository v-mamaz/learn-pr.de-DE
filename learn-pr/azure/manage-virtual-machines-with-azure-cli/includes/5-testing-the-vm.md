<span data-ttu-id="96fa9-101">Wenn Sie einen virtuellen Computer erstellen, wird diesem eine öffentliche IP-Adresse zugewiesen, auf die über das Internet zugegriffen werden kann. Dem Computer wird auch eine private IP-Adresse zugewiesen, die innerhalb des Azure-Rechenzentrums verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="96fa9-101">When you create a virtual machine, it gets assigned a public IP address that is reachable over the Internet, and a private IP address used within the Azure data center.</span></span> <span data-ttu-id="96fa9-102">Mit dem Tool „`ssh`“ können wir schnell testen, ob der virtuelle Linux-Computer betriebsbereit ist.</span><span class="sxs-lookup"><span data-stu-id="96fa9-102">We can quickly test that the Linux VM is up and running using the `ssh` tool.</span></span> <span data-ttu-id="96fa9-103">Denken Sie daran, dass der Administratorname auf „`aldis`“ festgelegt wurde, und verwenden Sie diesen.</span><span class="sxs-lookup"><span data-stu-id="96fa9-103">Remember that we set our admin name to `aldis`, so we have to specify that.</span></span>

```azurecli
ssh 168.61.54.62 -l aldis
```

> [!NOTE]
> <span data-ttu-id="96fa9-104">Ein Kennwort ist nicht notwendig, weil wir das SSH-Schlüsselpaar während der Erstellung des virtuellen Computers generiert haben.</span><span class="sxs-lookup"><span data-stu-id="96fa9-104">We don't need a password because we generated an SSH key pair as part of the VM creation.</span></span> <span data-ttu-id="96fa9-105">Wenn Sie zum ersten Mal über eine Shell auf den virtuellen Computer zugreifen, werden Sie aufgefordert, die Echtheit des Hosts zu bestätigen.</span><span class="sxs-lookup"><span data-stu-id="96fa9-105">The first time you shell into the VM, it will give you a prompt about the authenticity of the host.</span></span> 
> 
> <span data-ttu-id="96fa9-106">Dies liegt daran, dass wir direkt auf eine IP-Adresse anstatt auf einen Hostnamen zugreifen.</span><span class="sxs-lookup"><span data-stu-id="96fa9-106">This is because we are hitting an IP address directly instead of a host name.</span></span> <span data-ttu-id="96fa9-107">Wenn Sie mit „Ja“ antworten, wird die IP-Adresse als gültiger Host für die Verbindung gespeichert und die Verbindung wird hergestellt.</span><span class="sxs-lookup"><span data-stu-id="96fa9-107">Answering "yes" will save the IP as a valid host for connection and allow the connection to proceed.</span></span>

```output
The authenticity of host '168.61.54.62 (168.61.54.62)' can't be established.
RSA key fingerprint is SHA256:hlFnTCAzgWVFiMxHK194I2ap6+5hZoj9ex8+/hoM7rE.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '168.61.54.62' (RSA) to the list of known hosts.
```

<span data-ttu-id="96fa9-108">Anschließend wird eine Remoteshell angezeigt, in der Sie Linux-Befehle eingeben können.</span><span class="sxs-lookup"><span data-stu-id="96fa9-108">Then you'll be presented with a remote shell where you can enter Linux commands.</span></span>

```output
The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
aldis@SampleVM:~$
```

<span data-ttu-id="96fa9-109">Probieren Sie zur Übung ein paar Befehle aus, und melden Sie sich von Ihrem Konto ab, wenn Sie fertig sind (geben Sie „`logout`“ oder „`exit`“ in der Shell ein).</span><span class="sxs-lookup"><span data-stu-id="96fa9-109">Try a few commands as practice and when you are finished, sign out of your account (type `logout` or `exit` in the shell).</span></span>