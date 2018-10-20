---
title: 'Competitions'
weight: 50
---

## What are Competitions?

Competitions allow players to find new friends by playing head to head with players from around the world! Competitions can be configured to reset daily, weekly, or monthly giving new players the opportunity to reach the top of the leaderboard and encourages experienced players to come back to reclaim their position. Competitions can automatically cycle through a schedule of challenge definitions to present your players with new and exciting gameplay modes each time the competition resets.

When a player joins the competition they are automatically placed in a league with up to 50 other players. The top 100 players will be ranked on the competition's leaderboard, giving the most determined players an a way to compete for the coveted #1 position.

## Competition Schedule

Competitions automatically reset on a schedule that you define in the [Zapic Portal](https://portal.zapic.net). They can be configured to last for a day, a week, or a month. Competitions allow players to submit scores from 12:00 AM (midnight) on the day the competition starts to 11:59 PM on the day that the competition ends. Because your players may be distributed around the globe midnight does not always mean midnight. You will need to select the timezone in which to base the start and end times on. We recommend setting the timezone to be aligned with the location of your most active player base.

## Competition Definition

A Competition Definition represents a unique set of rules that will used to compare players against each other to determine their rank. You may define multiple competitions defintions for your game but only 1 competition will be active at a time, the active competition is determined by your [competition rotation]({{< ref "#competition-rotation" >}}).

Each Competition Definition consists of:

- **Title** - The title should describe what the goal of the competition is. (ex. High Score)

- **Descriptions** - The description should give players additional context around the competition. This may include things like what level they need to play or which character they should be using in order to participate in the competition.

- **Parameter** - Name of the parameter that will used to compute the value for each player. (ex. "score")

- **Function** - Defines how the value should be computed (Minimum, Maximum, Total)

- **Filters** - Collection of parameter filters that must be valid for an event to count towards a user's value. This allows you to scope a competition to a particular set of constraints. (ex. "character" == "princess" or "level" = 5)

Once you have created a competition definition in the [Zapic Portal](https://portal.zapic.net) the competition will automatically begin at midnight.

## Competition Rotation

When one competition has finished, Zapic will automatically start the next competition based on the order of the [competition definitions]({{< ref "#competition-definition" >}}) in the rotation. When the a competition has completed, it is added to the back of the rotation, activating the next competition. You may reconfigure the order or even remove a specific competition prior to the competition starting, but once it has started the competition definition is locked. Competition rotations are a great way to add variety to your game, encouraging players to come back and play each of the different competitions that you have defined.
