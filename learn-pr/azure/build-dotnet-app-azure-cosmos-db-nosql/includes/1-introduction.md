The .NET SDK for the Azure Cosmos DB for NoSQL enables client applications to connect to resources and items via the account endpoint. You can create many of NoSQL's resources, such as containers, databases, and items by using the SDK. The .NET SDK is useful for business applications that need to perform common create, read, update, and delete (CRUD) operations from code. The .NET SDK also supports querying and batching of operations.

## Example scenario

Suppose you're a developer at a sporting-goods retail company. You're working on software to import new inventory into your database. Your application adds multiple items using the .NET SDK for Azure Cosmos DB for NoSQL. After you import your data, the application will run a query and display the results so you can validate that the correct items were added.

:::image type="content" source="../media/project-visual.svg" alt-text="Illustration of icons indicating data being uploaded to the cloud and then queried using common search techniques." border="false":::

## What are we doing?

This module specifically walks through the steps to connect to an Azure Cosmos DB for NoSQL account from a .NET console application. Your console application creates a single database and container resource if they don't already exist in your account. You then use both individual and orchestrated operations to populate the container with multiple items. Once the data is populated, you validate everything by querying the items.

In short, the application will:

- **Connect** to the API for NoSQL using a connection string.
- **Create** the necessary databases and containers.
- **Insert** new items into a container.
- **Orchestrate** multiple item operations together within the same container.
- **Query** the resulting items in the container.

## What is the main goal?

By the end of this module, you're able to create a .NET application that connects to Azure Cosmos DB for NoSQL and perform the most common operations and queries.
