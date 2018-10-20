---
title: 'Showing UI'
weight: 80
---

## Overview

Zapic provides all the user interfaces you need, allowing you to focus on building your game instead of building menus. Whenever you want to show a Zapic UI you simply need to call `Zapic.ShowPage({pagename})`, we take care of the rest.

When you add the "Z" button to your main menu, you will need to show the Zapic home page by calling `Zapic.ShowDefaultPage()`. This will take the player to a landing page with access to all of the different features within Zapic.

## What Zapic Pages Can Be Shown?

- **Challenges** - Opens up the player's list of challenges.

- **Competitions** - Opens up the competition for your game, allowing a player to join or view their rank if they have already joined.

- **CreateChallenge** - Opens the wizard for a player to start creating a challenge.

- **Profile** - Opens the player's profile page, allowing them to update their display name or profile photo.

- **Stats** - Opens the player's stats page, showing all stats and ranks for the player in your game.

- **Login** - If the player has not yet logged into Zapic, this will open up to a login/registration page, when the player completes the login process the Zapic UI will automatically close taking the player back to your game. This is a great way to encourage players to sign in before they can access a specific feature or game mode such as head to head multiplayer.

- **Current** - This will open Zapic to the last page that the user was on before going back to your game.
