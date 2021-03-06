---
id: config-advanced
title: Editing the `config.yml` File
sidebar_label: Config (Advanced)
---

## Server Currency
If your server has a form of currency, you can tell BattleArena the name so it 
can display accurate messages. 
```yaml
    moneyName: Gold
```

## Adding New Classes

Here are some examples of adding classes:
```yaml
classes:
    gladiator:
        displayName: "&4Gladiator" ### Used for signs
        items:
            - diamond_sword: sharp:1 1
            - bow: 1
            - arrow: 32
            - diamond_helmet: 1
            - diamond_chestplate: 1
            - diamond_leggings: 1
            - diamond_boots: 1
            - potion: effects="heal:2" displayName="Potion of Healing" 1 # potion of healing 2
            - potion: effects="regeneration:1:45" displayName="Potion of Regeneration" 1 # potion of regen
            - splash_potion: effects="harm:1" displayName="Splash Potion of Harming" 1 # splash potion of harming 1
        enchants:
            - speed:1:120
            - resistance:1:120
    archer:
        displayName: "&2Archer" ### Used for signs
        items:
            - iron_sword: sharp:1 1
            - bow: flame:2 power:3 punch:2 1
            - arrow: 32
            - leather_helmet: 1
            - iron_chestplate: prot:3 1
            - leather_leggings: 1
            - leather_boots: 1
            - potion: effects="heal:2" displayName="Potion of Healing" 1 # potion of healing 2
            - potion: effects="regeneration:1:45" displayName="Potion of Regeneration" 1 # potion of regen
            - splash_potion: effects="harm:1" displayName="Splash Potion of Harming" 1 # splash potion of harming 1
    monk:
        displayName: "&fMonk" ### Used for signs
        items:
            - leather_helmet: 1
            - leather_chestplate: 1
            - leather_leggings: 1
            - leather_boots: 1
            - potion: effects="heal:2" displayName="Potion of Healing" 1 # potion of healing 2
            - potion: effects="regeneration:1:45" displayName="Potion of Regeneration" 1 # potion of regen
            - splash_potion: effects="harm:1" displayName="Splash Potion of Harming" 1 # splash potion of harming 1
        enchants:
            - strength:2:900 # increase attack power
            - speed:2:900 # increase movement
            - haste:2:900 # increase attack speed
            - resistance:1:900 # reduce damage taken
            - jump:2:900 # jump 2 blocks higher than normal
            - regen:1:60 # regen life
```

## default Match Options (these can be overridden by each match type) 
```yaml
defaultMatchOptions:
    secondsTillMatch: 3 ## Time between onPrestart and onStart
    secondsToLoot: 5 ## Time after winning to run around and collect loot
    matchTime: 120 ## How long do timed matches last, (in seconds)
    matchUpdateInterval: 30 ## For timed matched, how long between sending players match updates

    eventCountdownTime: 180 ## How long before announcing an automated event and its start
    eventCountdownInterval: 60 ## How often will it announce a reminder that its open and you can join

    ### Match Announcements
    ## these only affect the broadcasts, not the messages the fighting players receive
    ## announce : announce this message to the server
    ## hc=<channel> : use herochat with the channel specified
    announcements:
        onPreStart: [announce, hc=pvp ]  ## match going to happen soon, example 'P1[p1Elo] vs P2[p2elo]'
        onVictory: [announce, hc=pvp ] ## match has been won, exmaple 'P1[p1elo] has defeated P2[p2elo]'

### Prerequisites
# prerequisites is what they need to have BEFORE joining, this will also be rechecked when the players teleport in
# if there is money, this is taken from their account when they type the command to join
# Prerequisite Options
# needsArmor
# needsItems: if specified you need an item list below
# money=<amount of money>
# maxElo=<maximum elo to join>
# minElo=<minimum elo to join>

### Match Stages
# onOpen: *only called for events, such as ffa/tourney, that have an open stage.
# onPrestart: happens secondsTillMatch seconds before onStart
# onStart: Start of match
# onVictory : happens when match is won by a player
# onComplete: What happens after the match, happens between the time period (onVictory + timeToLoot)
#             if onComplete contains clearInventory it will not allow a player to take inventory out of the arena
#             (except for prize items, or givenItems from onComplete)

### Match Transition Events
# onSpawn: Happens on teleport or on player Respawn ( if respawn is set within onDeath)
# onDeath: What happens when a player dies
# onJoin: player joining a match
# onEnter: Happens when the player first enters the arena.  right after before they are teleported in.  
# onLeave: Happens when the player leaves the arena(aka if they win(after onComplete), or if they die(and dont respawn) )

### Prizes
# winner: given to the winner after onComplete
# losers: given to the losers after onComplete
# firstPlace: (for tourneys) given to winner after tournament complete
# participants: (for tourneys) given to all participants(except winner) after tournament complete

# valid options for everything but preReqs
# clearInventory,
# giveItems: needs a list under items
# teleportIn
# teleportOut
# pvpon or pvpoff
# health=<health amount>
# hunger=<hunger amount>
# money=<money to give>
# experience=<exp to give>
# teamPvpOn : if not specified defaults to off
# respawn: 
# enchants: needs a list of enchants under enchants
# deEnchant: get rid of all potion effects on player
# disguiseAll=<name>: disguise all players with the given value
# undisguise: undisguise players
# storeExperience/restoreExperience: store/restore Experience 
# storeItems/restoreItems : store/restore items

## Defaults: these events(if not overwritten) get filled with the following values
# onEnter:
#    options: [storeExperience, storeItems(if preReqs contains clearInventory)] 
# onLeave:
#    options: [restoreExperience, restoreItems(if preReqs contains clearInventory)] 

#### Events vs Matches
### Events
## Events can have "open" phases were people are joining but the event hasnt started
## They also can have multiple "matches" that occur as part of the event (like a tournament, where 
## each match is part of the whole 'Tournament Event')
## Some Events like the FreeForAll only have 1 match, but still have the open phase that lasts until someone starts it
### Match
## a single battle between teams
```
## Matches

