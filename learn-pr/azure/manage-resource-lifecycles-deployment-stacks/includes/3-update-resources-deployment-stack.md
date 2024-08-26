As an application evolves, so does its resources. How do we update a deployment stack and its managed resources when new services and features are added? What situations require us to update a deployment stack?

The deposits application is undergoing significant change. Azure resource properties need to be modified, new resources need to be added, and existing resources need to be removed. You need to learn more about when to update a deployment stack and how to update existing managed resources.

In this unit, you learn about what situations call for an update to a deployment stack. You also learn how to modify resources managed by a deployment stack.

[!INCLUDE [Note - don't run commands](../../../includes/dont-run-commands.md)]

## Updating a deployment stack

Over time, the resources that make up an application change. Properties of existing resources need to be modified, resources need to be added or deleted, or an application needs to integrate resources that were deployed through other approaches. A deployment stack can be updated to implement the changes in our applications. What situations require us to update a deployment stack?

- Modifying the property of a managed resource
- Adding an existing resource as a managed resource
- Adding a new managed resource
- Detaching a managed resource
- Deleting a managed resource

How are these changes implemented? As we discussed in the last module, deployment stacks manage resources that are defined in a Bicep file, ARM JSON template, or template spec. When you create a deployment stack, you reference one of these files to deploy your resources. The same is true for updating a deployment stack. To update resources managed by a deployment stack, update the underlying template file.

## Updating an existing managed resource

It's common practice to modify your resources deployed in Azure. You may need to change a property value of a resource to incorporate a new feature or enhance its functionality. If you currently use infrastructure as code to define your resources in Azure, you're familiar with how to modify the properties of a resource. With deployment stacks, the process is identical. Make the change to the resource in your Bicep file and run an update operation on the stack.

Let's consider our Bicep file from the last module. Our file defines an app service plan, a web app, and an Azure SQL server and database. We want to modify the SKU of the app service plan from the `F1` SKU to the `S1` SKU.

:::code language="bicep" source="code/1b-template.bicep" range="1-21,25-27,31-46,55-77" highlight="30":::

::: zone pivot="cli"

With the Bicep file modified, we want to update the deployment stack so that the changes made to the resources in the Bicep file are implemented.

To update a deployment stack using Azure CLI, use the `az stack group create` command.

```azurecli
az stack group create \
    --name stack-deposits \
    --resource-group rg-depositsApplication \
    --template-file ./main.bicep \
    --action-on-unmanage detachAll \
    --deny-settings-mode none
```

After the stack update is complete, we want to verify that the app service plan is now running on the `S1` SKU.

To view the configuration of the app service plan using Azure CLI, use the `az appservice plan show` command

```azurecli
az appservice plan show \
    --name plan-deposits
    --resource-group rg-depositsApplication
```

The output shows us that the update was successful and the app service plan is now running on the `S1` SKU.

```json
"sku": {
    "capacity": 1,
    "family": "S",
    "name": "S1",
    "size": "S1",
    "tier": "Standard"
},
```

::: zone-end

::: zone pivot="powershell"

With the Bicep file modified, we want to update the deployment stack so that the changes made to the resources in the Bicep file are implemented.

To update a deployment stack using Azure PowerShell, use the `Set-AzResourceGroupDeploymentStack` command.

```azurepowershell
Set-AzResourceGroupDeploymentStack `
    -Name stack-deposits `
    -ResourceGroupName rg-depositsApplication `
    -TemplateFile ./main.bicep `
    -ActionOnUnmanage DetachAll `
    -DenySettingsMode None
```

After the stack update is complete, we want to verify that the app service plan is now running on the `S1` SKU.

To view the configuration of the app service plan using Azure PowerShell, use the `Get-AzAppServicePlan` command

```powershell
$plan = Get-AzAppServicePlan `
    -ResourceGroupName rg-depositsApplication `
    -Name plan-deposits
$sku = $plan.Sku
$sku
```

The output shows us that the update was successful and the app service plan is now running on the `S1` SKU.

```powershell
Name         : S1
Tier         : Standard
Size         : S1
Family       : S
Capacity     : 1
```

::: zone-end
