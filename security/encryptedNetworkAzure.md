```lua
-- Create Group 
az group create --name resourceGroup --location eastus
```
```lua
-- Create VNet
az network vnet create \
    --resource-group myResourceGroup \
    --name myVirtualNetwork \
    --address-prefix 10.0.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.0.1.0/24
```