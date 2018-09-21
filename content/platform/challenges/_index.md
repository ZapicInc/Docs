---
title: 'Challenges'
weight: 40
---

## What are Challenges?

Challenges are a great way to keep players engaged by providing them a way to compete with friends. As a developer, it is your job to define the rules for a challenge by creating one or more Challenge Definitions.

## Challenge Definitions

A Challenge Definition represents a unique type of challenge that your players can create. You may have multiple challenge definitions per game, but for best results you should ensure that they offer meaningful and varied gameplay. Check out our [examples]({{< ref "platform/examples" >}}) for more info.

Each Challenge Definition consists of:

- **Title** - The title should describe what the goal of the challenge is. (ex. High Score)

- **Parameter** - Name of the parameter that will used to compute the value for each player. (ex. "score")

- **Function** - Defines how the value should be computed (Minimum, Maximum, Total)

- **Filters** (Coming Soon) - Collection of parameter filters that must be valid for an event to count towards a user's value. This allows you to scope a challenge to a particular set of contraints. (ex. "character" == "princess" or "level" = 5)

Once you have defined a challenge in the [Zapic Portal](https://portal.zapic.net) players will be able to create a challenge and invite their friends to compete in your game.
