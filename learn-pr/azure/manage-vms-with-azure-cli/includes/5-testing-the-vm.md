<span data-ttu-id="82e4d-101">Wenn Sie einen virtuellen Computer erstellen, ruft er eine öffentliche IP-Adresse, die über das Internet erreichbar ist zugewiesen, und eine private IP-Adresse, die in das Azure-Rechenzentrum verwendet.</span><span class="sxs-lookup"><span data-stu-id="82e4d-101">When you create a virtual machine, it gets assigned a public IP address that is reachable over the Internet, and a private IP address used within the Azure data center.</span></span> <span data-ttu-id="82e4d-102">Wir können schnell testen, ob es sich bei der Linux-VM aktiviert ist und ausgeführt wird, mit der `ssh` Tool.</span><span class="sxs-lookup"><span data-stu-id="82e4d-102">We can quickly test that the Linux VM is up and running using the `ssh` tool.</span></span> <span data-ttu-id="82e4d-103">Beachten Sie, wir legen unsere Administratornamen auf `aldis` damit, die angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="82e4d-103">Remember we set our admin name to `aldis` so we have to specify that.</span></span>

```azurecli
ssh 168.61.54.62 -l aldis
```

> [!NOTE]
> <span data-ttu-id="82e4d-104">Wir benötigen ein Kennwort nicht, da wir im Rahmen der Erstellung des virtuellen Computers eine SSH-Schlüsselpaar generiert.</span><span class="sxs-lookup"><span data-stu-id="82e4d-104">We don't need a password because we generated an SSH key pair as part of the VM creation.</span></span> <span data-ttu-id="82e4d-105">Das erste Mal, wenn Sie Shell auf dem virtuellen Computer, es wird erhalten Sie eine Eingabeaufforderung zu die Echtheit des Hosts.</span><span class="sxs-lookup"><span data-stu-id="82e4d-105">The first time you shell into the VM, it wil give you a prompt about the authenticity of the host.</span></span> 
> 
> <span data-ttu-id="82e4d-106">Dies ist, da wir eine IP-Adresse direkt anstelle eines Hostnamens erreichen.</span><span class="sxs-lookup"><span data-stu-id="82e4d-106">This is because we are hitting an IP address directly instead of a host name.</span></span> <span data-ttu-id="82e4d-107">Antwortenden "Ja" die IP-Adresse als einen gültigen Host für die Verbindung gespeichert und ermöglichen die Verbindung, um den Vorgang fortzusetzen.</span><span class="sxs-lookup"><span data-stu-id="82e4d-107">Answering "yes" will save the IP as a valid host for connection and allow the connection to proceed.</span></span>

```
The authenticity of host '168.61.54.62 (168.61.54.62)' can't be established.
RSA key fingerprint is SHA256:hlFnTCAzgWVFiMxHK194I2ap6+5hZoj9ex8+/hoM7rE.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '168.61.54.62' (RSA) to the list of known hosts.
```

<span data-ttu-id="82e4d-108">Anschließend wird eine Remoteshell angezeigt werden, können Sie Linux-Befehle eingeben.</span><span class="sxs-lookup"><span data-stu-id="82e4d-108">Then you'll be presented with a remote shell where you can enter Linux commands.</span></span>

```
The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
aldis@SampleVM:~$
```

<span data-ttu-id="82e4d-109">Versuchen Sie es ein paar Befehlen als Übung, und wenn Sie fertig sind, melden Sie sich Ihr Konto (Typ `logout` oder `exit` in der Shell).</span><span class="sxs-lookup"><span data-stu-id="82e4d-109">Try a few commands as practice and when you are finished, sign out of your account (type `logout` or `exit` in the shell).</span></span>