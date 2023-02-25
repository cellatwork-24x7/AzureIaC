## Terraform resource types

- [random_pet](https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/pet)
- [random_string](https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/string)
- [azurerm_resource_group](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/resource_group)
- [azurerm_log_analytics_workspace](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/log_analytics_workspace)
- [azurerm_log_analytics_solution](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/log_analytics_solution)
- [azurerm_kubernetes_cluster](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/kubernetes_cluster)

## Variables

| Name | Description | Default |
|-|-|-|
| `resource_group_name_prefix` | Prefix of the resource group name that's combined with a random ID so name is unique in your Azure subscription. | rg |
| `resource_group_location` | Location of the resource group. | eastus |
| `agent_count` | Initial number of nodes which should exist in this Node Pool. Value must be between 1 and 1000. | 3 | 
| `ssh_public_key` | File containing the an ssh_key block. | ~/.ssh/id_rsa.pub |
| `dns_prefix` | DNS prefix specified when creating the managed cluster. | k8stest |
| `cluster_name` | Name of the Managed Kubernetes Cluster to create. | k8stest |
| `log_analytics_workspace_name` | Prefix of the name of the Log Analytics Workspace. Random value is appended to ensure uniqueness across Azure. | testLogAnalyticsWorkspaceName |
| `log_analytics_workspace_location` | Azure location where the resource exists. | eastus |
| `log_analytics_workspace_sku` | SKU of the Log Analytics Workspace. | PerGB2018 |
| `aks_service_principal_app_id` | Service principal app ID. | |
| `aks_service_principal_client_secret` | Service principal password. | |
| `aks_service_principal_object_id` | Service principal object ID. | |


## Example Objectives:

1. Use HCL (HashiCorp Language) to define a Kubernetes cluster
2. Use Terraform and AKS to create a Kubernetes cluster
3. Use the kubectl tool to test the availability of a Kubernetes cluster

# Prerequisites
1. Azure subscription: If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.
2. Configure Terraform: If you haven't already done so, configure Terraform using one of the following options:

    a. [Configure Terraform in Azure Cloud Shell with Bash](https://learn.microsoft.com/en-us/azure/developer/terraform/get-started-cloud-shell-bash)
    b. [Configure Terraform in Azure Cloud Shell with PowerShell](https://learn.microsoft.com/en-us/azure/developer/terraform/get-started-cloud-shell-powershell)
    c. [Configure Terraform in Windows with Bash](https://learn.microsoft.com/en-us/azure/developer/terraform/get-started-windows-bash)
    d. [Configure Terraform in Windows with PowerShell](https://learn.microsoft.com/en-us/azure/developer/terraform/get-started-windows-powershell)

3. Azure service principal: If you don't have a service principal, create a [service principal](https://learn.microsoft.com/en-us/azure/developer/terraform/authenticate-to-azure#create-a-service-principal). Make note of the appId, display_name, password, and tenant.

4. SSH key pair: Use one of the following articles:

    a. [Portal](https://learn.microsoft.com/en-us/azure/virtual-machines/ssh-keys-portal#generate-new-keys)
    b. [Windows](https://learn.microsoft.com/en-us/azure/virtual-machines/linux/ssh-from-windows#create-an-ssh-key-pair)
    c. [Linux/MacOS](https://learn.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys#create-an-ssh-key-pair)
    
5. Kubernetes command-line tool (kubectl): [Download kubectl](https://kubernetes.io/releases/download/)

# Initialize Terraform
Run terraform init to initialize the Terraform deployment. This command downloads the Azure modules required to manage your Azure resources.
```
terraform init
```

# Create a Terraform execution plan
Run terraform plan to create an execution plan.
```
terraform plan -out main.tfplan
```

Key points:

1. The terraform plan command creates an execution plan, but doesn't execute it. Instead, it determines what actions are necessary to create the configuration specified in your configuration files. This pattern allows you to verify whether the execution plan matches your expectations before making any changes to actual resources.
2. The optional -out parameter allows you to specify an output file for the plan. Using the -out parameter ensures that the plan you reviewed is exactly what is applied.

# Apply a Terraform execution plan
Run terraform apply to apply the execution plan to your cloud infrastructure.
```
terraform apply main.tfplan
```

Key points:

1. The terraform apply command above assumes you previously ran terraform plan -out main.tfplan.
2. If you specified a different filename for the -out parameter, use that same filename in the call to terraform apply.
3. If you didn't use the -out parameter, call terraform apply without any parameters.

### Verify the Results [Reference](https://learn.microsoft.com/en-us/azure/developer/terraform/create-k8s-cluster-with-tf-and-aks#verify-the-results)
