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
- Resource Group Name
- Resource Group Location

2. Login to Azure Sandbox account through Azure CLI

3. Clone current repo

4. Update variables.tf
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
  
  ![azure-kubenetes1](https://user-images.githubusercontent.com/97861554/157278624-1d40179c-fbb8-4490-85aa-b817b70c562f.png)


7. Create the Kubenetes cluster
  
  a. Terraform Init
  Run below command in Azure CLI by replacing <YourAzureStorageAccountName> and <YourAzureStorageAccountKey> from step #6
  
  `terraform init -backend-config="storage_account_name=<YourAzureStorageAccountName>" -backend-config="container_name=tfstate" -backend-config="access_key=<YourStorageAccountAccessKey>" -backend-config="key=codelab.microsoft.tfstate"`
  
  ![azure-kubenetes2](https://user-images.githubusercontent.com/97861554/157278635-94213092-ed86-48e0-8e29-d2c7a42eba5b.png)
  
  b. Terraform plan
  Run below command in Azure CLI after successfully with init in step #7a
  
  `terraform plan -out out.plan`
  
  ![azure-kubenetes3](https://user-images.githubusercontent.com/97861554/157278649-f766e4f1-3fe3-4e85-bd6e-a7001111a41f.png)
  ![azure-kubenetes4](https://user-images.githubusercontent.com/97861554/157278660-9ea00359-74e5-41e3-ba8f-728bdb72f04a.png)
  
  c. Terraform apply
  Run below command in Azure CLI after successfully with plan in step #7b
  
  'terraform apply out.plan'
  
  ![azure-kubenetes5](https://user-images.githubusercontent.com/97861554/157278665-5ee90401-d7c2-4966-9f52-8cc9c8138e46.png)

8. Following will be created in Azure Account
  
  <img width="1511" alt="azure-kubenetes6" src="https://user-images.githubusercontent.com/97861554/157278673-40e5935a-696d-45f1-a84b-ed64a56883b2.png">
  
  <img width="1512" alt="azure-kubenetes7" src="https://user-images.githubusercontent.com/97861554/157278677-077f6ee7-322e-499f-a84b-7ef272658bbb.png">
  
  <img width="758" alt="azure-kubenetes8" src="https://user-images.githubusercontent.com/97861554/157278681-bebfc52a-8021-4bd9-b0ec-581bdf77fbe2.png">
  
  <img width="758" alt="azure-kubenetes9" src="https://user-images.githubusercontent.com/97861554/157278691-8d9e34a6-3256-42b9-ba2c-dcaf308764a5.png">
  
  ![azure-kubenetes10](https://user-images.githubusercontent.com/97861554/157278693-dbec6284-25cb-490e-8fa4-da79e4ac6fb3.png)
