# Feast on Azure

This project provides resources to enable a [Feast](http://feast.dev) feature store on Azure. There are two options for operating Feast on Azure:

1. **Feast Azure Provider** is a simple, light-weight architecture that acts as a plugin to allow feast users to connect to Azure hosted offline, online and registry stores.
1. **Feast on Azure Kubernetes Service (AKS)** is a comprehensive solution, such as a Kubernetes based registry deployment, as well as a Spark based ingestion mechanism.

## Feast Azure Provider
The [Feast Azure provider](./provider/README.md) acts like a plugin that allows Feast users to connect to:

- Azure SQL DB and/or Synapse SQL as the _offline store_
- Azure cache for Redis as the _online store_
- Azure blob storage for the feast _registry store_

### 📐 Architecture

The _interoperable_ design of feast means that many Azure services can be used to _produce_ and/or _consume_ features (for example: Azure ML, Synapse, Azure Databricks, Azure functions, etc).

![azure provider architecture](provider/media/arch.png)

### 🐱‍👤 Getting Started

If you want to install locally:

```bash
pip install feast-azure-provider
```

We recommend the [getting started tutorial](provider/tutorial/) that walks you through an end-to-end example.

You can deploy the infrastructure for feast using:

> You may want to first make sure your subscription has registered `Microsoft.Synapse`, `Microsoft.SQL` and `Microsoft.Network` providers before running the template below, as some of them may require explicit registration.

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Ffeast-azure%2Fmain%2Fprovider%2Fcloud%2Ffs_sqldb_azuredeploy.json)

The only 2 required parameters during the set-up are:

- **Admin Password** for the the Dedicated SQL Pool being deployed.
- **Principal ID** this is to set the storage permissions for the feast registry store. You can find the value for this by opening **Cloud Shell** and run the following command:

```bash
# If you are using Azure portal CLI or Azure CLI 2.37.0 or above
az ad signed-in-user show --query id -o tsv

# If you are using Azure CLI below 2.37.0
az ad signed-in-user show --query objectId -o tsv
```

## Feast on Azure Kubernetes Service (AKS)
The [Feast on AKS](./cluster/README.md) is a secure enterprise deployment on a customer provisioned AKS cluster in an Azure VNET. This deployment does not expose any public endpoints and leverages Azure Private Link over the Feast core and serving so that the traffic flows over the Microsoft Network. This deployment also supports secure connectivity from Azure Synapse Analytics and Azure Machine Learning via private endpoints.
### 📐 Architecture

![Feast on AKS architecture](cluster/media/architecture.png)

### 🐱‍👤 Getting Started
Please refer to [Feast on AKS](./cluster/README.md) which will walkthrough the instructions to setup, install the required packages and then run the sample from Azure Synapse Analytics and Azure Machine Learning.

## Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.opensource.microsoft.com.

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

## Trademarks

This project may contain trademarks or logos for projects, products, or services. Authorized use of Microsoft 
trademarks or logos is subject to and must follow 
[Microsoft's Trademark & Brand Guidelines](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general).
Use of Microsoft trademarks or logos in modified versions of this project must not cause confusion or imply Microsoft sponsorship.
Any use of third-party trademarks or logos are subject to those third-party's policies.
