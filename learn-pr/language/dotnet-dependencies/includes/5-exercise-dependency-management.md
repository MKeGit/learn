Dependencies that you use in your apps can be updated often and may contain new features, bug fixes, and critical security updates. The app that you created is small, and has only a single dependency. Updating it should be straightforward. To take advantage of the latest features, see if you can update the app.

## Upgrade app dependencies

1. In the **DotNetDependencies.csproj** file, look at the `dependencies`. It should look like this code:

    ```xml
    <ItemGroup>
        <PackageReference Include="Humanizer" Version="2.7.9" />
    </ItemGroup>
    ```

1. To see installed dependencies, run this command:

   ```dotnetcli
   dotnet list package
   ```

   This should output the requested version and the final resolved (installed) version

   ```output
   Top-level Package      Requested   Resolved
   > Humanizer            2.7.9        2.7.9
   ```

1. To see what dependencies are outdated, run this command:

   ```dotnetcli
   dotnet list package --outdated
   ```

   The output should look something like the following output. You might get different values in the `Latest` column.

   ```output
   Project `DotNetDependencies` has the following updates to its packages
      [net8.0]:
      Top-level Package      Requested   Resolved   Latest
      > Humanizer            2.7.9       2.7.9      2.11.10
   ```

   By default, this command will check for the latest stable version. To check for pre-release packages, append `--include-prerelease` to the previous command:

   ```dotnetcli
   dotnet list package --outdated --include-prerelease
   ```

1. You can, with some level of confidence, update to the `Latest` version. Doing so will ensure the dependencies get the latest features and patches in that major version. To install the latest version, run the following command:

   ```dotnetcli
   dotnet add package Humanizer 
   ```

   You should get output similar to the following:

   ```output
   info : PackageReference for package 'Humanizer' version '2.11.10' updated in file 'C:\Users\username\Desktop\DotNetDependencies\DotNetDependencies.csproj'.
   ```

   The output states that your project dependencies have been updated.

   If you want to upgrade to a specific version of the dependency, you can append the `--version` parameter and specify the specific version.

   ```dotnetcli
   dotnet add package Humanizer --version 2.11.10
   ```

   Lastly, you can also install the latest pre-release package by appending the `--prerelease` parameter.

   ```dotnetcli
   dotnet add package Humanizer --prerelease
   ```

   Your results might be slightly different. The listed version should correspond to the latest available version of the package.

Congratulations. You've upgraded the dependency in your app. Well done!
