### creating a resource group
az group create --name resourcegroupname --location ukwest
### creating a VM for app
az vm create --resource-group resourcegroupname --name vmname --image 

UbuntuLTS --admin-username ekurbiba --generate-ssh-keys
### opening port 5000 for the app
az vm open-port --port 5000 --resource-group resourcegroupname --name vmname
### creating a vault 
az keyvault create --location ukwest --name vaultname --resource-group 

resourcegroupname --network-acls-ips 0.0.0.0/0
### setting vault policies
az keyvault set-policy -n vaultname --spn $clientid$ --secret-permissions delete get list set --key-permissions create decrypt delete encrypt get list unwrapKey wrapKey
### create your secrets
az keyvault secret set --name secret-key --vault-name vaultname --value anythingyouwant 

az keyvault secret set --name translator-text-key --vault-name vaultname --value KEY1fromcognitiveservice 

az keyvault secret set --name translator-text-endpoint --vault-name vaultname --value endpointfromcognitiveservice 
### list public ips within the group
az network public-ip list -g resourcegroupname
### copy the group name ip address and ssh into it
ssh ekurbiba@publicipaddress
### while in the machine we will update our package tool
sudo apt-get update
### installing python 3.8
sudo apt install python3.8
### install pip
sudo apt install python3-pip
### pip install azure prerequisites
pip3 install azure-keyvault-secrets

pip3 install azure.identity
### export variables
export AZURE_CLIENT_ID=clientid

export AZURE_CLIENT_SECRET=clientsecret

export AZURE_TENANT_ID=tenantid

export KEY_VAULT_NAME=vaultname

export VAULT_URL=yourvaultdnsname
### then we make a directory for our project
mkdir project && cd "$_"
### the we clone our project & cd into it
git clone https://github.com/ValrynMilly/AZURE-KEYS-COGNITIVE-PROJECT.git

cd AZURE-KEYS-COGNITIVE-PROJECT
### install prerequisits from requirements.txt
pip3 install -r requirements.txt
### run the app
python3 app.py 