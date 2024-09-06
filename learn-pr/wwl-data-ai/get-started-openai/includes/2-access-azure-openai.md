The first step in building a generative AI solution with Azure OpenAI is to provision an Azure OpenAI resource in your Azure subscription. Azure OpenAI Service is now available to all Azure accounts, with some advanced features (like custom content filters) restricted behind a limited access policy.

> [!NOTE]
> By using the Azure OpenAI Service you are agreeing to the ethical use of the service. You can read Microsoft's Transparency note for Azure OpenAI Service [here](/legal/cognitive-services/openai/transparency-note?azure-portal=true).

Once you have access to Azure OpenAI Service, you can get started by creating a resource in the [Azure portal](https://portal.azure.com/?azure-portal=true) or with the Azure command line interface (CLI).

## Create an Azure OpenAI Service resource in the Azure portal

When you create an Azure OpenAI Service resource, you need to provide a subscription name, resource group name, region, unique instance name, and select a pricing tier.
![Screenshot of the Azure portal's page to create an Azure OpenAI Service resource.](../media/create-azure-openai-portal.png)

## Create an Azure OpenAI Service resource in Azure CLI

To create an Azure OpenAI Service resource from the CLI, refer to this example and replace the following variables with your own:

- MyOpenAIResource: *replace with a unique name for your resource*
- OAIResourceGroup: *replace with your resource group name* 
- eastus: *replace with the region to deploy your resource*
- subscriptionID: *replace with your subscription ID*

```dotnetcli
az cognitiveservices account create \
-n MyOpenAIResource \
-g OAIResourceGroup \
-l eastus \
--kind OpenAI \
--sku s0 \
--subscription subscriptionID
```

>[!NOTE]
>You can find the regions available for a service through the CLI command `az account list-locations`. To see how to sign into Azure and create an Azure group via the CLI, you can refer to the [documentation here](/azure/cognitive-services/openai/how-to/create-resource?pivots=cli#sign-in-to-the-cli?azure-portal=true). 
  

### Regional availability 
Azure OpenAI Service provides access to many types of models. Certain models are only available in select regions. Consult the [Azure OpenAI model availability guide](/azure/cognitive-services/openai/concepts/models#model-summary-table-and-region-availability/?azure-portal=true) for region availability. You can create two Azure OpenAI resources per region.
