Synoid Breach Starfall - Game Design Document
1. Game Overview
1.1 Game Title
Synoid Breach Starfall
1.2 Core Premise
Set in the Alpha Centauri system on June 9, 4200 (Sol Calendar), humanity faces an invasion by the Synoids, extradimensional enemies wielding advanced technology. Synoids and their warbots mirror human archetypes (e.g., Soldier, Technician), acting as AI-driven enemies. The player, a lone hero in a single-player tactical RPG, navigates a hexagonal grid-based world, engaging in turn-based combat, scavenging loot, and managing resources to exploit enemy weaknesses (e.g., EMP for warbots). The hook: Synoid enemies are “player-like” with mirrored stats, and scavenging their tech risks destabilizing reality. Story details are TBD.
1.3 Genre
Single-player tactical RPG with turn-based combat and procedural level generation.
1.4 Platform
Developed using Unreal Engine 5.6 with the Gameplay Ability System (GAS).
1.5 Target Audience
Players who enjoy tactical RPGs with deep customization, inspired by Diablo’s loot system and turn-based strategy games.
2. Game Vision
2.1 Gameplay Pillars

Exploration: Navigate a hexagonal grid with a mini-map and fog of war, revealing enemy, item, and event locations.
Tactical Combat: Engage in turn-based battles with strategic action management and enemy weaknesses.
Progression: Customize builds via skill trees, attributes, and randomized gear affixes, with no build restrictions.
Replayability: Procedural levels and persistent progression encourage multiple playthroughs.

2.2 Unique Selling Points

Hexagonal grid-based navigation with guaranteed enemy encounters and strategic mini-map icons.
Diablo-like loot system with random affixes on class-specific and universal gear.
Synoid enemies mirroring player archetypes, creating dynamic, player-like combat.
Deep customization via skill trees and rare action slot affixes on Legendary/Mythic items.

3. Technical Overview
3.1 Engine
Unreal Engine 5.6, utilizing the Gameplay Ability System (GAS) for abilities, status effects, and attribute management.
3.2 UI Framework
Unreal Motion Graphics (UMG) for menu-driven interfaces, including radial menus, inventory tabs, and combat displays.
3.3 Core Systems

Navigation: Radial menu for hex grid movement.
Combat: Turn-based with GAS-driven abilities and effects.
Progression: Attribute-based (max 99) and skill tree system.
Loot: Randomized affixes on gear, inspired by Diablo.
Level Design: Procedural hex grids with pre-assigned content.

4. Gameplay Mechanics
4.1 Core Gameplay Loop
The core loop revolves around exploration, turn-based combat, and progression:

Explore: Navigate a hexagonal grid of rooms via a radial menu (1-6 directions), using a mini-map with fog of war revealing adjacent hexes and their icons (e.g., ?? for enemies, ?? for items).
Combat: Enter combat hexes for guaranteed encounters (100% enemy spawns), resolved via turn-based combat with initiative.
Progress: Defeat enemies for XP, level up, collect gear (class-specific and universal with random affixes), and advance via hexes or puzzles.
Repeat: New procedural hex map each run, with persistent character progression (levels, gear).

4.2 Specific Mechanics

Movement: Menu-driven navigation on a hexagonal grid (20–100 tiles per level, layouts TBD, e.g., City grids, Wilderness paths). Players select a direction (1-6) via radial menu. Empty hexes are inaccessible. Mini-map in top-right corner shows fog of war, revealing current and adjacent hexes with icons (e.g., ?? for enemy, ?? for chest, ?? for shop, ?? for narrative event, ? for puzzle, ?? for hazard).
Combat System:
Turn-Based with Initiative: Combat triggers on entering enemy hexes (100% spawn). Initiative is Agility (AGI)-driven (TBD formula, e.g., AGI * 2 + Equipment Bonus - Status Penalty). Higher initiative acts first.
Actions: Players start with 1 attack action and 2 secondary actions (e.g., defend, move, scan, reload, use item) per turn, regenerating each turn. Secondary actions cost varying sec points (e.g., scan: 1, defend: 2, TBD pool size). Additional slots (attack or secondary) granted by rare Legendary/Mythic items:
Equippable: Grant slots while equipped (e.g., Overclock Module: +1 attack slot).
Consumable: Grant temporary slots (TBD turns, stackable TBD, TBD drop chance).


Status Effects (implemented as GAS Gameplay Effects):
Stun: Skips turn, resistible via roll (TBD, e.g., WIL vs. stun DC). Tag: Effect.Stun.SkipTurn.
Poison: Reduces health (scales with user level, TBD amount/duration, e.g., 5 + Level/2 HP/turn). Tag: Effect.Poison.DamageOverTime.
EMP: Stuns robots (skip 1-2 turns, TBD) and reduces shields (TBD %, e.g., -50% for 3 turns). Tag: Effect.EMP.RobotStun.
Corrosive: Reduces armor/resistances (TBD %, e.g., -20% for 2 turns, stacking TBD). Tag: Effect.Corrosive.ArmorReduction.
Radiation: Random attribute debuff (e.g., -5 STR/INT for 2 turns, TBD). Tag: Effect.Radiation.Debuff.
Psionic: Confusion (enemies attack allies or miss turns, TBD chance/duration). Tag: Effect.Psionic.Confusion.


