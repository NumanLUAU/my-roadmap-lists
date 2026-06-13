# Larp The Facility

## Day 1 - Core Survivor Gameplay

### Crawl System
- [ ] Crawling state
- [ ] Crawl animations
- [ ] Crawl movement speed
- [ ] Server validation

### Computer Hacking System
- [ ] Computer interact prompt
- [ ] Hacking progress
- [ ] Skill check system
- [ ] Failure penalties
- [ ] Computer completion tracking
- [ ] Shared progress replication

### Test Dummies
- [ ] Survivor dummy
- [ ] Beast dummy
- [ ] Dummy spawning utility

### Architecture
- [ ] Character state system
- [ ] Interaction framework
- [ ] Replication framework
- [ ] Object tagging system

---

## Day 2 - Roles & Combat

### Role System
- [ ] Survivor role
- [ ] Beast role
- [ ] Team assignment
- [ ] Spawn logic
- [ ] Dummy role support

### Hammer System
- [ ] Hammer equip
- [ ] Swing animations
- [ ] Swing cooldown
- [ ] Server hit validation

### Hitbox System
- [ ] Dynamic hitboxes
- [ ] Lag compensation
- [ ] Anti exploit validation
- [ ] Damage event pipeline

### Character States
- [ ] Alive
- [ ] Downed
- [ ] Dragged
- [ ] Frozen
- [ ] Escaped

---

## Day 3 - Downing, Dragging & Freezers

### Ragdoll System
- [ ] Beast attacks cause ragdoll
- [ ] Ragdoll replication
- [ ] Recovery prevention

### Dragging System
- [ ] Rope attachment
- [ ] Dragged state
- [ ] Drag movement
- [ ] Release system

### Freezer Detection
- [ ] Highlight nearby freezers
- [ ] Beast freezer prompts
- [ ] Freezer occupancy tracking

### Freezer System
- [ ] Place survivor into freezer
- [ ] Frozen state
- [ ] Freezer timers
- [ ] HP drain while frozen
- [ ] Survivor rescue interaction

### Anti-Camp System
- [ ] Beast distance monitoring
- [ ] Camp detection
- [ ] Reduced freezer decay while camping
- [ ] Camp warning system

---

## Day 4 - Objectives, Abilities & Rounds

### Exit Phase
- [ ] Detect all completed computers
- [ ] Objective switch
- [ ] Exit highlighting
- [ ] Exit interaction

### Ability Framework

#### Core Architecture
- [ ] Ability base class
- [ ] Passive abilities
- [ ] Active abilities
- [ ] Cooldown framework
- [ ] Server-authoritative execution
- [ ] Client prediction layer

#### Cooldown System
- [ ] Server cooldown tracking
- [ ] GUI synchronization
- [ ] Replicated cooldown updates

### Role Selection
- [ ] Survivor role selection
- [ ] Beast role selection
- [ ] Ability selection
- [ ] Loadouts

### Round System
- [ ] Lobby state
- [ ] Intermission
- [ ] Round start
- [ ] Round end
- [ ] Winner determination

### Player Requirements
- [ ] Minimum 2 players
- [ ] Auto start checks

---

## Day 5 - Maps, Balance & Production Architecture

### Dynamic Map System

#### Map Loader
- [ ] Map loading
- [ ] Map unloading
- [ ] Spawn generation
- [ ] Round integration

#### Computer Spawning
- [ ] Spawn point tags
- [ ] Dynamic computer placement

Example:

```lua
local SurvivorComputerMap = {
    ["1"] = 2,
    ["2"] = 3,
    ["3"] = 4,
    ["4"] = 5,
    ["5"] = 6,
    ["6"] = 7,
    ["7"] = 7,
    ["8"] = 7,
}
```

Rules:
- Spawn required computers
- Spawn 2 extra backup computers
- Prevent softlocks from camping

### Beast Scaling
- [ ] 1 Beast if ≤ 5 players
- [ ] 2 Beasts if ≥ 6 players

### Beast Movement
- [ ] Jump slowdown
- [ ] Recovery timer
- [ ] Speed restoration after 0.8s
- [ ] Timer reset on repeated jumps

### Beast Recovery
- [ ] 3 second stun after successful hit
- [ ] Recovery state handling

### Ability Production Pass
- [ ] Create all Survivor abilities
- [ ] Create all Beast abilities
- [ ] No hardcoded ability logic
- [ ] Fully module driven

### Final Polish
- [ ] Testing
- [ ] Bug fixing
- [ ] Replication optimization
- [ ] Exploit prevention
- [ ] Performance profiling

---

# Final Architecture

## Initializer

```text
ReplicatedStorage
└── Shared
    ├── Framework
    ├── States
    ├── Abilities
    ├── Roles
    ├── Maps
    └── Config

ServerScriptService
└── Server
    ├── RoundService
    ├── RoleService
    ├── AbilityService
    ├── CombatService
    ├── DragService
    ├── FreezerService
    ├── ComputerService
    └── MapService

StarterPlayer
└── StarterPlayerScripts
    └── Client
        ├── AbilityController
        ├── UIController
        ├── InteractionController
        └── CameraController
```

## Abilities

```text
Abilities
├── Survivor
│   ├── Runner
│   ├── Medic
│   ├── Hacker
│   └── ...
│
├── Beast
│   ├── SpeedBoost
│   ├── Tracker
│   ├── Slam
│   └── ...
│
└── BaseAbility
```

Each ability module exposes:

```lua
return {
    Name = "Runner",
    Cooldown = 20,
    Passive = false,

    Activate = function(player)
    end,

    Deactivate = function(player)
    end
}
```

## Character State Machine

```text
Alive
 ├─> Crawling
 ├─> Hacking
 ├─> Downed
 │     └─> Dragged
 │             └─> Frozen
 │
 └─> Escaped
```
