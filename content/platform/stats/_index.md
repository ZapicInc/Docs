---
title: Stats and Ranks
weight: 30
---

## What are Stats and Ranks?

Stats are a great way to keep players engaged by providing a method to compare with friends using metrics collected from your game. As a developer, it is your job to define the tracked metrics by creating one or more Stat Definitions. Ranks build on Stats to keep players engaged by providing a method to compare with all players of your game through the use of leagues. As a developer, it is your job to enable the leagues by creating one or more Rank Definitions.

{{< figure src="/img/client_stats_ranks.png" width="450" height="400" >}}

## Stat Definitions

A Stat Definition represents a tracked metric. You may have up to ten Stat Definitions per game.

Each Stat Definition consists of:

- **Title** - The title describe the metric and is presented to your players in the Zapic UI. An example would include "High Score".

- **Parameter** - The name of the event parameter that is used as the value when computing the players' metric. An example would include "SCORE".

- **Function** - The name of the method that is used on the value when computing the players' metric. This may be "Maximum", "Minimum", or "Total".

- **Filters** (Coming Soon) - An optional collection of event parameter values that must be valid for an event to count towards the players' metric. This enables metrics to be scoped to a particular set of contraints. An example would include "CHARACTER equals PRINCESS".

Once you have defined a Stat Definition in the [Zapic Portal](https://portal.zapic.net), players will be able to view their metrics in your game.

{{< figure src="/img/portal_stats.png" width="600" height="350" >}}

## Rank Definitions

A Rank Definition represents a division of players into leagues. You may have up to two Rank Definitions per game.

Each Rank Definition is directly associated with a Stat Definition.

Once you have defined a Rank Definition in the [Zapic Portal](https://portal.zapic.net), players will be able to view their league assignment in your game.

{{< figure src="/img/portal_ranks.png" width="600" height="350" >}}
