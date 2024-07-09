Intune supports several protected Microsoft apps and partner apps that specially incorporate mobile app management capabilities. Intune protected apps are enabled with a rich set of mobile application protection policies. These apps allow you to:

- Restrict copy-and-paste and save-as functions.
- Configure web links to open inside the secure Microsoft browser.
- Enable multi-identity use and app-level Conditional Access.
- Apply data loss prevention policies without managing the user's device.
- Enable app protection without requiring enrollment.
- Enable app protection on devices managed with third-party EMM tools.

To better understand the available protected apps that integrate with Intune, see a list of [Microsoft Intune protected apps](/mem/intune/apps/apps-supported-intune-apps?azure-portal=true).

## Create protected apps using tools

Normally to add an app to Intune, you would start from Intune and select an app from a list of store apps. Many apps are designed specifically to work with Intune and have extended functionality. These apps are called protected apps. Protected apps incorporate mobile app management capabilities using the Intune App Software Development Kit (SDK) or the App Wrapping Tool for either iOS or Android. You would use these tools if you're an apps developer.

An example of a protected app that can be managed with Intune is Outlook for iOS and Android. You can use Intune app protection and configuration policies with Outlook for iOS and Android to ensure team collaboration experiences are always accessed with safeguards in place. Organizations can use Microsoft Entra Conditional Access policies to ensure that users can only access work or school content using Outlook for iOS and Android.
