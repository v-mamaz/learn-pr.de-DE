In this exercise, you will create a virtual network in Microsoft Azure. You will then create two virtual machines and use the virtual network to connect the virtual machines to each other and to the internet.

Before you begin this unit, you will need to log into [Azure Cloud Shell](https://shell.azure.com) with your trial subscription credentials. We will use Azure Cloud Shell to create the resource groups, virtual networks, and virtual machines.

## Create a resource group

1. In the **Welcome to Azure Cloud Shell** window, click **PowerShell (Linux)**.

1. In the **you have no storage mounted** window, click **Create Storage**.

1. In the Azure PowerShell command-line prompt, type the following code and press Enter.

    ```PowerShell
    az group create --name myResourceGroup --location eastus
    ```

## Create a virtual network

1. To create a virtual network, enter the following command and press Enter.

    ```PowerShell
    az network vnet create --name myVirtualNetwork --resource-group myResourceGroup --subnet-name default
    ```

## Create two virtual machines

1. To create the first virtual machine, execute the following command to create a Windows VM with a public IP address that is accessible over port 3389 (Remote Desktop):

    ``` PowerShell
    az vm create --name dataProcessingStage1 --resource-group MyResourceGroup --admin-username "DataAdmin"--image Win2016Datacenter
    ```

1. Supply values for your password at the prompts.

1. Execute the following command to create a Windows VM without a public IP address:

    ```PowerShell
    az vm create -n dataProcessingStage2 -g MyResourceGroup --public-ip-address '' --admin-username "DataAdmin"--image Win2016Datacenter
    ```

1. When completed, the output from the second command will return a value for publicIpAddress.

## Connect to dataProcessingStage1 using Remote Desktop

1. On your client computer, press the Windows key and type RDP.

1. Ensure that **Remote Desktop Connection** app is selected, and then press Enter.

1. In the **Remote Desktop Connection** dialog box, in the **Computer** field, enter the value of dataProcessingStage1PublicIPAddress, and then click **Connect**.

1. In the **Do you trust this remote connection?** dialog box, click **Connect**.

1. In the **Windows Security** dialog box, enter the user name and password you used when you created dataProcessingStage1.

1. In the **Remote Desktop Connection** dialog box, click **OK**.

1. Sign in to the remote computer in Azure.

1. When the **Networks** message appears, click **No**.

1. Close Server Manager.

1. In the remote session, right-click the Windows key and click **Command Prompt**.

1. In the command prompt window, type the following command and press Enter.

    ```cmd
    ping dataProcessingStage2 -4
    ```

1. There should be no response from the remote computer. This is because by default, Windows Firewall prevents ICMP responses.

## Connect to dataProcessingStage2 using Remote Desktop

1. On your client computer, press the Windows key and type **RDP**. Select the **Remote Desktop Connection** app and press Enter.

1. In the **Computer** field, enter the value of dataProcessingStage2PublicIPAddress, and then click **Connect**.

1. In the **Do you trust this remote connection?** dialog box, click **Connect**.

1. In the **Windows Security** dialog box, enter the user name and password you used when you created dataProcessingStage2.

1. In the **Remote Desktop Connection** dialog box, click **OK**. You now sign in to the remote computer in Azure.

1. When the **Networks** message appears, click **No**.

1. Close Server Manager.

1. On dataProcessingStage2, press the Windows key, type **Firewall**, and press Enter. The **Windows Firewall with Advanced Security** console appears.

1. In the left-hand pane, click **Inbound Rules**.

1. In the right-hand pane, scroll down and right-click **File and Printer Sharing (Echo Request - ICMPv4-In)**, and then click **Enable Rule**.

1. Switch back to the dataProcessingStage1 console and in the command prompt window, type the following command and press Enter.

    ```cmd
    ping dataProcessingStage2 -4
    ```

1. dataProcessingStage2 responds with four replies, demonstrating connectivity between the two VMs.

## Summary

You have successfully created a virtual network, created two VMs that are attached to that virtual network, connected to one of the VMs and shown network connectivity to the other VM within the same virtual network. You can use Azure Virtual Network to connect resources within the Azure network. However, those resources need to be within the same resource group and subscription. Next, we will look at VPN gateways, which enable you to connect virtual network in different resource groups, subscriptions, and even geographical regions.
