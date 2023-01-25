# create-secure-workspace-template

[msft tutorial-create-secure-workspace-template](https://learn.microsoft.com/en-us/azure/machine-learning/tutorial-create-secure-workspace-template?tabs=bicep%2Ccli)
[repo based on](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.machinelearningservices/machine-learning-end-to-end-secure)

# Changes made to secure workspace bicep
- removed bastion
- removed aks
- updated to workspaces@2022-10-01


# bicep steps
- change storage to open to my ip address
```bash
az login --use-device-code
az extension update -n ml

az group create --name example-ml-secure-wise --location australiaeast

```

```bash
az deployment group create \
    --resource-group example-ml-secure-wise\
    --template-file main.bicep \
    --parameters \
    prefix=wisem
```

# make workspace publicly accessible
[Enable public access](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-configure-private-link#enable-public-access) to the workspace.
[Configure the Azure Storage firewall](https://learn.microsoft.com/en-us/azure/storage/common/storage-network-security?toc=/azure/storage/blobs/toc.json#grant-access-from-an-internet-ip-range) to allow communication with the IP address of clients that connect over the public internet.
Configure the registry to have 

# init compute instance
```bash
git clone https://github.com/Azure/azureml-examples.git --depth 1


az version
az extension update -n ml

az login --use-device-code
```

# tests
## registry access

> **Warning**
> Works for only for Azureml registry. Need to make azureml registry ontop of acr.
> After creating Azureml registry takes 30 mins to appear in GUI but can see in CLI strait away

```bash
cd /home/azureuser/cloudfiles/code/azureml-examples/cli/jobs/pipelines-with-components/basics/1b_e2e_registered_components
az ml component create --file train.yml --registry-name test

az ml component list --registry-name test
```

## RAI via component

## Endpoint