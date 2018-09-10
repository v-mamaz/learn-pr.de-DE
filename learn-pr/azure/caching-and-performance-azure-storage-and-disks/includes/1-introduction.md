You manage your corporate database infrastructure of SQL Server VMs running in Azure. Times are good, and you need to scale up your operation, while still managing costs. Some database operations involve many reads of existing data. The regular invoice and reporting runs are write-heavy operations. You'd like to find a way to optimize your infrastructure to handle all operation types. Before investing in infrastructure improvements, you decide to explore VM disk caching options first.

Caching is a common approach to speeding up computing resources. Azure supports a range of caching technologies to help optimize data access across the Azure landscape, including specific cache options for the Azure storage and disks used by Azure virtual machines (VMs).

We're going to explore all disk caching options in Azure and manage disk caching with the portal and PowerShell.

## Learning objectives

In this module, you will:

- Describe the key considerations around disk performance in Azure (IOPS)
- Describe the affects of caching on disk performance in Azure
- Enable and manage cache settings with the Azure portal
- Enable and manage cache settings with PowerShell