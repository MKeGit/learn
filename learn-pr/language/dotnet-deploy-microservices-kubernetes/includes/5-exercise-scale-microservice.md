Your microservice might come under heavy load during certain times of the day. Kubernetes makes it easy to scale your microservice by adding more instances for you.

1. In the codespace, on the **TERMINAL** tab, run the following command to scale the backend microservice to five instances:

    ```bash
    kubectl scale --replicas=5 deployment/productsbackend
    ```

    The reason we need to specify **deployment/productsbackend** instead of just **productsbackend** is because we're scaling the entire Kubernetes deployment of the backend service, and that scales the instances of the individual pods correctly.

1. To verify five instances are up and running, run this command:

    ```bash
    kubectl get pods
    ```

    Once all the instances are spun up, you should see five pod instances (represented as individual rows) in the output. Each row starts with **productsbackend** and is then followed by a random string.

1. To scale the instance back down, run the following command:

    ```bash
    kubectl scale --replicas=1 deployment/productsbackend
    ```