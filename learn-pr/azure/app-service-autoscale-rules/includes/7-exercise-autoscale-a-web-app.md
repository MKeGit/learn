Autoscaling is a key part of ensuring that a system remains available and responsive.

You want to implement autoscaling for the hotel reservation system web app, based on the CPU usage of the host. When the CPU utilization rises over a specific threshold, you want the web app to scale out. If the CPU usage drops, you want the web app to scale back in again.

In this unit, you set up the web app and run a test client app that imposes a load on the web app. You see the types of errors that can occur when the web host becomes overloaded. Next, you configure autoscaling for the web app and run the test client again. You monitor the autoscale events that occur and examine how the system responds to the workload.

## Setup

The web app for the hotel reservation system implements a web API. The web API exposes HTTP POST and GET operations that create and retrieve customer bookings. In this exercise, the bookings aren't saved, and the GET operation simply retrieves dummy data.

The exercise also runs a client app that simulates many users issuing POST and GET operations simultaneously. This client app provides the workload for testing how the web app autoscales.

[!include[](../../../includes/azure-exercise-subscription-prerequisite.md)]

1. Sign in to the [Azure portal](https://portal.azure.com/?azure-portal=true).

1. From the Azure portal menu, select **Create a resource**.

1. In the left menu pane, select **Web**, and then search for and select **Web App**. The **Web App** panel appears.

1. Select **Create**. The **Create Web App** panel appears.

1. On the **Basics** tab, enter the following values for each setting.

    > [!NOTE]
    > The web app must have a unique name. We suggest using something like **\<*your name or initials*\>hotelsystem**. Use this name wherever you see *\<your-webapp-name\>* in this exercise.

    | Setting  | Value  |
    |---|---|
    | **Project Details** |
    | Subscription | Select the Azure subscription you'd like to use for this exercise  |
    | Resource Group | Select the **Create new** link, and in the **Name** dialog, enter **mslearn-autoscale** |
    | **Instance Details** |
    | Name | *\<your-webapp-name\>* |
    | Publish | Code |
    | Runtime stack | .NET Core 3.1 (LTS) |
    | Operating System | Windows |
    | Region | Select a region close to you |

1. Select **Review + create**, and then select **Create**.

1. In the top right menu bar of the Azure portal, open the Cloud Shell (first icon in row of menu choices).

1. To download the source code for the hotel reservation system, run the following command.

    ```bash
    git clone https://github.com/MicrosoftDocs/mslearn-hotel-reservation-system.git
    ```

1. Move to the `mslearn-hotel-reservation-system/src` folder.

    ```bash
    cd mslearn-hotel-reservation-system/src
    ```

1. Build the apps for the hotel system. The two apps are (1) a web app that implements the web API for the system and (2) a client app that you use for load testing the web app.

    ```bash
    dotnet build
    ```

1. Prepare the HotelReservationSystem web app for publishing.

    ```bash
    cd HotelReservationSystem
    dotnet publish -o website
    ```

1. Go to the **website** folder containing the published files, zip up the files, and deploy the files to the web app you created in the previous task. Replace `<your-webapp-name>` with the name of your web app.

    ```bash
    cd website
    zip website.zip *
    az webapp deployment source config-zip --src website.zip --name <your-webapp-name> --resource-group mslearn-autoscale
    ```

## Test the web app before configuring autoscaling

1. Using a web browser, go to `https://<your-webapp-name>.azurewebsites.net/api/reservations/1`. Visiting this URL sends a GET request to the web API to retrieve the details of reservation number 1. You should see a result similar to the one that follows. The response contains a JSON document with the details of the booking. Remember that the image shows fictitious data.

    :::image type="content" source="../media/7-web-api-annotated.png" alt-text="Screenshot of a web browser sending a web API request to the hotel reservation system web app.":::

1. Return to the Cloud Shell, and move to the **~/mslearn-hotel-reservation-system/src/HotelReservationSystemTestClient** folder.

   ```bash
   cd ~/mslearn-hotel-reservation-system/src/HotelReservationSystemTestClient
   ```

1. In the Cloud Shell, select the **code** editor (icon with curly brackets), and edit the App.config file in this folder.

    ```bash
    code App.config
    ```

1. Uncomment the line that specifies the **ReservationsServiceURI**, and replace the value with the URL of your web app. The file should look like the example that follows.

    ```text
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="NumClients" value="100" />
            <add key="ReservationsServiceURI" value="https://<your-webapp-name>.azurewebsites.net/"/>
            <add key="ReservationsServiceCollection" value="api/reservations"/>
        </appSettings>
    </configuration>
    ```

    The **NumClients** setting in this file specifies the number of simultaneous clients that attempt to connect to the web app and perform work. The work consists of creating a reservation, and then running a query to fetch the details of a reservation. All the data used is fictitious and isn't persisted anywhere. Leave the **NumClients** value set to 100.

1. Save the file by selecting the ellipsis (...) in the upper right corner of the editor.

1. In the Cloud Shell, edit the HotelReservationSystemTestClient.csproj file in this folder.

    ```bash
    code HotelReservationSystemTestClient.csproj
    ```

1. Edit the line that specifies the **TargetFramework**, so that it matches the Runtime stack you selected for your web app. Change the **TargetFramework** value to `netcoreapp3.1`. The file should look like the following example.

    ```text
    <Project Sdk="Microsoft.NET.Sdk">
    
      <PropertyGroup>
        <OutputType>Exe</OutputType>
        <TargetFramework>netcoreapp3.1</TargetFramework>
      </PropertyGroup>
    
      <ItemGroup>
        <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
        <PackageReference Include="System.Configuration.ConfigurationManager" Version="4.5.0" />
      </ItemGroup>
    
      <ItemGroup>
        <ProjectReference Include="..\HotelReservationSystemTypes\HotelReservationSystemTypes.csproj" />
      </ItemGroup>
    
    </Project>
    ```

1. Save the file by selecting the ellipsis (...) in the upper right corner of the editor, and then close the code editor.

1. Rebuild the test client app with the new configuration.

    ```bash
    dotnet build
    ```

1. Run the client app. You see a number of messages appear as the test clients start running, make reservations, and run queries. Allow the system to run for a couple of minutes. The responses become slow, and soon the client requests start to fail with HTTP 408 (Timeout) errors.

    ```bash
    dotnet run
    ```

   :::image type="content" source="../media/7-web-client-annotated.png" alt-text="Screenshot of a client app running, showing the responses and error messages that occur.":::

1. To stop the client app, press <kbd>Enter</kbd>.

## Enable autoscaling and create a scale condition

1. In the Azure portal, return to your web app.

1. Under **Settings**, select **Scale out (App Service plan)**, and then select **Custom autoscale**.

1. In the **Default** autoscale rule, verify that the scale mode is set to **Scale based on a metric**, and then select **Add a rule**.

    :::image type="content" source="../media/7-add-rule-annotated.png" alt-text="Screenshot of the web app in the Azure portal while configuring autoscaling.":::

1. Add a rule that increases the instance count by one if the average CPU utilization across all instances in the website exceeds 50 percent in the preceding five minutes. This is a scale-out rule.

    :::image type="content" source="../media/7-first-rule-annotated.png" alt-text="Screenshot of the web app in the Azure portal while configuring the autoscaling scale-out rule.":::

1. Select **Add a rule** again. Add a rule that reduces the instance count by one if the average CPU utilization across all instances in the website drops below 30 percent in the preceding five minutes. This is a scale-in rule. Remember that it's good practice to define autoscale rules in pairs.

    :::image type="content" source="../media/7-second-rule-annotated.png" alt-text="Screenshot of the web app in the Azure portal while configuring the autoscaling scale-in rule.":::

1. In the **Default** autoscale condition window, in the **Instance limits** section, set the **Maximum** instance count to five. Name the Autoscale setting **ScaleOnCPU**, and then select **Save**.

    :::image type="content" source="../media/7-web-autoscale-settings-annotated.png" alt-text="Screenshot of the complete autoscale settings for the web app.":::

## Monitor autoscale events

1. Return to the Cloud Shell, go to the **~/hotelsystem/HotelReservationSystemTestClient** folder, and run the test client again.

    ```bash
    cd ~/hotelsystem/HotelReservationSystemTestClient
    dotnet run
    ```

1. While the test client app is running, switch back to the Azure portal showing the autoscale settings for the web app, and select **Run history**. Under **show data for last**, select **1 hour**. Initially, the chart is empty because it takes several minutes for autoscaling to kick in.

1. While you wait for autoscaling events to occur, go to the pane for your web service (not the pane for the App Service plan). Under **Monitoring**, select **Metrics**.

1. Add the following metrics to the chart, set the time range to **Last 30 minutes**, and then pin the chart to the current dashboard:

   - CPU Time. Select the Sum aggregation.
   - Http Server Errors. Select the Sum aggregation.
   - Http 4.xx. Select the Sum aggregation.
   - Average Response Time. Select the Avg aggregation.

1. Allow the system to stabilize, and note the CPU time, the number of HTTP 4.xx errors, and the average response time. Before the system autoscales, you should see many HTTP 4.xx errors (these are HTTP 408 Timeout errors), and the average response time should be several seconds. There also could be the occasional HTTP server error, depending on how the web server copes with the burden.

1. After 10 minutes or so, you should see the following trends in this chart:

   - CPU time jumps up.
   - Number of HTTP 4.xx errors diminishes.
   - Average response time drops.

    :::image type="content" source="../media/7-metrics-chart-annotated.png" alt-text="Screenshot of the Metrics chart for the web app with three lines pointing towards autoscaling events.":::

    Each major spike in the CPU time indicates that more CPU processing power has become available. This change is a result of autoscaling.

1. For the web app and examine the charts, return to the **Overview** page. The overview charts should indicate the following trends:

    - Data In, Data Out, and Requests metrics have increased.
    - Average response time has dropped.
  
    :::image type="content" source="../media/7-overview-charts.png" alt-text="Screenshot of the charts on the Overview page of the web app.":::

1. Select **Scale out (App Service plan)**, and then select **Run history**. Select **1 hour**. The graph should now indicate that autoscaling occurred. The number of instances increased (it might reach five, depending on how long the client app has been running), and you should see several autoscale events reported.

    :::image type="content" source="../media/7-increase-instances.png" alt-text="Screenshot of the chart showing how autoscaling increased the instance count for the web app.":::

    > [!NOTE]
    > Autoscale events are reported in pairs. The first event occurs when autoscaling triggers an increase in the number of instances. The second event occurs when autoscaling completes.

1. Return to the Cloud Shell. You should see that the app runs faster and that far fewer requests fail.

1. To stop the app, press Enter.

1. After several minutes, if you examine the run history of the App Service Plan, you see the number of instances drop. This decrease results from the scale-in rule releasing resources.

You configured autoscaling for the hotel reservation system. The system scaled out when the total CPU usage across all instances hosting the website exceeded 50 percent in a five-minute period. The system scaled back in when the total CPU utilization dropped below 30 percent, again for a five-minute period. You subjected the hotel reservation system to a test load and monitored when autoscaling occurred.