### Arena
```yaml
arena:
    enabled: true
    type: versus
    tracking:
        dbTableName: arena
    rated: true
    prefix: "&6[Arena]&e"
    onJoin:
        options: [pvpOff]
    preReqs:
        options: [clearInventory]
    onStart:
        options: [teleportIn, pvpOn,blockBreakOff]
    onSpawn:
        options: [deEnchant, giveItems, hunger=20, health=20]
        giveClass:
            default: gladiator
        items: # ignored if options doesnt have "giveItems"
            - bread: 5
    onComplete:
        options: [teleportOut, clearInventory]
    winner:
        options: [health=20, hunger=20]
```

### Skirmish 
```yaml
skirmish:
    enabled: true
    type: versus
    database: arena
    rated: false
    prefix: "&b[Skirmish]&e"
    onStart:
        options: [teleportIn, pvpOn, blockBreakOff]
    onComplete:
        options: [teleportOut]
    winner:
        options: [health=20, hunger=20]
```

### BattleGround
```yaml
battleground:
    enabled: true
    command: bg
    type: battleground
    database: bg
    prefix: "&c[Battleground]&e"
    victoryCondition: highestKills
    matchTime: 60
    minTeams: 2
    minTeamSize: 5
    maxTeamSize: 5
    preReqs:
        options: [clearInventory]
    onJoin:
        options: [pvpOff]
    onPrestart:
        options: [pvpOff, teleportIn, giveItems, deEnchant, disguiseAllAs=ArenaGuy]
        giveClass:
            default: gladiator
            team1: archer
            team2: monk
            team3: gladiator
        items: # ignored if options doesnt have "giveItems"
            - bread: 5
    onStart:
        options: [pvpOn]
    onComplete:
        options: [teleportOut, clearInventory, deEnchant, undisguise]
    onSpawn:
        options: [enchants, health=20, hunger=20, deEnchant, disguiseAllAs=ConfusedGuy,woolTeams]
        enchants:
            - speed:3
    onDeath:
        options: [respawn]
    winner:
        options: [enchants, money=1,experience=300, health=20, hunger=20]
        enchants:
            - speed:1:900
            - resistance:1:900
```
     
