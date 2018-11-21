---
title: Unity
weight: 10
---

The Zapic SDK for Unity can be used in any project in Unity 5.6 or higher exported for iOS or Android.

When exporting for iOS, the Zapic SDK for Unity can be used in any project with a target minimum iOS version of 9.0. Under the hood, the Zapic SDK for Unity simply wraps the Zapic SDK for iOS. Refer to the [iOS Guide]({{< ref "sdk/ios" >}}) for additional iOS platform details.

When exporting for Android, the Zapic SDK for Unity can be used in any project with a minimum API level of 19 (KitKat). The compiled apps may be distributed in various storefronts including, but not limited to, the Google Play Store, Amazon Appstore, and Samsung Galaxy Apps. Under the hood, the Zapic SDK for Unity simply wraps the Zapic SDK for Android. Refer to the [Android Guide]({{< ref "sdk/android" >}}) for additional Android platform details.

The Zapic SDK for Unity is distributed as a `.unitypackage`. It is published as an attachment to the [GitHub releases](https://github.com/ZapicInc/Zapic-SDK-Unity/releases).

# Getting Started

This guide demonstrates integrating the Zapic SDK for Unity into an existing app in Unity.

## Installing the SDK

Download the latest Zapic SDK for Unity from the [GitHub releases](https://github.com/ZapicInc/Zapic-SDK-Unity/releases/latest), and extract the `Zapic.unitypackage` file from the ZIP file.

In Unity, import the contents of the `Zapic.unitypackage` into your project using the menu item "Assets" > "Import Package" > "Custom Package...". The "Examples" directory is optional.

When exporting for Android, the Zapic SDK for Unity leverages Google's [Unity JAR Resolver](https://github.com/googlesamples/unity-jar-resolver) to download the required dependencies. You may run the resolver using the menu item "Assets" > "Play Services Resolver" > "Android Resolver" > "Resolve".

{{< figure src="/img/unity_1_jar_resolver.png" width="400" height="100" >}}

## Integrating the SDK

In your first scene, simply call `Zapic.Start` in the `Start` or `Awake` methods of a `GameObject` in the scene. For example:

```c#
void Start()
{
    Zapic.Start();
}
```

## Showing Pages

The Zapic SDK for Unity provides all of the required user interface components. You only need to include buttons in your own menus to display the desired page.

Showing Zapic pages is as simple as calling `Zapic.ShowDefaultPage` or `Zapic.ShowPage` with the desired page name. The `ZapicPages` class provides constant values for the supported page names. A common use case is to show a Zapic page after a button click. For example:

```c#
private void ShowZapic()
{
    Zapic.ShowDefaultPage();
}

private void ShowChallenges()
{
    Zapic.ShowPage(ZapicPages.Challenges);
}
```

You must include a button on your app's main menu that shows the default Zapic page as described in the [branding guidelines](https://www.zapic.com/brand). You may include additional buttons that jump directly to other Zapic pages from anywhere in your app.

## Submitting Events

Zapic uses a system of [events]({{< ref "platform/events" >}}) to track everything from player activity to calculating statistics to updating achievement progress. These events are automatically processed to update stats, ranks, and challenges and to award achievements.

Submitting a Zapic event is as simple as calling the `Zapic.SubmitEvent` method with a collection of key value pairs, each representing a single parameter. For example:

```c#
var parameters = new Dictionary<string, object>();
parameters.Add("Distance", 147);
parameters.Add("Score", 22);
Zapic.SubmitEvent(parameters);
```

The best time to submit Zapic events is immediately after an important trigger such as the end of a play session or level. Refer to the [Events Guide]({{< ref "platform/events" >}}) for additional details on this powerful system.

## Handling Interactions

Zapic integrates with device features as well as 3rd party services in order to build a better experience for your players. A common example of a 3rd party integration is a linking services that allow players to invite their friends to a challenge via a "Share Sheet" by posting a message of Facebook or sending an SMS.

In some of these cases Zapic will attach special meta data that allows Zapic to automatically react to a user interacting with Zapic generated content. Continuing with our example: when a challenge invite link is clicked, a challenge invitation page will automatically open in Zapic allowing the player to accept or reject the invite. In this case the meta data associated with this link would indicate that the link is for a challenge and also include the specific id of the challenge.

It is the responsibility of the developer to pass this meta data from the 3rd party to Zapic so it can be processed by the Zapic SDK. The `HandleInteraction` method should be called with the required meta data so Zapic can automatically respond to the player's actions.

```c#
Zapic.HandleInteraction({data})
```

Please check specific integration guides for details on using `HandleInteraction`.

## Player Management

Player authentication and identity management are a critical component to many games, allowing players to play on multiple devices or participate in a multiplayer match. Zapic automatically manages player accounts and exposes player information so it can be used from within the game. For more details review the detailed [player information]({{< ref "platform/players" >}})

### Handling Players

When a player successfully with Zapic, your game will be notified with the newly logged in player information. In order to receive the player notifications you must set the `OnLogin` and `OnLogout` callbacks. These handlers should be set before calling `Start` to ensure all player notifications are handled by your game.

```c#
using UnityEngine;

public class ExampleStartup : MonoBehaviour
{
    void Start()
    {
        Zapic.OnLogin = ((player) =>
        {
            //Do stuff here
        });

        Zapic.OnLogout = ((player) =>
        {
            //Do stuff here
        });

        Zapic.Start();
    }
```

## iOS

### Permissions

Zapic requires a handful of common permissions to function properly, these include camera access in order to allow players to customize their Zapic profile. These permissions are automatically handled for you via the SDK. All the required permissions are automatically added for you as part of a "PostBuildProcess" that is run when Unity exports the XCode project. If you wish to update the permission request text you can update the exported `.plist` file.

### Enable Modules

Zapic uses objective c modules to automatically add references to core frameworks. The "PostBuildProcess" should automatically enable modules for your project. If you encounter issues with Frameworks not being found, please check that modules are enabled.

![Example Zapic Menu Button](/img/ios-modules-setting.png)

### IDFA

IDFA is the abbreviation for identifier for advertisers on iOS. The IDFA allows Zapic to track a user when they click on an advertisement or promotion in order to attribute that install back to your app or game. Users may opt out if IDFA tracking via their iOS settings.

After integrating the Zapic SDK, you need to let Apple know that you use the IDFA. To follow proper protocol when submitting your next release to the App Store, you should:

1. Answer `Yes` to the question **Does this app use the Advertising Identifier (IDFA)?**
2. Check the two boxes for:
   1. **Attribute this app installation to a previously served advertisement**
   2. **Attribute an action taken within this app to a previously served advertisement**

## Android

### Runtime Permissions

By default Unity will automatically prompt the user for all permissions that the app uses when the game launches for the first time. Zapic supports runtime permissions, meaning that the user will be asked to grant the permission when a feature required elevated rights is accessed. You can enable runtime permissions by updating your Manifest. For more info check out the Unity docs for [Runtime permissions in Android 6.0 (Marshmallow)](https://docs.unity3d.com/Manual/android-manifest.html)

```
<meta-data android:name="unityplayer.SkipPermissionsDialog" android:value="true" />
```

{{% notice warning %}}
Adding this completely suppresses the permission dialog shown on startup, but you must handle runtime permissions carefully to avoid crashes. Zapic fully supports this, but it may cause issues if you use other SDKs or tools that dont support runtime permissions.
{{% /notice %}}