Damage/Resistance Types: Kinetic, Laser, Plasma, EMP, Corrosive, Radiation, Psionic. Resistances are attribute-driven (TBD mapping, e.g., END for Radiation, WIL for Psionic) with item affix boosts (e.g., +15% Plasma resistance).
Weapons (implemented as GAS abilities or Blueprints):
Single-Target: Pistol, SMG, Rifle, Blade, EMP Spike, Gauss, Throwing (e.g., Pistol: 20 Kinetic damage, 12 ammo).
Multi-Target: Shotgun (2-3 enemies, reduced damage), Cannon (Plasma, applies Plasma Burn), Launcher/Explosive/Pocket Nuke (AoE, hits all enemies, e.g., Rocket: 50 damage), Auto Turret (deploys for multi-turn attacks).
Burst Rifle: Multiple hits on one enemy (e.g., 3 shots, 10 damage each).
Ammo: Unique per weapon class (e.g., Kinetic Ammo for Rifle, Energy Cells for Cannon, Rockets for Launcher). Mag sizes TBD (e.g., Pistol: 12, Launcher: 3). Refilled via chests/shops.
Status effects tied to weapons (e.g., Cannon: 30% chance Plasma Burn, 10 damage/turn for 3 turns).


Abilities: Each class (Soldier, Enforcer, Technician, Psionic, Infiltrator, Specter, Demolitionist, Scourge) has 3 abilities (TBD), unlocked via skill tree with prerequisites. Cost energy (100-point pool, regenerates 10/turn) and have turn-based cooldowns (TBD). GAS tags: e.g., Ability.Soldier.PlasmaSlash, Damage.Plasma.


Inventory: 12-slot grid for weapons, gear, consumables, keys (slots: Weapon, Body, TBD others). Managed via UMG menu tab. Consumables stack (TBD max, e.g., 99).
Progression:
Leveling: XP scales with dungeon depth/enemy level (TBD formula, e.g., XP = Enemy Level * Depth * Multiplier). Level cap 99, grants skill points (TBD amount) for attributes (STR, AGI, DEX, END, INT, WIL, CHA, max 99 each) and skill tree.
Skill Tree: Shared basic unlocks (e.g., +5 AGI, +10% crit chance) and class-specific ability/weapon proficiency unlocks with prerequisites (TBD, e.g., Soldier needs 15 STR for Ability 2).
Gear: Class-specific (e.g., Technician Railgun, Psionic Focus Crystal) and universal (e.g., Nanite Core: +5 END). Diablo-like random affixes:
Tiers: Common (0 affixes), Uncommon (1), Rare (2), Legendary (3), Mythic (4+).
Affixes: Randomly rolled on drop (e.g., +5-15 STR/AGI/INT, +5-20% crit/damage, +10-20% resistance, +1 action slot on Legendary/Mythic only). Any affix can roll on any item with slots.


Narrative Events: Unlock via hexes/puzzles, require leveling/gear to progress (no underlevel guidance).


Win/Lose Conditions:
Win: Defeat final boss on level 10 (TBD objective).
Lose: Death resets map, retains levels/gear.


Balance: Enemy stats scale with level (TBD, e.g., +10% HP/damage). No build limits for player freedom.
GAS Implementation: Uses Gameplay Abilities for attacks/abilities (e.g., Ability.Launcher.AoE), Gameplay Effects for status/affixes (e.g., Effect.Poison, Effect.CritChance +10%), Attribute Sets for stats (e.g., Attribute.AGI, Attribute.Resistance.Plasma). Action slots via Attribute Modifiers (e.g., Modifier.ActionSlot +1).

4.3 Flowchart
[Start] -> [View Mini-Map] -> [Choose Direction/Enter Hex] -> [Enemy Icon?]
    ^                              | [Yes: Combat (1 Attack + 2 Sec)] | [No: Item/Puzzle/Narrative]
[Death: Reset Map] <-------- [Adjacent Hexes Revealed] <--- [Win: XP/Gear] <--- [Event/Boss]

5. Characters, Enemies, and Assets
5.1 Playable Character

