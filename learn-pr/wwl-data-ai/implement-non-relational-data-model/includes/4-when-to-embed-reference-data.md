In the previous unit, we embedded the customer address and password data into a new customer document. That action reduces the number of requests, which improves performance and reduces cost. However, you can't always embed data. There are rules for when you should embed data in a document instead of referencing it in a different row.

## When should you embed data?

Embed data in a document when the following criteria apply to your data:

- **Read or updated together**: Data that's read or updated together is nearly always modeled as a single document. This reduces the number of requests which is our objective in being efficient. In our scenario, all of the customer entities are read or written together.
- **1:1 relationship**: For example, **Customer** and **CustomerPassword** have a 1:1 relationship.
- **1:Few relationship**: In a NoSQL database, it's necessary to distinguish 1:Many relationships as bounded or unbounded. **Customer** and **CustomerAddress** have a bounded 1:Many relationship because customers in an e-commerce application normally have only a handful of addresses to ship to. When the relationship is bounded, this is a 1:Few relationship.

## When should you reference data?

Reference data as separate documents when the following criteria apply to your data:

- **Read or updated independently**: This is especially true where combining entities that would result in large documents. Updates in Azure Cosmos DB require the entire item to be replaced. If a document has a few properties that are frequently updated alongside a large number of mostly static properties, it's much more efficient to split the document into two. One document then contains the smaller set of properties that are updated frequently. The other document contains the static, unchanging values. 
- **1:Many relationship**: This is especially true if the relationship is unbounded. If you have a document which increases in size an unknown or unlimited amount of times, the cost and latency for those updates will keep increasing. This is due to the increasing size of the update costing more RU/s and the payloads going over the network which itself, is also inefficient.
- **Many:Many relationship**: We'll explore an example of this relationship in a later unit with product tags.

  Separating these properties reduces throughput consumption for more efficiency. It also reduces latency for better performance.
