<div style="background-color:black; color:white; padding:10px">
<p><strong>Example code to create a secure network on Azure</strong></p>
<pre>
# Define variables
rg_name="my-resource-group"
vnet_name="my-virtual-network"
subnet_name="my-subnet"

# Create a resource group
az group create --name $rg_name --location eastus

# Create a virtual network and subnet
az network vnet create --resource-group $rg_name --name $vnet_name --address-prefixes 10.0.0.0/16 --subnet-name $subnet_name --subnet-prefix 10.0.1.0/24

# Create a network security group
az network nsg create --resource-group $rg_name --name my-nsg

# Create a network security group rule to allow incoming SSH traffic
az network nsg rule create --resource-group $rg_name --nsg-name my-nsg --name allow-ssh --protocol tcp --direction inbound --source-address-prefix '*' --source-port-range '*' --destination-address-prefix '*' --destination-port-range 22 --access allow --priority 1000

# Create a network security group rule to allow incoming HTTP traffic
az network nsg rule create --resource-group $rg_name --nsg-name my-nsg --name allow-http --protocol tcp --direction inbound --source-address-prefix '*' --source-port-range '*' --destination-address-prefix '*' --destination-port-range 80 --access allow --priority 1100

# Create a virtual network interface with public IP address and associate it with the network security group
az network nic create --resource-group $rg_name --name my-nic --vnet-name $vnet_name --subnet $subnet_name --network-security-group my-nsg --public-ip-address my-public-ip

# Create a virtual machine with Azure-managed encryption
az vm create --resource-group $rg_name --name my-vm --location eastus --nics my-nic --image UbuntuLTS --admin-username azureuser --generate-ssh-keys --size Standard_B1ls --os-disk-name my-os-disk --storage-sku Standard_LRS --encryption-at-host --encryption-type "AzureDiskEncryption" --encryption-key-source "Microsoft.Keyvault" --encryption-key-vault $keyvault_name --encryption-key-name $key_name --encryption-key-version $key_version
</pre>
</div>