# Prerequisites
If you don't have an Azure subscription, create a free account before you begin.

# Review the Bicep file - main.bicep
The Bicep file used in this quickstart is from Azure Quickstart Templates

The following Azure resources have been defined in the Bicep file:

1. Microsoft.Network/virtualNetworks: Create an Azure virtual network.
2. Microsoft.Network/virtualNetworks/subnets: Create a subnet.

# Deploy the Bicep file
1. Save the Bicep file as main.bicep to your local computer.

2. Deploy the Bicep file using either Azure CLI or Azure PowerShell.

### Azure CLI:
```
az group create --name exampleRG --location eastus
az deployment group create --resource-group exampleRG --template-file main.bicep
```

### Azure Powershell:
```
New-AzResourceGroup -Name exampleRG -Location eastus
New-AzResourceGroupDeployment -ResourceGroupName exampleRG -TemplateFile ./main.bicep
```

# Review deployed resources
Use Azure CLI or Azure PowerShell to review the deployed resources.

### Azure CLI:
```
az resource list --resource-group exampleRG
```

### Azure Powershell:
```
Get-AzResource -ResourceGroupName exampleRG
```

### You can use the Azure portal to explore the resources by browsing the settings blades for VNet1.

1. On the Overview tab, you will see the defined address space of 10.0.0.0/16.
2. On the Subnets tab, you will see the deployed subnets of Subnet1 and Subnet2 with the appropriate values from the Bicep file.

# Clean up resources
When you no longer need the resources that you created with the virtual network, use Azure portal, Azure CLI, or Azure PowerShell to delete the resource group. This removes the virtual network and all the related resources.

### Azure CLI:
```
az group delete --name exampleRG
```

### Azure Powershell:
```
Remove-AzResourceGroup -Name exampleRG
```
