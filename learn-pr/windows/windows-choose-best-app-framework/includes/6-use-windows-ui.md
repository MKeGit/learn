Your company wants to build a consumer application to help people manage the files they're syncing to a cloud provider, which must be deployed via the Microsoft Store.

In this scenario, we discuss how each native Windows UI framework can be used to create the file sync app. We also discuss whether it's the best option, based on the latest requirements.

In this unit, you learn the benefits and limitations of the frameworks, and how they may work with the requirements for the file sync app.

## Building the file sync application

The cloud-based file synchronization application is a consumer-facing app. The differentiating requirements to focus on for this application are:

- **Appearance and style of the application:** This application supports modern Windows design and matches the experience of Windows in-box apps. It must be a first-class Windows app with modern experience and great usability.
- **The device compatibility:** The file sync app should run on the latest Windows devices, including desktops and tablet PCs with Intel or Arm processors, and take advantage of modern hardware. The team may decide to support non-Windows platforms in the future.
- **Multimedia support:** The app should support multimedia content, such as images and videos, and provide a rich user experience.
- **Deployment options:** The application is available in the Microsoft Store. There's no need for enterprise deployment scenarios.

## Analyzing the decision criteria

In this section, we analyze the requirements for the file sync app and see how each framework can be used to meet those requirements. We also look at the benefits and limitations of the frameworks and how they may affect the decision of which to use for the file sync app.

### Appearance and style of the application

WinUI applications offer the best possible experience on Windows. The Fluent design system is a set of guidelines for creating apps that look and feel like they belong on Windows. The WinUI design language evolves alongside Fluent to create a design that is human, universal, and truly feels like Windows. WinUI currently provides the best experience for users on Windows. This requirement is a perfect match for the file sync app's requirement to provide the same great experience as in-box Windows apps. WPF and Windows Forms don't offer the same modern experiences and usability. The WPF team is working on adding support for Windows 11 styles in .NET 9, and it's currently available in preview.

### Tablet usability (touch) and device compatibility

WinUI is designed to work seamlessly with touch and pen input. The WinUI team works to ensure that WinUI apps adapt and provide the best experience on all form factors, including tablets, 2-in-1 devices, and desktop PCs. These apps also run great on x86, x64, and Arm64 CPUs. WinUI apps are built to run on Windows 10, version 1809 or later, and Windows 11. Again, this capability is an excellent match for the file sync app's requirement to be usable with touch and pen input. WPF and Windows Forms can be used with touch and pen input, but they don't provide the same experience as WinUI.

### Skillset of the team's enterprise developers

Developers can use C# and .NET or C++ and WinRT to build WinUI apps. Teams that are familiar with XAML and C# or C++ feel at home developing WinUI applications. Developers who have experience with WPF or UWP find that WinUI is similar to those frameworks. In fact, UWP and WinUI share the same XAML and can access many of the same WinRT APIs.

The team who is leading this project is familiar with the latest version of .NET and C#. The developers are also familiar with XAML, so they can use the XAML designer or editor in Visual Studio to build the UI for the application. They're comfortable developing with any of the frameworks being considered for this project.

### Application performance and responsiveness

WinUI apps have a vector-based UI that uses the GPU. XAML-based UIs make the apps performant and responsive. WinUI apps are built on the latest .NET runtime, which is the fastest version of .NET to date. There's no concern about the performance of the application with WinUI. WinUI also has support for multimedia content playback, including images and videos. This capability is a good match for the file sync app's requirement to support multimedia content.

### Deployment scenarios and options

The default WinUI project template creates an app packaged with MSIX. It's the recommended deployment option for WinUI apps but isn't required. MSIX is a Windows app package format that provides a modern packaging experience to all Windows apps. Its package format preserves the functionality of existing app packages and/or installs files. In addition, it enables new modern packaging and deployment features to packaged desktop apps.

There are two ways in which you can deploy packaged WinUI apps using the Windows App SDK.

- **Framework-dependent:** Your app depends on the Windows App SDK runtime and/or Framework package being present on the target machine. Framework-dependent deployment is the default deployment mode of the Windows App SDK for its efficient use of machine resources and serviceability.
- **Self-contained:** Your app carries the Windows App SDK dependencies with it. Self-contained deployment is a deployment option that's available in Windows App SDK 1.1 and later.

Each type of app can be published to the Microsoft Store, and installed that way or via Windows App Installer, Windows Package Manager, or Microsoft Intune.

Windows Forms and WPF applications can also be deployed to the Microsoft Store. In this case, there's no advantage to using WinUI over Windows Forms or WPF for deployment.

## Choosing the framework

WinUI seems like a great match for the file sync app. It works seamlessly with touch and pen input. It also provides the best modern experiences for Windows users. Windows App SDK is built on the .NET 8 runtime, which is the fastest version of .NET to date. It's also easy to deploy WinUI apps to the Microsoft Store. WinUI is a full-featured framework for teams building apps for Windows, and it's the best choice for this project.
