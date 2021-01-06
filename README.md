# provisioning-with-azure-resource-manager

The repository contains sample code for [blog post](https://sszarek.blogspot.com/2021/01/provisioning-with-azure-resource.html) about basics of Azure Resource Manager templates.

It contains
* `azuredeploy.json` - the actual ARM template which is responsible for deploying Storage Account with Blob container.
* `azuredeploy.parameters.json` - parameters files where you can set values for parameters required by the template

## Deployment
In order to deploy the template you need to have Azure CLI tool installed on your machine.

Login to Azure and set default subscription (this is where deployment will be done).
```
az login
az account set --subscription "Subscription of your choice"
```

Create Resource Group. You can choose any other Azure region than `eastus`.
```
az group create --location eastus --name my-infra-rg
```

Perform actual deployment.
```
az deployment group create --resource-group my-infra-rg --template-file .\azuredeploy.json --parameters .\azuredeploy.parameters.json
```
After the command finishes its run, you should have new Storage Account created inside `my-infra-rg` resource group.

## Cleaning up the resources
In order to remove resources created in previous step, you can just remove `my-infra-rg` Resource Group. Note that this step will remove all the resource contained in the Group.
```
az group delete --name my-infra-rg
```