---
title: Players
weight: 10
---

## Introduction

Zapic is designed to allow players to connect with friends, discover new games and play together. Having a unified account is critical to giving players a seamless gaming experience on any device.

In order for a user to use Zapic, they are first required to create a Zapic account that can be used in any Zapic enabled game. Zapic will keep track of critical information for each player, such as identity, social connections, and gameplay information such as scores or stats.

Authentication is securely handled by the Zapic UIs & SDKs without any developer involvement. When a user plays your game they will have the option to create a new account or log in with an existing Zapic account. Once a player has successfully logged into a game, that player association is saved in the game until the player explicitly signs out or their login expires and they must login again.

Only one player is allowed to be authenticated in a game at a time; for a new player to be authenticated, the existing authenticated player must first sign out.

## Unique Player Identifier

Every player account is uniquely identified by a `playerId` string contained within a `ZapicPlayer` object. The `playerId` is created when the player first logs in to your game and never changes, even if other information in the account changes. Thus, `playerId` is the only reliable way to track a particular player.

In order to protect a player's personal information and prevent a player from being tracked across multiple games, a unique `playerId` is generated for each game. A player will use a Zapic account across multiple games, but the `playerId` will be unique for each game that the player logs into.

In addition to using `playerId` in your interactions with Zapic, your game should also use the `playerId` whenever it wants to store data locally about a specific player. For example, if your game stores data to track a player’s progress (such as on the device or on your own server), use `playerId` to distinguish between multiple players playing on the same device. That way, if a different player signs into the game, you can immediately personalize the experience by showing content or progress specific to that player.

{{% notice warning %}}
Never make assumptions about the format or length of playerId. Although any individual playerId string is immutable, the format and length of playerId strings are subject to change. You must treat playerId strings as opaque tokens.
{{% /notice %}}
