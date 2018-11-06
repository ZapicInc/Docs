---
title: iOS
weight: 20
---

## Installing the SDK

The Zapic iOS SDK is provided as a Swift framework. It can be used in both Swift and Objective-C projects that target iOS 9.0 and above.

{{% notice note %}}
Zapic requires iOS 9.0 or newer. Please ensure your iOS target is properly set for your project.
{{% /notice %}}

{{% notice warning %}}
The 2.0.0 release of Zapic now requires you to configure your [IDFA settings]({{< ref "#idfa" >}}) when submitting your app to the App Store. Please ensure your settings are correct to ensure your app is not rejected.
{{% /notice %}}

### Install using CocoaPods

[CocoaPods](http://cocoapods.org) is a dependency manager for Cocoa projects. You can install it with the following command:

```bash
$ gem install cocoapods
```

To integrate Zapic into your Xcode project using CocoaPods, specify it in your `Podfile`:

```ruby
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '9.0'
use_frameworks!

target '<Your Target Name>' do
    pod 'Zapic', '~> 2.0.0'
end
```

Then, run the following command:

```bash
$ pod install
```

### Install using Carthage

[Carthage](https://github.com/Carthage/Carthage) is a decentralized dependency manager that can install, update, and build your game's dependencies. Carthage is the recommended way to install and update the Zapic iOS SDK in your game.

You can install Carthage with [Homebrew](http://brew.sh/) using the following commands:

```bash
$ brew update
$ brew install carthage
```

Add the Zapic iOS SDK as a dependency of your project by adding the following line to your `Cartfile`:

```none
github "ZapicInc/Zapic-SDK-iOS" ~> 1.3.0
```

Use Carthage to download and build the framework using the following command:

```bash
$ carthage update
```

Finally, drag the built `Zapic.framework` file from the `Carthage` directory in your project into the Xcode project directory.

## Configuring Permissions

Zapic requires some common permissions to be elevated in order to function properly.

{{% notice warning %}}
These setting must be included in your Info.plist file or your app may crash when users access specific features within Zapic.
{{% /notice %}}

### Photos Permissions

Zapic allows players to upload a profile photo from the user's photo album. Before submitting your app to Apple you must configure the `info.plist` to include the `NSPhotoLibraryUsageDescription`. You must also provide a description that will be displayed to the user before they can upload a photo, letting them know why they should grant permission. The standard description is:

```none
Zapic will only use the Photos you select.
```

### Camera Permissions

Zapic allows players to take a profile photo with the camera. Before submitting your app to Apple you must configure the `info.plist` to include the `NSCameraUsageDescription`. You must also provide a description that will be displayed to the user before they can take a photo, letting them know why they should grant permission. The standard description is:

```none
Zapic allows you to take photos.
```

## Initializing

It is important to initialize Zapic as early as possible in your game's startup process. This places your game on the player's activity feed and increases the accuracy of your player analytics.

Initializing Zapic is as simple as importing the framework and calling the `start` method from within the `AppDelegate` application methods. For example:

```swift
import Zapic

func application(_ application: UIApplication, didFinishLaunching...) -> Bool {
    Zapic.start()
    return true
}
```

## Player Management

Player authentication and identity management are a critical component to many games, allowing players to play on multiple devices or participate in a multiplayer match. Zapic automatically manages player accounts and exposes player information so it can be used from within the game. For more details review the detailed [player information]({{< ref "platform/players" >}})

### Handling Players

When a player successfully with Zapic, your game will be notified with the newly logged in player information. In order to receive the player notifications you must set the `onLoginHandler` and `onLogoutHandler`. These handlers should be set before calling `start` to ensure all player notifications are handled by your game.

```swift
//AppDelegate.swift
import Zapic

@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {

  func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {

    Zapic.onLoginHandler = {(newPlayer: ZapicPlayer) -> Void in
        //Do stuff here
    }

    Zapic.onLogoutHandler = {(prevPlayer: ZapicPlayer) -> Void in
        //Do stuff here
    }

    Zapic.start()

    return true
  }
```

or

```objc
//AppDelegate.m
@import Zapic;

@implementation AppDelegate

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

  [Zapic setOnLoginHandler:^(ZapicPlayer * newPlayer){
    //Do stuff here
  }];

  [Zapic setOnLogoutHandler:^(ZapicPlayer * prevPlayer){
    //Do stuff here
  }];

  [Zapic start];

  return YES;
}

@end
```

## Showing Pages

The Zapic iOS SDK allows you to show all of the required UI components. You only need to include buttons in your own game menus to launch the desired Zapic page.

Showing Zapic is as simple as calling `showDefaultPage` or `showPage` with the desired page name. The usual place to launch a Zapic page is from within the action selector of a button. For example:

```swift
import Zapic

func showZapicChallengesAction(sender: UIButton!) {
    Zapic.showPage(ZapicPages.challenges)
}

func showZapicDefaultAction(sender: UIButton!) {
    Zapic.showDefaultPage())
}
```

or

```objc
@import Zapic;

- (void) showZapicChallengesAction {
    [Zapic showPage:@"challenges"];
}

- (void) showZapicDefaultAction {
    [Zapic showDefaultPage];
}
```

The default page is the main page within Zapic that gives players access to all the included features. You must include a button on your primary game menu that shows the default page as described in the [branding guidelines](https://www.zapic.com/brand). You may include additional buttons that jump directly to other pages from anywhere in your game (e.g. challenges or stats).

## Submitting Events

Zapic uses a system of [events]({{< ref "platform/events" >}}) to track everything from player activity to achievement progress and high scores. These events are automatically processed to award achievements and to update challenges.

Submitting Zapic events is as simple as calling the `submitEvent` method with a collection of key value pairs, each representing a single parameter. The best time to submit Zapic events is as soon as the desired trigger within your game occurs. Events can have 1 to n parameters, here is an example of sending events:

```swift
import Zapic

Zapic.submitEvent(["Distance": 147,"Score":22])
```

or

```objc
@import Zapic;

[Zapic submitEvent:@{ @"Distance": @147,@"Score":@22}];
```

Be sure to review the [Events]({{< ref "platform/events" >}}) guide for the complete details on this powerful system.

## Handling Interactions

Zapic integrates with device features as well as 3rd party services in order to build a better experience for your players. A common example of a 3rd party integration is a linking services that allow players to invite their friends to a challenge via a "Share Sheet" by posting a message of Facebook or sending an SMS.

In some of these cases Zapic will attach special meta data that allows Zapic to automatically react to a user interacting with Zapic generated content. Continuing with our example: when a challenge invite link is clicked, a challenge invitation page will automatically open in Zapic allowing the player to accept or reject the invite. In this case the meta data associated with this link would indicate that the link is for a challenge and also include the specific id of the challenge.

It is the responsibility of the developer to pass this meta data from the 3rd party to Zapic so it can be processed by the Zapic SDK. The `handleInteraction` method should be called with the required meta data so Zapic can automatically respond to the player's actions.

```swift
import Zapic

Zapic.handleInteraction({data})
```

or

```objc
@import Zapic;

 [Zapic handleInteraction:{data}];
```

Please check specific integration guides for details on using `handleInteraction`.

## IDFA

IDFA is the abbreviation for identifier for advertisers on iOS. The IDFA allows Zapic to track a user when they click on an advertisement or promotion in order to attribute that install back to your app or game. Users may opt out if IDFA tracking via their iOS settings.

After integrating the Zapic SDK, you need to let Apple know that you use the IDFA. To follow proper protocol when submitting your next release to the App Store, you should:

1. Answer `Yes` to the question **Does this app use the Advertising Identifier (IDFA)?**
2. Check the two boxes for:
   1. **Attribute this app installation to a previously served advertisement**
   2. **Attribute an action taken within this app to a previously served advertisement**

## Common Issues

### Enable Modules

Zapic uses objective c modules to automatically add references to core frameworks. If you encounter issues with Frameworks not being found or imports failing, please check that modules are enabled.

![Example Zapic Menu Button](/img/ios-modules-setting.png)
