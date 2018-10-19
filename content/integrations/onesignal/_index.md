---
title: 'OneSignal'
weight: 10
---

## What is OneSignal?

OneSignal is a high volume and reliable push notification service for websites and mobile applications. They support all major native and mobile platforms by providing dedicated SDKs for each platform, a RESTful server API, and an online dashboard for marketers to design and send push notifications.

## Setup OneSignal SDK

The first step is to configure OneSignal and setup the SDK for your desired platform [iOS](https://documentation.onesignal.com/docs/ios-sdk-setup), [Android](https://documentation.onesignal.com/docs/android-sdk-setup), or [Unity](https://documentation.onesignal.com/docs/unity-sdk-setup).

## Configure the Zapic Developer Portal

Once you have created your OneSignal application, you will need to give Zapic your `ONESIGNAL APP ID` & `REST API KEY` in order for Zapic to send push notifications on your behalf to your players. These can be found in the OneSignal Dashboard under "Settings" > "Keys & IDs"

## Tag a Device

OneSignal allows you to [tag users with meta data](https://documentation.onesignal.com/docs) in order to target them when sending a push notifications. Zapic will send notifications to specific users based on actions taken within Zapic (ex. challenge invitiations). In order to deliver this message to the correct player, you must tag the player with the key `zapic_player_token` and the `NotificationToken` provided when a player logs in.

{{% notice warning %}}
If you do not tag the player, they will not receive any push notifications from Zapic.
{{% /notice %}}

You will also need to delete the notification tag when the player logs out of Zapic so that device will no longer receive notifications for that user.

### iOS - Swift

```objc
 func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
    // Replace 'YOUR_APP_ID' with your OneSignal App ID.
    OneSignal.initWithLaunchOptions(launchOptions,
        appId: "YOUR_APP_ID",
        handleNotificationAction: { (result) in
            let data = result?.notification.payload.additionalData
            Zapic.handleInteraction(data)
        },
        settings: onesignalInitSettings)

    OneSignal.inFocusDisplayType = OSNotificationDisplayType.notification;

    //Update OneSignal when the player is logs into Zapic
    Zapic.onLoginHandler = {(player: ZapicPlayer) -> Void in
        OneSignal.sendTag(Zapic.notificationTag, value:player.notificationToken);
    }

    //Remove the previousPlayer from OneSignal when the player is logs out of Zapic
    Zapic.onLogoutHandler = {(prevPlayer: ZapicPlayer) -> Void in
        OneSignal.deleteTag(Zapic.notificationTag);
    }

    Zapic.start()
}
```

### Unity

```csharp
void Start() {
    // Replace 'YOUR_APP_ID' with your OneSignal App ID.
    OneSignal.StartInit("YOUR_APP_ID")
        .HandleNotificationOpened(HandleNotificationOpened)
        .EndInit();

    // Update OneSignal when the player logs into Zapic
    Zapic.OnLogin = (player) =>
    {
        OneSignal.SendTag(Zapic.NotificationTokenKey, player.NotificationToken);
    };

    Zapic.OnLogout = (prevPlayer) =>
    {
        OneSignal.DeleteTag(Zapic.NotificationTokenKey);
    };

    Zapic.Start();
}
```

### Android

```java
public class MainApplication extends Application {
    @Override
    public void onCreate() {
        super.onCreate();

        // Initialize Zapic.
        Zapic.start(this);
        Zapic.setPlayerAuthenticationHandler(new ZapicPlayerAuthenticationHandler() {
            @Override
            public void onLogin(@NonNull ZapicPlayer player) {
                // Associate player/device with OneSignal for push notifications.
                OneSignal.sendTag(Zapic.NOTIFICATION_TAG, player.getNotificationToken());
            }

            @Override
            public void onLogout(@NonNull ZapicPlayer player) {
                // Disassociate player/device from OneSignal for push notifications.
                OneSignal.deleteTag(Zapic.NOTIFICATION_TAG);
            }
        });

        // Initialize OneSignal.
        OneSignal.startInit(this)
                .inFocusDisplaying(OneSignal.OSInFocusDisplayOption.Notification)
                .unsubscribeWhenNotificationsAreDisabled(true)
                .setNotificationOpenedHandler(new OneSignal.NotificationOpenedHandler() {
                    @Override
                    public void notificationOpened(OSNotificationOpenResult result) {
                        JSONObject data = result.notification.payload.additionalData;
                        if (data != null) {
                            Zapic.handleInteraction(data);
                        }
                    }
                })
                .init();
    }
}
```

## Handle Notification Actions

When Zapic send a push notification to a player sometimes we attach metadata that lets the app know what to do when the notification is opened. An example of this would be information about which challenge the user was invited to so we can open up directly to that challenge page. As a developer, you need to get this data from the OneSignal SDK and pass it to the Zapic SDK so it can be processed. All SDKs support a `HandleInteraction` method that is responsible for processing this meta data.

### iOS

```swift
// Replace 'YOUR_APP_ID' with your OneSignal App ID.
OneSignal.initWithLaunchOptions(launchOptions,
    appId: "YOUR_APP_ID",
    handleNotificationAction: { (result) in
        let data = result?.notification.payload.additionalData
        Zapic.handleInteraction(data)
    },
    settings: onesignalInitSettings)
```

### Unity

```c#
void Start() {
    // Replace 'YOUR_APP_ID' with your OneSignal App ID.
    OneSignal.StartInit("YOUR_APP_ID")
        .HandleNotificationOpened(HandleNotificationOpened)
        .EndInit();
}

private static void HandleNotificationOpened(OSNotificationOpenedResult result)
{
    if (result == null)
        return;

    var data = result.notification.payload.additionalData;

    Zapic.HandleInteraction(data);
}
```

### Android

```java
public class MainApplication extends Application {
    @Override
    public void onCreate() {
        super.onCreate();

        // Initialize Zapic.
        Zapic.start(this);
        Zapic.setPlayerAuthenticationHandler(new ZapicPlayerAuthenticationHandler() {
            @Override
            public void onLogin(@NonNull ZapicPlayer player) {
                // Associate player/device with OneSignal for push notifications.
                OneSignal.sendTag(Zapic.NOTIFICATION_TAG, player.getNotificationToken());
            }

            @Override
            public void onLogout(@NonNull ZapicPlayer player) {
                // Disassociate player/device from OneSignal for push notifications.
                OneSignal.deleteTag(Zapic.NOTIFICATION_TAG);
            }
        });

        // Initialize OneSignal.
        OneSignal.startInit(this)
                .inFocusDisplaying(OneSignal.OSInFocusDisplayOption.Notification)
                .unsubscribeWhenNotificationsAreDisabled(true)
                .setNotificationOpenedHandler(new OneSignal.NotificationOpenedHandler() {
                    @Override
                    public void notificationOpened(OSNotificationOpenResult result) {
                        JSONObject data = result.notification.payload.additionalData;
                        if (data != null) {
                            Zapic.handleInteraction(data);
                        }
                    }
                })
                .init();
    }
}
```

## Monitor & Track User Engagement

Since Zapic is sending push notifications through the OneSignal APIs you will be able to monitor user engagement with the push notifications just like you do with any other push notification that you already send.

Push notifications that Zapic sends are visible under the "Delivery" tab in the OneSignal Dashboard.
