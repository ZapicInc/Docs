---
title: Events
weight: 20
---

## What are Events

Events are the fundamental building block for all features within Zapic. Your game will submit events as the player progresses through the game, Zapic will then process these events to update challenges, award acheivements.

An event is simply a collection of parameters & values that you define to meet the specific needs of you game. It is your responsibility as the game developer to define each event to meet the needs of your game.

Here is an example of an event that might be triggered when a player's run ends in Flappy Bird.

```json
{
  "score": 45
}
```

or when a player completes a race in a kart racing game.

```json
{
  "place": 1,
  "time": 258.8,
  "character": "plumber",
  "map": "rainbow rue"
}
```

## Why Events

Traditional gaming systems like GameCenter or Google Play Games Services require you to hardcode in which achievement you want to award to a player in your app, events give you the flexibility to dynamically update features within your game (ie. challenges or achievements) in realtime without publishing updates to the App Store. Added a new challenge or achievement is as simple as updating the [Zapic Portal](https://portal.zapic.net) with new information, Zapic will then start processing new events automatically.

## When Should Events Be Sent

Each game will be different, they should only be sent when a significant action occurs in your game such as the end of a level. Events should NEVER be sent within a game loop, if we notice excessive events your access to Zapic can be revoked.

## What Events Should I Send

Since Zapic allows you to dynamically configure how events are processed, it is ok to send events that are not curretly associated with a specific challenge or achievement. When designing your game, if you think there is a possible use case for an event add it to your code now and decide later how you want to utilize that event. Check out our [examples]({{< ref "platform/examples" >}}) for more info.
