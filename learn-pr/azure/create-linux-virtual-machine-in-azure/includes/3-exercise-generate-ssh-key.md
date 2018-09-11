Before we can create a Linux virtual machine in Azure, we will need to think about remote access. We want to be able to sign in to our Linux web server to configure the software and perform maintenance. The default approach to administering Linux VMs hosted in Azure is SSH.

## What is SSH?

Secure Shell (SSH) is an encrypted connection protocol that allows secure sign-ins over unsecured connections. SSH allows you to connect to a terminal shell from a remote location using a network connection.

There are two approaches we can use to authenticate an SSH connection: ** username/password**, or a **SSH key pair**. 

> [!TIP]
> Although SSH provides an encrypted connection, using passwords with SSH connections leaves the VM vulnerable to brute-force attacks or guessing of passwords. A more secure and preferred method of connecting to a Linux VM with SSH is with a public-private key pair, also known as SSH keys.

With an SSH key pair, you can sign in to Linux-based Azure virtual machines without a password. This is a more secure approach if you only plan to sign in to the VM from a few computers. If you need to be able to access the Linux VM from a variety of locations, a username and password combination might be a better approach. There are two parts to an SSH key pair: a public key and a private key.

* The public key is placed on your Linux VM or any other service that you wish to use with public-key cryptography. This can be shared with anyone.

- The **private key** is what you present to your Linux VM when you make an SSH connection, to verify your identity. Consider this confidential information and protect this like you would a password or any other private data.

You can use the same single public-private key pair to access multiple Azure VMs and services.

## Create the SSH key pair

On Linux, Windows 10, and MacOS, you can use the built-in `ssh-keygen` command to generate the SSH public and private key files. 

> [!TIP]  
> Windows 10 includes an SSH client with the **Fall Creators Update**. Earlier versions of Windows require additional software to use SSH; [check the documentation for full details](https://docs.microsoft.com/azure/virtual-machines/linux/ssh-from-windows). Alternatively, you can install the Linux subsystem for Windows and get the same functionality.

> [!NOTE]  
> We will use Azure Cloud Shell, which will store the generated keys in Azure in your private storage account. You can also type these commands directly into your local shell if you prefer. You will need to adjust the instructions throughout this module to reflect a local session if you take this approach.

Here is the minimum command necessary to generate the key pair for an Azure VM. This will create an SSH protocol 2 (SSH-2) RSA public-private key pair with a 2048-bit length (the minimum length). 

Type this command into Cloud Shell:

```bash
ssh-keygen -t rsa -b 2048
```

The tool will prompt for filenames and an optional passphrase. Just take the defaults. It will create two files: `id_rsa` and `id_rsa.pub` in the `~/.ssh` directory. The files are overwritten if they exist. There are various options you can use to provide the filename or a passphrase to avoid the prompt.

### Private key passphrase

You can optionally provide a passphrase while generating your private key. This is a password you must enter when you use the key. This passphrase is used to access the private SSH key file and is not the user account password. 

When you add a passphrase to your SSH key, it encrypts the private key using 128-bit AES, so that the private key is useless without the passphrase to decrypt it. 

> [!IMPORTANT]  
> It is **strongly** recommended that you add a passphrase. If an attacker stole your private key, and that key did not have a passphrase, they would be able to use that private key to log in to any servers that have the corresponding public key. If a passphrase protects a private key, it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.

Here is an example showing how to set the passphrase. You don't need to execute this command (although you can if you want to):

```bash
ssh-keygen -t rsa -b 4096 \
    -C "azureuser@myserver" \
    -f ~/.ssh/mykeys/myprivatekey \
    -N someReallySecurePhraseYouWillRemember
```

| Parameter | What it does |
|-----------|--------------|
| `-t` | Type of key to create. Must be **rsa**. |
| `-b` | Number of bits in the key. Minimum length is 2048; maximum is 4096. |
| `-C` | An optional comment to append to the public key that can be used to identify it. Normally this is an email address, but it's simple text, and you can use whatever identification method you prefer. |
| `-f` | The location and filename of the private key file. A corresponding public key file appended with **.pub** is generated in the same directory. The directory must exist. |
| `-N` | The passphrase used to encrypt the private key. |

## Use the SSH key pair with an Azure Linux VM

Once you have the key pair generated, you can use it with a Linux VM in Azure. You can supply the public key during the VM creation or add it after the VM has been created. 

You can view the contents of the file in Azure Cloud Shell with the following command: 

```bash
cat ~/.ssh/id_rsa.pub
```

It will be a single line and look something like:

```output
ssh-rsa XXXXXXXXXXc2EAAAADAXABAAABAXC5Am7+fGZ+5zXBGgXS6GUvmsXCLGc7tX7/rViXk3+eShZzaXnt75gUmT1I2f75zFn2hlAIDGKWf4g12KWcZxy81TniUOTjUsVlwPymXUXxESL/UfJKfbdstBhTOdy5EG9rYWA0K43SJmwPhH28BpoLfXXXXXGX/ilsXXXXXKgRLiJ2W19MzXHp8z3Lxw7r9wx3HaVlP4XiFv9U4hGcp8RMI1MP1nNesFlOBpG4pV2bJRBTXNXeY4l6F8WZ3C4kuf8XxOo08mXaTpvZ3T1841altmNTZCcPkXuMrBjYSJbA8npoXAXNwiivyoe3X2KMXXXXXdXXXXXXXXXXCXXXXX/ azureuser@myserver
```

Copy this value, so you can use it in the next exercise.

### Use the SSH key when creating a Linux VM

To apply the SSH key while creating a new Linux VM, you will need to copy the contents of the public key and supply it to the Azure portal, _or_ supply the public key file to the Azure CLI or Azure PowerShell command. We'll use this approach when we create our Linux VM.

### Add the SSH key to an existing Linux VM

If you have already created a VM, you can install the public key onto your Linux VM with the `ssh-copy-id` command. Once the key has been authorized for SSH, it grants access to the server without a password.

Pass it the public key file and the username to associate with the key:

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub azureuser@myserver
```

Now that we have our public key, let's switch to the Azure portal and create a Linux VM.
