Azure Machine Learning is a cloud service for accelerating and managing the machine learning project lifecycle. Machine learning professionals, data scientists, and engineers can use it in their day-to-day workflows to  train and deploy models and manage Machine Learning Ops.

You can create a model in Azure Machine Learning or use a model built from an open-source platform, such as Pytorch, TensorFlow, or scikit-learn. Machine Learning Ops support can help you monitor, retrain, and redeploy models.

There are many advantages of using the Azure Machine Learning platform to create computer vision models. It's an Enterprise grade platform service that facilitates the following capabilities when training and deploying CV models:

- It provides a single platform for labeling, training, and deploying models.
- The ability to execute the code for the model training on one compute while the real training of the model happens on another compute that is scalable to align with the number of images and modeling tasks.
- It uses the hyperdrive functionality of AutoML for images, making it possible to train hundreds of models using different algorithms and hyperparameters and then automatically have AML determine the best (champion) model automatically.

Learn more about [Machine Learning on Azure](https://azure.microsoft.com/services/machine-learning/#product-overview).

## Create an Azure Machine Learning Workspace

1. Sign into the [Azure portal](https://portal.azure.com/) by using the credentials for your Azure subscription.

1. In the upper-left corner of the Azure portal, select the three bars, the **+ Create a resource**.

    :::image type="content" source="../media/5-create-resource.png" alt-text="A screenshot is showing the Create a Resource section is highlighted." lightbox="../media/5-create-resource.png":::

1. Use the search bar to find **machine learning**, then select the **Machine Learning** result:

    :::image type="content" source="../media/5-marketplace-result.png" alt-text="A screenshot showing The Machine Learning marketplace result is shown highlighted." lightbox="../media/5-marketplace-result.png":::

1. In the **Machine Learning** pane, select the **Create** button to begin the deployment process:

    :::image type="content" source="../media/5-create-workspace.png" alt-text="A screenshot showing the create workspace option is highlighted." lightbox="../media/5-create-workspace.png":::

1. On the **Basics** tab, enter the following values for each setting:

    | Setting | Value |
    |---|---|
    | **Project details** |  |
    | Subscription | \<Your Subscription\> |
    | Resource Group | \<Create New\> OR \<Select an Existing Resource Group\> We suggest using the same resource group that contains the Azure Storage Account from previous steps. |
    | **Workspace details** |  |
    | Workspace name | Enter a unique name. A portion of this value is used to automatically prefix the names of new resources that are autopopulated for the following settings. |
    | Region | \<Select an appropriate region\> Use a location that is nearby geographically. |
    | Storage account | \<Create New\> The name is autopopulated using the **Workspace name** prefix. |
    | Key vault | \<Create New\> The name is autopopulated using the **Workspace name** prefix. |
    | Application insights | \<Create New\> The name is autopopulated using the **Workspace name** prefix. |
    | Container registry | Use the default value of *None*. |

    When you're finished select **Review + create** to validate the deployment of the Azure Machine Learning workspace.

    :::image type="content" source="../media/5-machine-learning-workspace-basics.png" alt-text="The settings of the Machine Learning workspace deployment are shown in a screenshot." lightbox="../media/5-machine-learning-workspace-basics.png":::

1. On the resulting page, you're able to validate the details of your deployment. When you're satisfied, select the **Create** button to start the deployment. This process can take a few minutes to complete.

    :::image type="content" source="../media/5-create-machine-learning-workspace.png" alt-text="The validation of the Machine Learning workspace deployment is shown in a screenshot." lightbox="../media/5-create-machine-learning-workspace.png":::

1. Once the deployment completes, navigate to your new Azure Machine Learning resource. You can easily locate this resource by typing "Azure Machine Learning" in the Azure search bar and choosing the Machine Learning icon. This lists all available Azure Machine Learning resources in your Azure Subscription.

    :::image type="content" source="../media/5-find-resource.png" alt-text="A screenshot that demonstrates how to navigate to your Azure Machine Learning resource." lightbox="../media/5-find-resource.png":::  

1. When you successfully navigate to the newly deployed instance, notice in the **Overview** section there's a button labeled **Download config.json**. Select this button to download the configuration and store it somewhere secure and accessible so that it can be used in Module 3.

    :::image type="content" source="../media/5-download-config.png" alt-text="A screenshot showing where to Download the Azure Machine Learning workspace configuration." lightbox="../media/5-download-config.png":::

1. While in the **Overview** section of the Azure Machine Learning workspace resource, select **Launch Studio** to open your workspace in the browser and prepare for the next unit.

    :::image type="content" source="../media/5-launch-studio.png" alt-text="A screenshot showing the launch studio option is highlighted." lightbox="../media/5-launch-studio.png":::