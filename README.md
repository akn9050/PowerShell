# Azure PowerShell

## Install Azure PowerShell
To install Azure PowerShell on your system, see [Install Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-az-ps).
**Check Window PowerShell version**

    $PSVersionTable.PSVersion
    
Install Azure PowerShell Module

    Install-Module -Name Az –AllowClobber

1. **Login to Azure Account**
  
         Connect-AzAccount
         **-----or----**
         Login-AzAccount
1. **Set Azure Subscription**

       Get-AzSubscription   
       This command gets the all Subscriptions on which you have access within your existing azure account.

       Select-AzSubscription -Subscription "Replace me with SubscriptionID"
       Set a subscription in which you are going to work.
1. **Create Resource Group**

       New-AzResourceGroup -Name "MyFirstRGwithPowerShell" -Location "West US"  
       This will create a resource group in your azure subscription in westus region.
    
1. **Create Storage Account**

       New-AzStorageAccount -Name "strg7hhk" -Location "westus" -ResourceGroupName "MyFirstRGwithPowerShell" -SkuName Standard_LRS 
       Storage account name must be unique globally.

1. **Create Virtual Network**

       $Subnet1 = New-AzVirtualNetworkSubnetConfig -Name frontendSubnet -AddressPrefix "10.0.0.0/24"
       New-AzVirtualNetwork -Name "MyVNet" -Location "westus" -ResourceGroupName "MyFirstRGwithPowerShell" -AddressPrefix "10.0.0.0/16" -Subnet $Subnet1

1. **Create virtual network and store it in an object variable.**

       $Subnet1 = New-AzVirtualNetworkSubnetConfig -Name frontendSubnet -AddressPrefix "10.100.0.0/24"
       $virtualNetwork = New-AzVirtualNetwork `
         -ResourceGroupName MyFirstRGwithPowerShell `
         -Location westus `
         -Name MyVNet2 `
         -AddressPrefix 10.100.0.0/16 `
         -Subnet $Subnet1

       $virtualNetworkName = $virtualNetwork.Name
       $virtualNetworkID = $virtualNetwork.Id

1. **Add Subnet to existing vNet (Virtual Network)**

       $subnetConfig = Add-AzVirtualNetworkSubnetConfig `
         -Name subnet2 `
         -AddressPrefix 10.100.3.0/24 `
         -VirtualNetwork $virtualNetwork

       $virtualNetwork | Set-AzVirtualNetwork
