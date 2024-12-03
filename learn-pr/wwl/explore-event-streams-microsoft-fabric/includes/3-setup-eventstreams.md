At their simplest, eventstreams capture real-time data from a source and load the captured data into a destination.

## Eventstream sources

Event sources in Fabric Real-Time Hub can include (among others):

* **Azure Event Hub**: Azure Event Hubs is a source that allows you to get event data from an Azure event hub. You can specify the data format and the consumer group of your Azure event hub. You can also create a cloud connection to your Azure event hub with the appropriate authentication and privacy level.
- **Azure IoT Hub**: A SaaS service used to connect, monitor, and manage millions of IoT assets with a no-code experience. 
- **Azure SQL Database Change Data Capture (CDC)**: Software process that identifies and tracks changes to data in a database, enabling real-time or near-real-time data movement. 
- **PostgreSQL Database CDC**: The PostgreSQL Database CDC (change data capture) connector for Microsoft Fabric event streams captures a current snapshot and tracks future changes in a PostgreSQL database, allowing real-time processing and analysis of this data within Fabric.
- **MySQL Database CDC**: The Azure MySQL Database CDC Source connector for Microsoft Fabric event streams captures a snapshot of your MySQL database and tracks table changes, enabling real-time processing and analysis of this data in Fabric.
- **Azure Cosmos DB CDC**: The Azure Cosmos DB CDC connector for Microsoft Fabric event streams captures and tracks real-time data changes in Cosmos DB for analysis and processing within Fabric.
- **Google Cloud Pub/Sub**: A messaging service for exchanging event data among applications and services.
- **Amazon Kinesis Data Streams**: Collect, process, and analyze real-time, streaming data.
- **Confluent Cloud Kafka**: A fully managed service based on Apache Kafka for stream processing.
- **Fabric workspace events**: Fabric workspace events are events triggered by changes in your Fabric Workspace, such as creating, updating, or deleting items. With Fabric event streams, you can capture, transform, and route these events for in-depth analysis and monitoring within Fabric. This integration offers enhanced flexibility in tracking and understanding workspace activities.
- **Azure blob storage events**: Azure Blob Storage events are system triggers for actions like creating, replacing, or deleting a blob. Microsoft Fabric event streams link these actions to Fabric events, allowing you to process Blob Storage events as continuous data streams for routing and analysis within Fabric. One unique trait of the Azure Blob Storage Events is their support for ***streamed*** or ***unstreamed*** events.
- **Custom endpoint**: You can use the REST API or software development kits (SDKs) provided by Microsoft Fabric to send event data from your custom app to your event stream. You can also specify the data format and the consumer group of your custom app.
- **Sample data**: Sample data is a source that allows you to use the out-of-box sample data provided by Microsoft Fabric. You can choose from different sample data sets, such as IoT, Retail, or Finance. You can also adjust the frequency and duration of the sample data generation.

> [!TIP]
> For more information about supported sources, see **[Supported sources for Fabric Real-Time hub](/fabric/real-time-hub/supported-sources)**.

## Destinations for routed events

Microsoft Fabric event streams also supports the ability to send data to the following destinations in the enhanced mode.

| Destination | Description |
|-------------|-------------|
| **Custom endpoint** | With this feature, you can seamlessly direct your real-time event traffic to a bespoke application. It enables the integration of your proprietary applications with the event stream, allowing for the immediate consumption of event data. This feature is advantageous when you aim to transfer real-time data to an independent system not hosted on the Microsoft Fabric. |
| **Lakehouse** | This destination empowers you to preprocess your real-time events before their ingestion into your lakehouse. The events are transformed into Delta Lake format and later stored in specific lakehouse tables, facilitating your data warehousing needs. For detailed guidance on utilizing the event processor for real-time data handling, refer to the 'Process event data with event processor editor' section. |
| **Eventhouse** | This destination offers the capability to funnel your real-time event data into a KQL database, granting you the power to employ the robust Kusto Query Language (KQL) for data interrogation and analysis. Housing your data within the KQL database unlocks the potential for enhanced comprehension of your event data and the creation of comprehensive reports and dashboards. You have the flexibility to opt for one of two data ingestion approaches: either direct ingestion or preprocessing of events before ingestion.|
| **Stream** | The stream is a specialized destination created post-application of stream operations like Filter or Manage Fields to an eventstream. It represents the altered default stream after processing, which can be routed to various destinations within Fabric and monitored in the Real-Time hub. |
| **Activator** | This destination facilitates a direct linkage of your real-time event data with a Reflex. A Reflex is an intelligent entity equipped with all necessary details to establish data connections, monitor specific conditions, and execute actions. Upon the event data meeting certain predefined criteria or identifying particular patterns, the Reflex autonomously initiates suitable responses, such as notifying users or triggering Power Automate workflows. |

You can attach to multiple destinations within an event stream at the same time without impacting or colliding with each other.
