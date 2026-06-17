# Larp The Facility

## Day 1 - Core Survivor Gameplay

### Crawl System
- [x] Crawling state
- [x] Crawl animations
- [x] Crawl movement speed
- [x] Server validation

### Computer Hacking System
- [x] Computer interact prompt
- [x] Hacking progress
- [x] Skill check system
- [x] Failure penalties
- [x] Computer completion tracking
- [x] Shared progress replication

### Test Dummies
- [x] Survivor dummy
- [x] Beast dummy
- [x] Dummy spawning utility

### Architecture
- [x] Character state system
- [x] Interaction framework
- [x] Replication framework
- [x] Object tagging system

---

## Day 2 - Roles & Combat

### Role System
- [x] Survivor role
- [x] Beast role
- [x] Team assignment
- [x] Spawn logic
- [x] Dummy role support

### Hammer System
- [x] Hammer equip
- [x] Swing animations
- [x] Swing cooldown
- [x] Server hit validation

### Hitbox System
- [x] Dynamic hitboxes
- [x] Lag compensation
- [x] Anti exploit validation
- [x] Damage event pipeline

### Character States
- [x] Alive
- [x] Downed
- [x] Dragged
- [x] Frozen
- [x] Escaped

---

## Day 3 - Downing, Dragging & Freezers

### Ragdoll System
- [x] Beast attacks cause ragdoll
- [x] Ragdoll replication
- [x] Recovery prevention

### Dragging System
- [x] Rope attachment
- [x] Dragged state
- [x] Drag movement
- [x] Release system

### Freezer Detection
- [x] Highlight nearby freezers
- [x] Beast freezer prompts
- [x] Freezer occupancy tracking

### Freezer System
- [x] Place survivor into freezer
- [x] Frozen state
- [x] Freezer timers
- [x] HP drain while frozen
- [x] Survivor rescue interaction

### Anti-Camp System
- [x] Beast distance monitoring
- [x] Camp detection
- [x] Reduced freezer decay while camping
- [x] Camp warning system

---

## Day 4 - Objectives, Abilities & Rounds

### Exit Phase
- [x] Detect all completed computers
- [x] Objective switch
- [x] Exit highlighting
- [x] Exit interaction

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
- [x] Lobby state
- [x] Intermission
- [x] Round start
- [x] Round end
- [x] Winner determination

### Player Requirements
- [x] Minimum 2 players
- [x] Auto start checks

---

## Day 5 - Maps, Balance & Production Architecture

### Dynamic Map System

#### Map Loader
- [x] Map loading
- [x] Map unloading
- [x] Spawn generation
- [x] Round integration

#### Computer Spawning
- [x] Spawn point tags
- [x] Dynamic computer placement

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
- [x] 1 Beast if ≤ 5 players
- [x] 2 Beasts if ≥ 6 players

### Beast Movement
- [x] Jump slowdown
- [x] Recovery timer
- [x] Speed restoration after 0.8s
- [x] Timer reset on repeated jumps

### Beast Recovery
- [x] 3 second stun after successful hit
- [x] Recovery state handling

### Ability Production Pass
- [ ] Create all Survivor abilities
- [ ] Create all Beast abilities
- [ ] No hardcoded ability logic
- [ ] Fully module driven

### Final Polish
- [ ] Testing
- [ ] Bug fixing
- [x] Replication optimization
- [ ] Exploit prevention
- [ ] Performance profiling

---

# Final Architecture

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
