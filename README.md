# TerraformAzureKubenetes-ACG
Create a Kubernetes cluster with Azure Kubernetes Service using Terraform

Create a Kubernetes cluster with Azure Kubernetes Service using Terraform

**RESOURCES**
- ACLOUDGURU Azure Cloud Sandbox account
- macOS Monterey v12.1, Apple M1 Pro
- Visual Studio Code v1.64.2
- Azure CLI v
- Terraform v
- Original documentation from https://docs.microsoft.com/en-us/azure/developer/terraform/create-k8s-cluster-with-tf-and-aks


**INSTRUCTIONS**
1. Start ACLOUDGURU Azure Cloud Sandbox. Take note of the following informations
Resource Group 
- Name
- Location

2. Login to Azure Sandbox account through Azure CLI

3. Clone current repo

4. Update following
variables.tf
- var.resource_group_name
- var.location

5. Create SSH key pair
https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys#create-an-ssh-key-pair

6. Storage Account
Create Storage Account in Azure Sandbox. Take note of the following informations
- Azure Storage Account Name
- Azure Storage Account Key

Next run below command in Azure CLI by replacing <YourAzureStorageAccountName> and <YourAzureStorageAccountKey> after successfully creating the Storage Account
`az storage container create -n tfstate --account-name <YourAzureStorageAccountName> --account-key <YourAzureStorageAccountKey>`

7. Create the Kubenetes cluster

a. Terraform Init
Run below command in Azure CLI by replacing <YourAzureStorageAccountName> and <YourAzureStorageAccountKey> from step #6
`terraform init -backend-config="storage_account_name=<YourAzureStorageAccountName>" -backend-config="container_name=tfstate" -backend-config="access_key=<YourStorageAccountAccessKey>" -backend-config="key=codelab.microsoft.tfstate"`

Sample Screenshots:

b. Terraform plan
Run below command in Azure CLI after successfully with init in step #7a
`terraform plan -out out.plan`

Sample Screenshots:

c. Terraform apply
Run below command in Azure CLI after successfully with plan in step #7b
'terraform apply out.plan'

Sample Screenshots:

