Many organizations work with vast amounts of data. This big data can often be raw, unorganized, and stored in a range of locations such as relational, nonrelational, and other storage systems. A significant challenge for these organizations is to bring order to this big data and refine it into actionable business insights.

Microsoft Azure Data Factory is a managed cloud service that you can use to create actionable business insights from your unorganized data. It can help you manage complex hybrid extraction, transformation, and loading (ETL), extract-load-transform, and data-integration projects.

:::image type="content" source="../media/problem-overview.png" alt-text="Graphic depicting a possible big data scenario. Elements depicted are data sources, ingestion, data storage, analysis, and visualization.":::

## Example scenario

Let's imagine you work for a gaming company, where you gather data logs that are generated during gaming sessions. If you could analyze this log data, you'd be able to get insights into customer preferences, demographics, and usage behavior. People on your sales team are expressing an interest in up-selling and cross-selling opportunities, and wonder whether these data logs might contain helpful information. The development and technical teams are interested in learning about potential problems with the gaming experience, and how new features might help solve those problems.

Your problem is that to successfully analyze the data in the logs, you also need to reference the data stored in on-premises locations. This data includes customer information, game information, and marketing-campaign information. Your company stores your gaming log data in a cloud data store and wants you to use all the on-premises data as well.

To move forward with data analysis, a crucial step is to combine the on-premises data with the other data from the gaming logs. The plan is to process the combined data by using Azure Analysis Services. Then, publish the transformed data into a cloud data warehouse and visualize it by using Power BI and other tools. Azure Data Factory can help you achieve this goal.

## What are we doing?

In this module, you discover how Azure Data Factory orchestrates your big data. You evaluate whether Azure Data Factory can help you integrate your data sources. You also learn how Azure Data Factory can ingest data from on-premises, multicloud, and software as a service (SaaS) data sources.

## What is the main goal?

By the end of this module, you know more about how Azure Data Factory can help you create and schedule data-driven workflows to ingest data from different data stores. You assess whether Azure Data Factory can help you build complex ETL processes to transform this data visually with compute services or with data flows.
