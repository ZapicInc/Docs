---
title: Android
weight: 20
---

The Zapic SDK for Android can be used in any project with a minimum API level of 19 (KitKat). It can be used in Java 7, Java 8, Kotlin, and Groovy projects. The compiled apps may be distributed in various storefronts including, but not limited to, the Google Play Store, Amazon Appstore, and Samsung Galaxy Apps.

The Zapic SDK for Android is distributed as an Android Archive (AAR) file. It is published to [JCenter](https://bintray.com/bintray/jcenter?filterByPkgName=zapic-sdk-android) and [Maven Central](https://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.zapic.sdk.android%22). It is also published as an attachment to the [GitHub releases](https://github.com/ZapicInc/Zapic-SDK-Android/releases); however, the GitHub releases do not bundle the required dependencies. We strongly encourage developers to leverage Gradle to ensure the required dependencies are downloaded automatically.

# Getting Started

This guide demonstrates integrating the Zapic SDK for Android into an existing app in Android Studio.

## Installing the SDK

In Android Studio, open your app's `build.gradle` file. Set the `minSdkVersion` to 19 or higher, and add the Zapic SDK for Android to the `dependencies` section:

```gradle
android {
  defaultConfig {
      minSdkVersion 19
  }
}

dependencies {
  implementation 'com.zapic.sdk.android:zapic-sdk-android:1.2.1'
}
```

If you are using the Android Plugin for Gradle with a version less than 3.0.0, replace the newer `implementation` dependency configuration with the older `compile` dependency configuration.

## Integrating the SDK

Create a subclass of `android.app.Application` if one is not already defined in your app. Include the name of the `Application` subclass in the `name` attribute of the `application` element in your `AndroidManifest.xml` file. For example, if you create a subclass of `android.app.Application` named `MyApp` in your package namespace you will add the following attribute:

```xml
<application
    android:name=".MyApp"
    ...>
</application>
```

Next, call `Zapic.start` in the `onCreate` method of your `Application` subclass to start the user's session. For example:

```java
import android.app.Application;
import com.zapic.sdk.android.Zapic;

public class MyApp extends Application {
    @Override
    public void onCreate() {
        super.onCreate();

        Zapic.start(this);
    }
}
```

Finally, call `Zapic.attachFragment` in the `onCreate` method of your `Activity` subclasses to ensure important notification messages are displayed to the user and events are processed in the background. For example:

```java
import android.app.Activity;
import com.zapic.sdk.android.Zapic;

public class MyActivity extends Activity {
    @Override
    protected void onCreate(final Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        Zapic.attachFragment(this);
    }
}
```

If your app is comprised of many `Activity` subclasses, ensure the call to `Zapic.attachFragment` is included in all. The Zapic SDK for Android will automatically route important notification messages to the topmost activity.

## Showing Zapic Pages

The Zapic SDK for Android provides all of the required user interface components. You only need to include buttons in your own menus to display the desired page.

Showing Zapic pages is as simple as calling `Zapic.showDefaultPage` or `Zapic.showPage` with the desired page name. The `ZapicPages` class provides constant values for the supported page names. A common use case is to show a Zapic page after a button click. For example:

```java
import com.zapic.sdk.android.Zapic;
import com.zapic.sdk.android.ZapicPages;

myZapicButton.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        Zapic.showDefaultPage(MyActivity.this);
    }
});

myChallengesButton.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        Zapic.showPage(MyActivity.this, ZapicPages.CHALLENGE_LIST);
    }
});
```

You must include a button on your app's primary activity or menu that shows the default Zapic page as described in the [branding guidelines](https://www.zapic.com/brand). You may include additional buttons that jump directly to other Zapic pages from anywhere in your app.

## Submitting Events

Zapic uses a system of [events]({{< ref "platform/events" >}}) to track everything from player activity to calculating statistics to updating achievement progress. These events are automatically processed to update stats, ranks, and challenges and to award achievements.

Submitting a Zapic event is as simple as calling the `Zapic.submitEvent` method with a JSON-encoded object of key value pairs, each representing a single parameter. For example:

```java
import com.zapic.sdk.android.Zapic;
import org.json.JSONObject;

JSONObject parameters = new JSONObject();
o.put("DISTANCE", 147);
o.put("SCORE", 22);
Zapic.submitEvent(parameters);
```

The best time to submit Zapic events is immediately after an important trigger such as the end of a play session or level. Refer to the [Events Guide]({{< ref "platform/events" >}}) for additional details on this powerful system.
