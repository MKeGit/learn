Contoso plans to increase the use of virtualization to optimize their computing environment as many physical servers are underutilized. In addition, there are plans to expand into additional sites and use virtualization to help expedite bringing a new site online. Bearing this in mind, it's important you can determine an appropriate method of licensing and activating these new VMs. 

## What is Automatic Virtual Machine Activation?

Contoso server admins can implement Automatic Virtual Machine Activation (AVMA) to help manage licensing and activation on new VMs. You can install VMs on a previously activated Hyper-V host, and use AVMA to manage the product keys for each VM on that host. AVMA binds the VM activation to the licensed Hyper-V server. When the VMs startup, they are automatically activated, assuming the host is properly activated.

> [!NOTE]
> AVMA provides reporting on usage in real-time, and historical data on the license state of the VMs.

On Hyper-V hosts that are activated with Volume Licensing or OEM Licensing, Contoso server admins can implement AVMA to support the following scenarios:

- Activation of VMs running on Windows Server Datacenter Hyper-V host in the remote location.
- Activation of VMs potentially without an internet connection.
- Tracking of VM usage and licensing without needing access rights to the VM.

## Requirements

Your virtualization host must be running one of the following operating systems:

- Windows Server 2025 Datacenter.
- Windows Server 2022 Datacenter.
- Windows Server 2019 Datacenter.
- Windows Server 2016 Datacenter.
- Windows Server 2012 Datacenter R2.

The following table describes the available activation options based on the operating system installed on the Hyper-V host.

| Host OS                | Supported guest OS                                           |
| ---------------------- | ------------------------------------------------------------ |
| Windows Server 2025    | Windows Server 2025, Windows Server 2022, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 |
| Windows Server 2022    | Windows Server 2022, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 |
| Windows Server 2019    | Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 |
| Windows Server 2016    | Windows Server 2016, Windows Server 2012 R2                  |
| Windows Server 2012 R2 | Windows Server 2012 R2                                       |

> [!TIP]
> You can activate all editions: Datacenter, Standard, or Essentials

## Implement AVMA

To implement AVMA, use the following procedure:

1. On your activated virtualization host running Windows Server Datacenter edition, install the Hyper-V Server role.
2. Create the VMs.
3. Install the AVMA key. One method is to use Windows PowerShell. On the VM using the following PowerShell cmdlet:

```PowerShell
slmgr /ipk <AVMA_key>
```

The VM will now activate.