### Colosseum
```yaml
Colosseum:
  name: Colosseum
  command: Colosseum
  prefix: '&8[Colosseum]'
  signDisplayName: &8[Colosseum]
  gameSize:
    nTeams: '4'
    teamSize: '1'
  nLives: '2'
  victoryCondition: LASTMANSTANDING
  tracking:
    database: col
    rated: true
    useTrackerMessages: false
  arenaType: Colosseum
  arenaClass: Arena
  onEnter:
    options:
    - STOREALL
  onLeave:
    options:
    - RESTOREALL
  preReqs:
    options:
    - clearInventory
  onJoin:
    options:
    - pvpOff
  onPreStart:
    options:
    - woolTeams
    - teleportIn
    - pvpOff
  onStart:
    options:
    - pvpOn
  onComplete:
    options:
    - teleportOut
    - clearInventory
  onSpawn:
    giveItems:
    - DIAMOND_SWORD DAMAGE_ALL:1 1
    - BOW 1
    - ARROW 32
    - DIAMOND_HELMET 1
    - DIAMOND_CHESTPLATE 1
    - DIAMOND_LEGGINGS 1
    - DIAMOND_BOOTS 1
    enchants:
    - speed:1:60
    options:
    - woolTeams
    - health=20.0
    - hunger=20
    - deEnchant
    - respawnWithClass
  onDeath:
    options:
    - clearInventory
    - respawn
  winners:
    enchants:
    - speed:1:900
    - prot:1:900
    options:
    - health=20.0
    - hunger=20
    - experience=300
    - money=1.0
```

## Events

### FFA Event
```yaml
freeForAll:
    enabled: true
    command: ffa
    type: ffa
    database: ffa
    prefix: "&c[FFA]&e"
    preReqs:
        options: [clearInventory]
    onJoin:
        options: [teleportIn, woolTeams]
    onOpen:
        options: [pvpOff]
    onPrestart:
        options: [pvpOff, giveItems, deEnchant]
        items: # ignored if options doesnt have "giveItems"
            - iron_sword: 1
            - bow: 1
            - tnt: 3
            - arrow: 32
            - leather_helmet: 1
            - leather_chestplate: 1
            - leather_leggings: 1
            - leather_boots: 1
            - bread: 5
    onStart:
        options: [pvpOn]
    onComplete:
        options: [teleportOut, clearInventory, deEnchant, undisguise]
    onSpawn:
        options: [enchants, health=20, hunger=20, deEnchant]
        enchants:
            - speed:3
    winner:
        options: [enchants, money=1,experience=300, health=20, hunger=20]
        enchants:
            - speed:2:900
            - resistance:2:900
```

### Death Match Event
```yaml
deathMatch:
    enabled: true
    command: dm
    type: deathMatch
    victoryCondition: highestKills
    database: dm
    prefix: "&8[DeathMatch]&e"
    preReqs:
        options: [clearInventory]
    onJoin:
        options: [teleportIn, woolTeams]
    onOpen:
        options: [pvpOff]
    onStart:
        options: [pvpOn]
    onComplete:
        options: [teleportOut, clearInventory, deEnchant, undisguise]
    onSpawn:
        options: [enchants, giveItems, health=20, hunger=20, deEnchant]
        items: # ignored if options doesnt have "giveItems"
            - iron_sword: 1
            - bow: 1
            - tnt: 3
            - arrow: 32
            - leather_helmet: 1
            - leather_chestplate: 1
            - leather_leggings: 1
            - leather_boots: 1
            - bread: 5
        enchants:
            - speed:1
    onDeath:
        options: [respawn,clearInventory]
    winner:
        options: [enchants, money=1,experience=300, health=20, hunger=20]
        enchants:
            - speed:2:900
            - resistance:2:900
```
 
## Tournament Event
```yaml
tourney:
    name: Punch Drunk
    type: Versus
    database: tourney
    prefix: "&5[Tourney]&e"
    timeBetweenRounds: 3
    preReqs:
        options: [clearInventory]
    onStart:
        options: [teleportIn, pvpOn, woolTeams]
    onComplete:
        options: [teleportOut, clearInventory]
    onSpawn:
        options: [deEnchant, giveItems, hunger=20, health=20]
        items:
            - iron_sword: 1
            - bow: 1
            - arrow: 16
            - iron_helmet: 1
            - iron_chestplate: 1
            - iron_leggings: 1
            - iron_boots: 1
            - potion: effects="heal:2" displayName="Potion of Healing" 1 # potion of healing 2
            - bread: 3
    winner:
        options: [clearInventory, experience=100, health=20, hunger=20]
    firstPlace:
        options: [enchants,experience=1000]
        enchants:
            - speed:2:900
            - resistance:2:900
            - haste:1:900
```
