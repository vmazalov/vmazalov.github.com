---
layout: post
category : 
tagline: ""
tags : [Azure, HPC 2012 R2, Auto-Scaling]
---
{% include JB/setup %}

[Microsoft HPC Pack](https://technet.microsoft.com/en-us/library/cc514029.aspx) is a free solution that allows easy setup and management of distributed computing cluster in Microsoft Azure. It typically contains a number of compute nodes and the head node, which is responsible for managing jobs and the compute nodes in the cluster.  The true benefits of running HPC in the cloud are realized when the computing resources are automatically adjustable based on the workload. Indeed, in most practical scenarios, the computing workload varies depending on many factors (time of the day, day of the week, business needs, etc), and it’s not satisfactory to keep all of the compute nodes constantly online and get billed for them.  The following explains how to make Microsoft HPC Pack 2012 R2 scalable based on the number of jobs in the queue. It’s written primarily for the classic (aka Service Management) Azure deployment model.

Let’s assume that an HPC Pack is setup in Azure with a fixed number of compute nodes that are always online (for help with setup, see [options to create and manage HPC in Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-hpcpack-cluster-options/)) and all prerequisites from [this article](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-hpcpack-cluster-node-autogrowshrink/) are met. We will primarily use [AzureAutoGrowShrink](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-hpcpack-cluster-node-autogrowshrink/) PowerShell script, but we will also describe some additional settings to ensure this script runs smoothly.

1. [Create a Node Template](https://technet.microsoft.com/en-us/library/cc972903(v=ws.10).aspx) for the Temporary Compute Nodes
This step is especially important if you plan to keep permanent nodes in the cluster, along with temporary nodes. Each of these node groups should be in their own Node Template to simplify management. 

1. Verify that the registry contains the following values in `HKLM:\Software\Microsoft\HPC\IaaSInfo`:
  * SubscriptionId
  * Location
  * VNet
  * SubNet
 

1. Ensure that Azure subscription is set for the user by running the [Get-AzureSubscription](https://msdn.microsoft.com/en-us/library/dn495302.aspx) command. If it’s not set, follow [these steps](https://msdn.microsoft.com/en-us/library/dn385850(v=nav.70).aspx) to download and import Azure subscription to the HPC headnode. Note, that the user should be admin or co-admin of the Azure subscription to be able to complete this step.

1. At the time of writing, the [AzureAutoGrowShrink](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-hpcpack-cluster-node-autogrowshrink/) script can only work with Azure PowerShell version 0.8.12. To check your version, run `(Get-Module -ListAvailable -Name Azure).Version`. If your version is higher, you would need to uninstall Azure PowerShell and install the proper version, that can be downloaded from [here](http://az412849.vo.msecnd.net/downloads03/azure-powershell.0.8.12.msi).

Having completed these steps, one should be able to run the AzureAutoGrowShrink script without any issues, e.g.

```
cd D:\scratch\HPCScalingLogs
```
```
AzureAutoGrowShrink.ps1 -NodeTemplates @('AMTempNodes') -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 16 -NumOfActiveQueuedTasksToGrowThreshold 1 -NumOfInitialNodesToGrow 1 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 3 -ShrinkCheckIdleTimes 3
```

Further, it's desirable to schedule the script to run upon start of the headnode. This can be done in the Task Scheduler GUI.

