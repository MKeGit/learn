## How does Azure Image Builder work?

The Azure Image Builder (AIB) service can be integrated with existing image build pipelines for a click-and-go experience. You can call the AIB service from your pipeline. Azure Image Builder lets you start with Windows or Linux images, either from the Azure Marketplace or from existing custom images. You can then add your own customizations. Also, you can specify how you want your resulting images to be distributed: from Azure Compute Gallery (formerly Shared Image Gallery), as managed images, or as virtual hard disks (VHDs).

## Azure Image Builder workflow

To use Azure Image Builder, you need to create a configuration that describes your image and submit it to the service. The service is where the image is built and then distributed. You can migrate your existing image customization pipeline to Azure as you continue to use existing scripts, commands, and processes. A high-level workflow is illustrated in the following diagram:

:::image type="content" source="../media/image-builder-flow.png" alt-text="Diagram of the AIB service process, showing the sources, customizations, and global distribution with Compute Gallery." border="false":::

Azure Image Builder allows you to pass template configurations by using Azure PowerShell, the Azure CLI, Azure Resource Manager templates, or a VM Image Builder DevOps task. When you submit the configuration to the service, Azure creates an image template resource. When the image template resource is created, a staging resource group is created in your Azure subscription that uses the following name format: `IT_<DestinationResourceGroup><TemplateName>(GUID)`. The staging resource group contains files and scripts, which are referenced in the File, Shell, and PowerShell customization in the `ScriptURI` property.

To run the build, you invoke `Run` on the VM Image Builder template resource. The service then deploys more resources to support the build, such as a virtual machine (VM), network, disk, and network adapter. If you build an image without using an existing virtual network, VM Image Builder also deploys a public IP address and network security group, and it connects to the build VM by using Secure Shell (SSH) or the Windows Remote Management (WinRM) protocol. If you select an existing virtual network, the service is deployed through Azure Private Link, and a public IP address isn't required.

After the build finishes, all resources are deleted, except for the staging resource group and the storage account. You can remove them by deleting the image template resource, or you can leave them in place to run the build again.
