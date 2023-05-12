# Azure Enrypted Network

```terminal
$ rg_name="my-resource-group"
$ vnet_name="my-virtual-network"
$ subnet_name="my-subnet"

$ az group create --name $rg_name --location eastus
$ az network vnet create --resource-group $rg_name --name $vnet_name --address-prefixes 10.0.0.0/16 --subnet-name $subnet_name --subnet-prefix 10.0.1.0/24
$ az network nsg create --resource-group $rg_name --name my-nsg
$ az network nsg rule create --resource-group $rg_name --nsg-name my-nsg --name allow-ssh --protocol tcp --direction inbound --source-address-prefix '*' --source-port-range '*' --destination-address-prefix '*' --destination-port-range 22 --access allow --priority 1000
$ az network nsg rule create --resource-group $rg_name --nsg-name my-nsg --name allow-http --protocol tcp --direction inbound --source-address-prefix '*' --source-port-range '*' --destination-address-prefix '*' --destination-port-range 80 --access allow --priority 1100
$ az network nic create --resource-group $rg_name --name my-nic --vnet-name $vnet_name --subnet $subnet_name --network-security-group my-nsg --public-ip-address my-public-ip
$ az vm create --resource-group $rg_name --name my-vm --location eastus --nics my-nic --image UbuntuLTS --admin-username azureuser --generate-ssh-keys --size Standard_B1ls --os-disk-name my-os-disk --storage-sku Standard_LRS --encryption-at-host --encryption-type "AzureDiskEncryption" --encryption-key-source "Microsoft.Keyvault" --encryption-key-vault $keyvault_name --encryption-key-name $key_name --encryption-key-version $key_version
```
.terminal {
  background-color: #000;
  color: #fff;
  font-family: "Courier New", Courier, monospace;
  padding: 10px;
  border-radius: 4px;
}
