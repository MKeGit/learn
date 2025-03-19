In this module, we'll build a cloud-enabled Spring Boot microservice. It uses a Spring Cloud service registry and a [Spring Cloud Config Server](https://cloud.spring.io/spring-cloud-config), which are both managed and supported by Azure Spring Apps.

This microservice uses Spring Data JPA to read and write data from an [Azure database for MySQL](/azure/mysql/?WT.mc_id=azurespringcloud-mslearn-judubois) database:

- Azure Spring Apps automatically binds that database to our service.
- Azure database for MySQL is a fully managed version of MySQL, running on Azure.

## Create the application on Azure Spring Apps

Create a specific `todo-service` application in your Azure Spring Apps instance:

```bash
az spring app create --name todo-service --resource-group "$RESOURCE_GROUP_NAME" --service "$SPRING_CLOUD_NAME" --runtime-version Java_17
```

## Create a MySQL database

Now create an Azure database for MySQL:

```bash
az mysql server create \
    --name ${SPRING_CLOUD_NAME}-mysql \
    --resource-group "$RESOURCE_GROUP_NAME" \
    --sku-name B_Gen5_1 \
    --storage-size 5120 \
    --admin-user "spring"
```

This operation can take a few minutes, and outputs a JSON document: copy the **password** attribute in that document, as we'll use it later.

Now create a **todos** database in that server, and open up its firewall so that Azure Spring Apps can access it:

```bash
az mysql db create \
    --name "todos" \
    --server-name ${SPRING_CLOUD_NAME}-mysql
```

```bash
az mysql server firewall-rule create \
    --name ${SPRING_CLOUD_NAME}-mysql-allow-azure-ip \
    --resource-group "$RESOURCE_GROUP_NAME" \
    --server ${SPRING_CLOUD_NAME}-mysql \
    --start-ip-address "0.0.0.0" \
    --end-ip-address "0.0.0.0"
```

Once this operation completes, you can have a look at what was created in the resource group that you created for this workshop.

## Bind the MySQL database to the application

Azure Spring Apps can automatically bind the MySQL database we created to our microservice.

1. Navigate to your Azure Spring Apps instance.
1. Select **Apps**.
1. Select the **todo-service** application.
1. Select **Service Connector** and then choose **+ Create**.
    1. For **Service type**, select **DB for MySQL single server**.
    2. Specify a connection name, for example *mysql_todos*.
    3. Verify that the correct subscription is shown.
    4. Choose the MySQL server created in the preceding steps.
    5. Select the MySQL database created earlier.
    6. Select **SpringBoot** as the Client type.
    7. Select the **Next: Authentication** button.
1. On the **Authentication** page, verify that **Connection string** is selected.
1. Select **Continue with...Database credentials** and fill in the username and password fields. The username is "spring" and the password is the password attribute that we copied earlier.

    > [!NOTE]
    > If you forget your password, you can reset it by using `az mysql server update -n ${SPRING_CLOUD_NAME}-mysql -g "$RESOURCE_GROUP_NAME" -p <new-password>`

1. Verify that **Configure firewall rules to enable access to target service** is selected.
1. Click on **Next: Review + Create**.
1. After the **Validation passed** message appears, select the **Create** button to create the Service Connector.

## Create a Spring Boot microservice

Now that we provisioned the Azure Spring Apps instance and configured the service binding, let's get the code for `todo-service` ready.

To create our microservice, we'll use [https://start.spring.io](https://start.spring.io) with the command line:

```bash
curl https://start.spring.io/starter.tgz -d type=maven-project -d dependencies=web,mysql,data-jpa,cloud-eureka,cloud-config-client -d baseDir=todo-service -d bootVersion=3.1.5.RELEASE -d javaVersion=17 | tar -xzvf -
```

> [!NOTE]
> We use the `Spring Web`, `MySQL Driver`, `Spring Data JPA`, `Eureka Discovery Client`, and the `Config Client` components.

## Add Spring code to manage data using Spring Data JPA

Next to the `DemoApplication` class, create a `Todo` JPA entity:

```java
package com.example.demo;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;

@Entity
public class Todo {

    public Todo() {
    }

    public Todo(String description, boolean done) {
        this.description = description;
        this.done = done;
    }

    @Id
    @GeneratedValue
    private Long id;

    private String description;

    private boolean done;

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getDescription() {
        return description;
    }

    public void setDescription(String description) {
        this.description = description;
    }

    public boolean isDone() {
        return done;
    }

    public void setDone(boolean done) {
        this.done = done;
    }
}

```

Then, create a Spring Data JPA repository to manage this entity, called `TodoRepository`:

```java
package com.example.demo;

import org.springframework.data.jpa.repository.JpaRepository;

public interface TodoRepository extends JpaRepository<Todo, Long> {
}
```

And finish coding this application by adding a Spring MVC controller called `TodoController`:

```java
package com.example.demo;

import org.springframework.web.bind.annotation.*;

import javax.annotation.PostConstruct;
import java.util.Arrays;

@RestController
public class TodoController {

    private final TodoRepository todoRepository;

    public TodoController(TodoRepository todoRepository) {
        this.todoRepository = todoRepository;
    }

    @PostConstruct
    public void init() {
        todoRepository.saveAll(Arrays.asList(
                new Todo("First item", true),
                new Todo("Second item", true),
                new Todo("Third item", false)));
    }

    @GetMapping("/")
    public Iterable<Todo> getTodos() {
        return todoRepository.findAll();
    }
}
```

## Configure Spring Boot to create the database tables

In order to automatically generate the database tables when the application is deployed, add this line to your `src/main/resources/application.properties` configuration file:

```yaml
spring.jpa.hibernate.ddl-auto=create-drop
```

## Deploy the application

You can now build your *todo-service* project and send it to Azure Spring Apps:

```bash
cd todo-service
./mvnw clean package -DskipTests
az spring app deploy --name todo-service --service "$SPRING_CLOUD_NAME" --resource-group "$RESOURCE_GROUP_NAME" --artifact-path target/demo-0.0.1-SNAPSHOT.jar
cd ..
```

If you want to check the logs of the application, in case something fails, you can use the `az spring app logs` command:

```bash
az spring app logs --name todo-service --service "$SPRING_CLOUD_NAME" --resource-group "$RESOURCE_GROUP_NAME" -f
```

## Test the project in the cloud

Now that the application is deployed, it's time to test it!

1. In the Azure portal, go to **Apps** in your Azure Spring Apps instance.
    1. Verify **todo-service** has a **Registration status** that says **0/1**. This information shows that it's correctly registered in the Spring Cloud service registry.
    1. Select **todo-service** to have more information on the microservice.
1. Copy/paste the "Test Endpoint" that is provided.

You can now use cURL to test the endpoint. Your test command should look like:

```bash
curl https://primary:XXXXXXXXXXXXXXXXXXXXXXXXXXXXX@azure-spring-cloud-workshop.test.azuremicroservices.io/todo-service/default/
```

And the result of this command should be the three items that were previously inserted in the MySQL database:

```json
[{"id":"1","description":"First item","done":true},{"id":"2","description":"Second item","done":true},{"id":"3","description":"Third item","done":false}]
```
