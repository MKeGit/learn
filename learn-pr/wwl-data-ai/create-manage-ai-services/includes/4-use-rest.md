
Azure AI services provide REST application programming interfaces (APIs) that client applications can use to consume services. In most cases, service functions can be called by submitting data in JSON format over an HTTP request, which may be a POST, PUT, or GET request depending on the specific function being called. The results of the function are returned to the client as an HTTP response, often with JSON contents that encapsulate the output data from the function.

:::image type="content" source="../media/rest-api.png" alt-text="Diagram of an app submitting a JSON request to an Azure AI services REST API and receiving a JSON response." border="false":::

The use of REST interfaces with an HTTP endpoint means that any programming language or tool capable of submitting and receiving JSON over HTTP can be used to consume AI services. You can use common programming languages such as Microsoft C#, Python, and JavaScript; as well as utilities such as Postman and cURL, which can be useful for testing.
