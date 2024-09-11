Self-contained deployments include the app and its dependencies, as well as the .NET runtime. Since the .NET runtime is included with the app, the target machine doesn't need to have the .NET runtime installed in order to run the app. This makes self-contained deployments larger than framework-dependent deployments, but it also makes them more portable. It also makes it easier to run multiple versions of the .NET runtime side by side on the same machine.

Your IT department has notified your team that for disaster recovery purposes, they are testing your app on servers that don't have the .NET runtime installed. They intend to test the app on both a 64-bit Windows server and a 64-bit Linux server. To support this testing, you need to publish the app as a self-contained deployment for each environment.

In this exercise, you'll publish an ASP.NET Core app as self-contained deployments for Windows and Linux.

## Create another ASP.NET Core app

1. In the terminal window, set your location to the *MyWebApp* directory. At the end of the previous exercise, you were in *MyWebApp/publish-fd*. You need to go back to the *MyWebApp* directory.

    ```dotnetcli
    cd ..
    ```

    You should now be in the *MyWebApp* directory.

1. Run the following command to publish the app as a self-contained deployment for 64-bit Windows:

    ```dotnetcli
    dotnet publish -c Release -r win-x64 -o publish-scd-win64 --self-contained
    ```

    In the previous command:

    - `-c Release` specifies that the app should be built in release mode. This optimizes the app for performance.
    - `-r win-x64` specifies that the app should be published for 64-bit Windows. `win-x64` is the [runtime identifier](/dotnet/core/rid-catalog) (RID) for 64-bit Windows, so the app will be published as a self-contained deployment for 64-bit Windows.
    - `-o publish-scd-win64` specifies the output directory for the published app.
    - `--self-contained` specifies that the app should be published as a self-contained deployment.

    This command builds and publishes the app as a self-contained deployment for 64-bit Windows to the *publish-scd-win64* directory.

1. Set your location to the *publish-scd-win64* directory and list the files in the directory.

    ```dotnetcli
    cd publish-scd-win64
    dir
    ```

    Note that the list of files is much larger than the list of files in the *publish-fd* directory. This is because the self-contained deployment includes the same files as the framework-dependent deployment, as well as the .NET runtime. The *MyWebApp.exe* file is the 64-bit Windows executable for the app.

1. Run the following command to publish the app as a self-contained deployment for 64-bit Linux:

    ```dotnetcli
    dotnet publish -c Release -r linux-x64 -o publish-scd-linux64 --self-contained
    ```

    This time, the `-r linux-x64` option specifies that the app should be published for 64-bit Linux.

1. Set your location to the *publish-scd-linux64* directory and list the files in the directory.

    ```dotnetcli
    cd publish-scd-linux64
    dir
    ```

    The list of files in the *publish-scd-linux64* directory is similar to the list of files in the *publish-scd-win64* directory, but the executable file is named *MyWebApp* instead of *MyWebApp.exe*. This is because Linux doesn't use file extensions to determine file types. After you deploy the app to a Linux server, you'll need to grant execute permission to the *MyWebApp* file with the `chmod +x` command before it can run.