Classes: Soldier, Enforcer, Technician, Psionic, Infiltrator, Specter, Demolitionist, Scourge. Chosen at start, each with TBD base stats (e.g., Soldier: high STR/END, Psionic: high INT/WIL).
Attributes: STR, AGI, DEX, END, INT, WIL, CHA (TBD starting values, max 99). Affect resistances (TBD mapping) and initiative (AGI-driven).
Resources: HP (TBD base), Energy (100, regenerates 10/turn).
Abilities: 3 per class, unlocked via skill tree (TBD effects, e.g., Technician: Railgun Overcharge, Psionic: Quantum Pulse). GAS tags: e.g., Ability.Psionic.QuantumPulse.

5.2 Enemies

Races: Synoids (extradimensional, TBD subtypes, e.g., Warbots, Organics). Mirror player classes (Soldier, Enforcer, etc.) with TBD abilities (same or simplified).
Stats: Scale with level (TBD, e.g., +10% HP/damage). Multiple enemies per hex (TBD scaling, e.g., 1-2 early, 3-5 later).
Weaknesses: Warbots vulnerable to EMP (stun, shield reduction), Organics to Poison/Radiation.
Drops: XP (50 per enemy, TBD scaling), gear (10% Common, 3% Rare, 1% Legendary, TBD Mythic), ammo, consumables.
Boss: Final boss (level 10, multi-phase, 1000 HP, 50 damage, TBD drops).

5.3 Assets

Weapons: Pistol, SMG, Rifle, Shotgun, Blade, EMP Spike, Cannon, Launcher, Explosive, Focus Crystal, Gauss, Throwing, Auto Turret, Pocket Nuke. Class-specific (e.g., Demolitionist: Launcher, Technician: Railgun) or universal. Have ammo (TBD mag sizes, e.g., Pistol: 12, Launcher: 3) and status effects (e.g., Cannon: 30% chance Plasma Burn, 10 damage/turn for 3 turns).
Items:
Class-Specific: E.g., Technician Railgun, Psionic Focus Crystal. Random affixes (e.g., +5-15 STR, +10% crit).
Universal: E.g., Nanite Core (+5 END), Scanner (+10% crit). Same affix rules.
Consumables: E.g., Health Potion (50 HP), Energy Cell (30 energy), stackable (TBD max). Some grant temp action slots (TBD duration).
Story Items: Rare, grant extra slots (e.g., Overclock Module: +1 attack while equipped, Legendary/Mythic only, TBD drop chance).


Affixes: Randomly rolled on drop (Diablo-style). E.g., +5-15 STR/AGI/INT, +5-20% crit/damage, +10-20% resistance, +1 action slot (Legendary/Mythic only). Tiers: Common (0), Uncommon (1), Rare (2), Legendary (3), Mythic (4+).

6. World and Level Design
6.1 World Overview

Structure: Procedural hex grid levels (20–100 tiles, TBD layouts, e.g., City grids, Wilderness paths). 10 levels, hex count scales (TBD, e.g., 7-19 hexes).
Mini-Map: Top-right, shows fog of war. Reveals current/adjacent hexes with icons (?? enemy, ?? item, ?? shop, ?? narrative, ? puzzle, ?? hazard).

6.2 Room Types (Hex Contents)

Combat: Enemies (100% spawn), ?? icon (stacked for multiples, e.g., ??x3).
Item: Chests with gear/ammo/consumables, ?? icon.
Puzzle: Sci-fi challenges (TBD, e.g., hack terminals with INT), ? icon.
Shop: Safe zones for upgrades/repairs, ?? icon.
Narrative: Event triggers (e.g., lore tablets), ?? icon (1-2 Mythic items in preset rooms).
Hazard: E.g., Radiation zones (apply ?? debuff), ?? icon.
Void: Inaccessible, no icon.

6.3 Level Progression

Scaling: Enemy count/stats increase (TBD, e.g., level 1: 1-2 enemies, level 10: 3-5). More hazards on higher levels.
Procedural Generation: Hexes from template pool, ensuring 1+ path to exit, 1-3 branches for secrets. Contents pre-assigned (e.g., 40% combat, 20% item).
Narrative: Unlocks via hexes/puzzles, requires leveling/gear (no underlevel guidance).

6.4 Mockup
Hex Grid (Mini-Map, Fog of War):
   / \   / \
  | ? | | ?? |
   \ /   \ /
  / \   / \   / \
 | ?? | |Current| | ?? |
  \ /   \ /   \ /
   / \   / \
  | ?? | | ??x2 |
   \ /   \ /

6.5 UI Layout

Main Screen (2/3): Exploration (hex description, e.g., “Corroded Lab: Toxic fumes”), Combat (action menus, enemy visuals).
Right Side: Mini-map (top), combat log (bottom, e.g., “Player poisons Synoid, 10 HP lost”).
UMG Tabs: Inventory, Skills, Attributes, Journal (TBD buttons vs. radial). Pause combat TBD.
Combat UI: Player (left), enemies (right), status icons (top, e.g., ?? EMP, ?? Radiation). Affixes in tooltips (e.g., “+5 STR, +10% crit”).
