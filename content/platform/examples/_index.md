---
title: Examples
---

Here are some example [events]({{< ref "platform/events" >}}) and [challenges]({{< ref "platform/challenges" >}}) that should help you determine what to do in your game. These are intended to be representative only.

## Flappy Bird

Here is the simplist of our examples since there is really only one thing to do. Get as far as possible without crashing.

### Parameter Definitions

```json
key: "score"
type: "numeric"
```

### Event

This simple event only includes 1 parameter, the player's score. This event should be sent each time a player crashes and the Game Over menu is shown to the player. In this example the player got a score of `15`.

(Check with you platform specific docs for the syntax to submit an event)

```json
{
  "score": 15
}
```

### Challenge Definition

This challenge will allow players to compete for the best score in Flappy Bird.

```json
"title":"Best Score",
"parameter":"score",
"function":"maximum"
```

## Kart Racing

Here is an example of everyones favorite Kart Racing game with plumbers, mushrooms, & turtles. In this type of game there are multiple parameters that will be sent at the end of each race as a single event.

### Parameter Definitions

_Time_ - The total time it took for the player to complete the race, in seconds.

```json
key: "time"
type: "numeric"
```

_Place_ - The position that the player finished the race in (1st, 2nd,...).

```json
key: "place"
type: "numeric"
```

_Character_ - The name of the character that was used for the race.

```json
key: "character"
type: "string"
```

_Powerups_ - The number of powerups collected in the race.

```json
key: "powerups"
type: "numeric"
```

### Event

Here is an example of the event that would be sumbitted at the end of a race.

```json
{
  "time": 157.2,
  "place": 2,
  "character": "princess",
  "powerups": 5
}
```

### Challenge Definitions

Because the events have more than one parameter it is possible to create multiple challenge definitions for our Kart game. This allows player to choose which type of challenge they want to create.

This challenge allows players to see who can get fastest time.

```json
"title":"Best Time",
"parameter":"time",
"function":"minimum"
```

This challenge allows players to see who can collect the most powerups in a single race.

```json
"title":"Most Powerups",
"parameter":"powerups",
"function":"maximum"
```

## First Person Shooter

In this example we will look at a traditional FPS game.

### Parameter Definitions

_Kills_ - The total number of kills by the player in the match.

```json
key: "kills"
type: "numeric"
```

_Kill Streak_ - The longest kill streak by the player in the match.

```json
key: "killstreak"
type: "numeric"
```

_Headshot Kills_ - The total number of headshot kills by the player in the match.

```json
key: "headshots"
type: "numeric"
```

_Flags_ - The number of times the player scored a point in a Capture the Flag match.

```json
key: "flags"
type: "numeric"
```

### Event

Here is an example of the event that would be sumbitted when a match has completed.

```json
{
  "kills": 11,
  "killstreak": 2,
  "headshots": 3,
  "flags": 0
}
```

### Challenge Definitions

In this case it is possible to create a challenge definition for each parameter creating 4 different challenge definitions. You can create multiple challenge definitions that use the same parameter as long as the `function` is different between the definitions.

This challenge allows players to see who can gets the most number of kills in a single match.

```json
"title":"Most Kills In A Match",
"parameter":"kills",
"function":"maximum"
```

You can also use the `total` function to compute a score across multiple events. In this case we will compute the total number of headshots for the entire duration of the challenge. These types are challenge can be very powerful since they encourage your players to play many times instead of just trying to get the best single score possible.

```json
"title":"Total Headshots",
"parameter":"headshots",
"function":"total"
```

## Need Another Example

If you think we are missing a specific example, reach out to us or feel free to submit a PR to these docs!
