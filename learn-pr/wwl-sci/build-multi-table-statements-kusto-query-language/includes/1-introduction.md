Kusto Query Language (KQL) is the query language used to perform analysis on data to create Analytics, Workbooks, and perform Hunting in Microsoft Sentinel.  Understanding how to correlate data from different tables with a KQL statement provides the foundation to build detections in Microsoft Sentinel.

You're a Security Operations Analyst working at a company that is implementing Microsoft Sentinel.  You're responsible for performing log data analysis to search for malicious activity, display visualizations, and perform threat hunting.  

To query log data, you use the Kusto Query Language (KQL). Often a result set from a KQL statement needs to be combined or joined with another result set.  You can use the union operator to combine two result sets.  The join operator joins rows together based on a key value.  You need to understand how the order of a KQL statement impacts your expected results.

>[!TIP]
>You can test the following KQL query examples in the [LA Demo site](https://ms.portal.azure.com/#view/Microsoft_OperationsManagementSuite_Workspace/LogsDemo.ReactView/). If you recieve the message "No results found", try changing the time range.
