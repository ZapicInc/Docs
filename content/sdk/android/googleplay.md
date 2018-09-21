//Old google play android docs

## Configuring Google Play Games Services

Open the [Google Play Console](https://play.google.com/apps/publish/).

Navigate to the "Games services" section in the left navigation menu and select the desired game from the list.

{{< figure src="/img/play_1_navigate.png" width="900" height="400" >}}

Navigate to the "Linked apps" section in the left navigation menu and select the "Link another app" drop down menu.

{{< figure src="/img/play_2_link_new_app.png" width="900" height="400" >}}

Select the "Web" option in the drop down menu.

{{< figure src="/img/play_3_link_new_web_app.png" width="900" height="400" >}}

In the form, enter the following values:

* Name: `Zapic`
* Launch URL: `https://app.zapic.net`
* Turn-based multiplayer: `Off`

Select the "Save and continue" button.

{{< figure src="/img/play_4_complete_form.png" width="900" height="400" >}}

Select the "Authorize your app now" button. This will create and link a Google APIs project with your Google Play Games Services app.

{{< figure src="/img/play_5_authorize.png" width="900" height="400" >}}

Select the "here in the APIs Console" link to navigate to the new Google APIs project.

{{< figure src="/img/play_6_navigate.png" width="900" height="400" >}}

Select the "Zapic" OAuth 2.0 client from the list.

{{< figure src="/img/play_7_navigate.png" width="900" height="400" >}}

Record the "Client ID" and "Client secret" values at the top of the page. These values will be entered into the Zapic Portal later.

In the form, enter the following values (some may already be correct):

* Name: `Zapic`
* Authorized JavaScript origins: `https://app.zapic.net`
* Authorized redirect URIs: `https://app.zapic.net/api/0.1/play-games-services/token-callback`

Select the "Save" button.

{{< figure src="/img/play_8_complete_form.png" width="900" height="500" >}}

In Android Studio, open your app's `resources/values/strings.xml` file, and copy the following elements into the `<resources>` element. Replace the `play_games_app_id` value with the numeric prefix of the "Client ID" value from the Google APIs console. Replace the `play_games_web_client_id` value with the full "Client ID" value from the Google APIs console.

```xml
<resources>
    ...

    <!-- Zapic and Google Play Games -->
    <string name="play_games_app_id">1234567890</string>
    <string name="play_games_web_client_id">1234567890-abcdefg.apps.googleusercontent.com</string>
</resources>
```

Open the [Zapic Portal](https://portal.zapic.net), and navigate to and edit your app.

Copy the "Client ID" and "Client secret" values into the "Play Store App Details" panel:

{{< figure src="/img/play_9_portal.png" width="546" height="338" >}}

Select the "Submit" button.