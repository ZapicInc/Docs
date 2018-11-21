---
title: 'Promotions'
weight: 85
---

## What Are Promotions

Zapic Promotions are the easiest way for you to fully control the ad content being shown to your players. You can promote anything you want, some examples include:

- Your other apps
- Social Media Accounts
- In App Purchases
- Your Website
- Zapic Challenges or Competitions
- ...

As the developer, you get full control of when the promotion will show up in your game, just like any other Zapic user interface. You can also control which of your promotions are active at any time through the [developer portal](https://portal.zapic.com).

## Promotion Requirements

A promotion simply consists of the creative content to display and a URL that the player will go to when they tap on your promotion.

### Creative Content

All creative content for a promotion must a **jpeg** with either a **480x320** (landscape) or **320x480** (portrait) resolution. In order to prevent the same promotion content being shown over and over, you may upload up to **5** different art assets per promotion. When it is time to show a promotion, Zapic will randomly select one of those assets to display to your player.

{{< img src="images/resolutions.jpg" width="600" title="Allowed Promotions Resolutions" >}}

#### Prohibited Content

Zapic prohibits the promotion of products or services in the following categories:

- Pornography, adult or mature content.
- Malware, phishing or other harmful codes / software.
- Fake virus, "scan alerts" or "technical support".
- Illegal, prescription, or recreational drugs.
- Alcohol or tobacco.
- Offensive, abusive or hate-mongering content.
- Auto-downloading of software / apps.
- Marketing materials that are protected by copyright and trademark laws.

Zapic also reserves the right to reject any content for any reason at our sole discretion.

{{% notice warning %}}
All promotion content is reviewed by Zapic to ensure it meets our community standards. Campaigns are continually reviewed by our staff and an active campaign can be suspended at any time. If, after approval, a campaign was modified in a way that does not follow our Guidelines, your account could be suspended or terminated.
{{% /notice %}}

{{% notice note %}}
If you have any questions regarding prohibited content please [contact us](mailto:contact@zapic.com).
{{% /notice %}}

### Promotion URL

When a user taps on a promotion in your app, Zapic will open the URL associated with the promotion content. Any valid URL is accepted by Zapic, this may be a direct link to your desired website, app store or could be a URL from a link shortener or deep linking service. If you are not using a deep linking service, please ensure that your promotion is targeting the proper type of device for the link supplied.

{{% notice warning %}}
Any content that is linked to must follow the same community standards as promotion content. If, after approval, a campaign was modified in a way that does not follow our Guidelines, your account could be suspended or terminated.
{{% /notice %}}

### Targeting

Zapic promotions can be targeting to specific mobile platforms, ensuring that your users go the proper link for the device they are using. For example if you are promoting another app, you would want to target iOS devices with your iTunes link and Android devices with your Play Store link.

### Showing Promotions

Just like any other Zapic interface that you show, you simply need to call the `Show Page` method with the page named `PROMOTION_INTERSTITIAL`. This will open a full page interstitial with your promotion content.

Unity Example:

```
Zapic.ShowPage(“PROMOTION_INTERSTITIAL”)
```

We recommend showing Zapic promotions just as you would show a traditional interstitial ad. The timing of showing interstitial ads is important so that to not interrupt the user's experience. These full page promotions are best shown during a natural pause in your game such as during a loading screen before the player starts playing or after a player has completed a level.

## Examples

### Cross Promoting Your Other Apps

{{< img src="images/app-promotion.jpg" width="200" title="Example Cross Application Promotion" align="right" >}}

Cross promoting your other games is a great way to encourage your existing players to try our your latest masterpiece. To cross promote another game, simply provide a link to your app store listings so players can quickly and easily find your new app or game.

If you are using a deep linking service such as [Branch](https://branch.io) you may not need to use Zapic's platform targeting since these types of links usually determine the users device and will take them to the appropriate app store (App Store or Play Store) to download your app.

If you are not using these types of services you will need to create two separate promotions, one for each platform. For the iOS promotion, you will need to include the link to your App Store page that targets only iOS devices, for Android, you will include your Google Play link that targets Android devices.

### Promote Your Social Media Accounts

You can also encourage players to follow you on social media to stay up to date with the latest news about you, your games, and the best cat videos around. Simply include the link to your social media account so users can quickly follow you.

{{< img src="images/social-promotion.jpg" width="500" title="Example Social Media Promotion">}}

### Promote In Game Content/App Purchases

{{< img src="images/iap-promotion.jpg" width="200" title="Example In App Purchase Promotion" align="right" >}}

Promotions can also be a great way to tell your players that there are new features, a special event, or a limited time bonus on In App Purchases.

In order to link directly to your in game content, such as an IAP page, you currently need to integrate with a deep linking service such as [Branch](https://branch.io). When a player taps on your Zapic promotion, the deep linking service will alert you to the deep link that was opened on, allowing you to handle the deep link event and which time you would open up your IAP or other in game menu.
