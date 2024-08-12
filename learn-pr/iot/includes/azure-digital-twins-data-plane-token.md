---
author: baanders
ms.author: baanders
ms.date: 08/09/2024
ms.topic: include
ms.service: azure-digital-twins
---

>[!TIP]
>If your data plane bearer token from [Unit 2](../explore-azure-digital-twins-api-for-creating-graph/2-set-up-http-file.yml) has expired, you'll get a *401 Unauthorized* error. Remember that you can re-run the `az account get-access-token --resource 0b07f429-9f4b-4714-9392-cc5e8e80c8b0` command to get a new token, and update the value of the `DPtoken` variable at the top of *data.http*.