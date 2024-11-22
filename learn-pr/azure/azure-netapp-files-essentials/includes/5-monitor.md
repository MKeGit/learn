The following services are recommended for monitoring your Azure NetApp Files workloads:

| Service | Description |
| -- | ---------- | 
| Azure Activity Log | The Azure Activity Log provides insight into subscription-level events. You can get information about when a resource is modified or when a virtual machine is started. You can view the activity log in the Azure portal or retrieve entries with PowerShell and CLI. You can also view the Activity log and send it to different destinations. |
| Azure NetApp Files metrics | Azure NetApp Files provides metrics on allocated storage, actual storage usage, volume IOPS, and latency. With these metrics, you can gain a better understanding on the usage pattern and volume performance of your NetApp accounts. You can find metrics for a capacity pool or volume by selecting the capacity pool or volume. Then click Metric to view the available metrics. |
| Azure Service Health | The Azure Service Health dashboard keeps you informed about the health of your environment. It provides a personalized view of the status of your Azure services in the regions where they are used. The dashboard provides upcoming planned maintenance and relevant health advisories while allowing you to manage service health alerts. |
| Capacity utilization monitoring | It's important monitor capacity regularly. You can monitor capacity utilization at the VM level. You can check the used and available capacity of a volume by using Windows or Linux clients. You can also configure alerts with [ANFCapacityManager](https://github.com/ANFTechTeam/ANFCapacityManager). |
