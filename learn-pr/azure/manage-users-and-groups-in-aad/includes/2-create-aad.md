Though they once shared a similar name, Microsoft Entra ID is *not* a cloud version of Windows Server Active Directory. It's also not intended as a complete replacement for an on-premises Active Directory. Instead, if you're already using a Windows AD server, you can connect it to Microsoft Entra ID to extend your directory into Azure. This approach allows users to use the same credentials to access local and cloud-based resources.

![Conceptual art showing Windows AD and Microsoft Entra ID controlling resources.](../media/2-azure-vs-windows-ad.png)

A user can also use Microsoft Entra ID independently of Windows AD. Smaller companies can use Microsoft Entra ID as their only directory service to control access to their applications and SaaS products, such as Microsoft 365, Salesforce, and Dropbox.

> [!NOTE]
> Keep in mind that this approach doesn't provide a completely centralized administrative model; for example, local Windows machines would authenticate using local credentials. Users can write applications to use Microsoft Entra ID and provide authentication and authorization to be administered by a user in a single place.

## Directories, subscriptions, and users

Microsoft offers several cloud-based offerings today, all of which can use Microsoft Entra ID to identify users and control access:

- Microsoft Azure
- Microsoft 365
- Microsoft Intune
- Microsoft Dynamics 365

When a company or organization signs up to use one of these offerings, they're assigned a default *directory*, an instance of Microsoft Entra ID. This directory holds the users and groups that will have access to each of the services the company has purchased. You can refer to this default directory as a *tenant*. A tenant represents the organization and the default directory assigned to it.

A *subscription* in Azure is both a billing entity and a security boundary. Resources such as virtual machines, websites, and databases are associated with a single subscription. Each subscription also has a single account *owner* responsible for any charges incurred by resources in that subscription. If your organization wants a subscription billed to another account, you can transfer the subscription. A subscription is associated with a **single Microsoft Entra directory**. Multiple subscriptions can trust the same directory, but a subscription can only trust one directory.

You can add users and groups to multiple subscriptions. This allows the user to create, control, and access resources in the subscription. When you add a user to a subscription, the user must be known to the associated directory, as shown in the following image:

![Conceptual art showing users, directories, and subscriptions in Azure.](../media/2-users-subs-and-directories.png)

If you belong to multiple directories, you can switch the current directory in which you're working through the **Directory + subscription** button in the Azure portal header.

![Screenshot showing the Directory selection dialog in Azure portal.](../media/2-directory-and-subscription.png)

You can also decide how the default directory is selected: last visited or a specific directory. You can also set the default filter for displayed subscriptions. Default filters are useful if you have access to several subscriptions, but typically only work in a few of them.

## Create a new directory

An organization (tenant) has one associated default Microsoft Entra directory. However, owners can create additional directories to support development or testing purposes, or because they want to have separate directories to synchronize with their local Windows Server AD forests.

> [!IMPORTANT]
> The steps to create a new directory follow; however, unless you're an owner of your Azure account, this option won't be available to you. The Azure Sandbox doesn't allow you to create new Microsoft Entra directories.

1. Sign in to the [Azure portal](https://portal.azure.com?azure-portal=true).

1. On the Azure home page, under **Azure services**, select **Create a resource**.

1. In the left menu pane, select **Identity**, and then search for and select **Microsoft Entra ID**.

1. Select **Create**.

1. Select **Microsoft Entra ID** for the tenant type, then select **Next : Configuration**.

1. Enter the following values for each setting.

    - **Organization name**: Enter a name for the directory to help distinguish it from your other directories. The directory to be created will be used in production; provide a name that your users will recognize as your organization's name. You can change the name later if you want.

    - **Initial domain name**: Enter a domain name associated with your organization. Azure will give a validation error unless the domain isn't known. The default domain name will always have the suffix `.onmicrosoft.com`. You can't change the default domain. If you choose to, you can add a custom domain owned by your organization so defined users can use a traditional company email, such as `john@contoso.com`.

    - **Country or region**: Select the country/region in which the directory should reside. The country/region will identify the region and data center where the Microsoft Entra instance will live;  you can't change it later.

    ![Screenshot showing the AD creation process.](../media/2-create-directory.png)

1. Select **Create** to create the new directory. A free tier directory will be created where you can add users, create roles, register apps and devices, and control licenses.

After you've created the directory, select **Click here to manage your new tenant** to go to the Overview dashboard that lets you control all directory aspects.

![Screenshot of the Microsoft Entra dashboard.](../media/2-aad-dashboard.png)

Let's explore one of the primary elements you'll work with in Microsoft Entra ID: **users**.
