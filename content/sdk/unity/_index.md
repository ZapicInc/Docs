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
