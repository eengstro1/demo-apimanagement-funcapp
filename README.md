# Instructions

__Requirements:__

1. [Visual Studio Code](https://visualstudio.microsoft.com/downloads/)

1. [Dotnet Core](https://www.microsoft.com/net/learn/get-started-with-dotnet-tutorial)

```powershell
dotnet --version

# Result
  2.1.301
```

1. [Azure CLI](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps?view=azurermps-6.5.0)

```powershell
az --version

# Result
  azure-cli (2.0.42)
```

__Build:__

```powershell
dotnet restore Demo.Functions.sln
dotnet build Demo.Functions.sln
```


### Deploy (bash cloud shell)

```bash
Resource_Group="demo"
Prefix="75098"
Code="https://github.com/danielscholl/demo-apimanagement-functioncode"

# Create Resource Group
az group create --name ${Resource_Group} \
	--location "eastus2"



az storage account create --name "${Prefix}storage" \
    --resource-group ${Resource_Group} \
    --sku Standard_LRS \
    --location eastus2 

# Deploy a Function App
az functionapp create --name "${Prefix}-funcapp" \
    --resource-group ${Resource_Group} \
    --storage-account  ${Storage_Account} \
    --deployment-source-url ${Code}  \
    --consumption-plan-location eastus2

```