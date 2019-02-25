=====
Rules
=====

**TODO:**

Game Board/Map
==============

The map is a square 30x30 grid of tiles. The origin is at the top-left corner. The X-axis moves from left to right, and the Y-axis from top to bottom.

The map has different types of terrain - Land, Water and GoldMines. Water is inaccessible to all units.

Units
=====

There are three types of units - villagers, soldiers and factories.

Villagers
---------

Villagers can move, mine the goldmines and build factories. They have low HP and low speed. They can attack the opponent's units but cause lesser damage than soldiers do. At any point of the game, a player can have a maximum of 30 villagers.

Soldiers
--------

Soldiers can move and attack the opponent's units. They have higher HP and speed compared to villagers and can cause more damage to the opponent. At any point of the game, a player can have a maximum of 30 soldiers.

Factories
---------

Factories can be built with Gold by Villagers on Land. They produce villagers or soldiers and have a high HP but cannot attack or move. A factory can switch between producing villagers or soldiers. A player can have upto 20 factories at any point in the game.

Starting the Game
=================

Each player begins with a set of villagers in their corner of the map and some initial amount of gold. Villagers can move, create factories and mine gold. Factories produce both villagers and soldiers and are stationary. Villagers and soldiers can move and attack other units of the opponent.

The API we provide is such that you need not worry about which side of the map you are on - it will always appear as if you are on the top-left corner and the enemy on the bottom right.

Goal
====

The goal is to eliminate your opponent by destroying all their units.

A Turn
======

Players take turns giving commands to their troops. Each turn consists of the following:

1. Commands to soldiers
2. Commands to villagers
3. Commands for factories

All of the above can be performed on the same turn.

Soldier Commands
----------------

You can issue exactly one command to each of your soldiers in a turn (that is, each soldier can do one thing). You can either order your soldier to

1. Move to a location on the map
2. Attack a villager, soldier or factory

Villager Commands
-----------------

You can issue exactly one command to each of your villagers in a turn. A villager can be ordered to do one of the following - 

1. Move to a location on the map
2. Mine a goldmine to collect gold
3. Build a factory at a location on the map
4. Attack a villager, soldier or factory

Killing the opponents units gives you gold and points.

Factory Commands
----------------

A factory can be commanded to -

1. Start or stop producing units
2. Produce a different unit, villager or soldier

Scoring
=======

A player is rewarded for the following 

1. Killing an opponent's units (soldiers, villagers or factories)
2. Building a factory to completion
3. The amount of gold they have

Instruction Limit
=================

The number of instructions executed by each player's code per turn is counted while the match is being simulated. This is because there is a limit on the number of instructions that a player can execute per turn.

There are two instruction limits - a turn limit and a game limit. Crossing the turn limit on any turn makes that particular turn invalid. Crossing the game limit (even once) makes the player lose the entire match.

End of the Game
===============

The game ends when one player destroys all of their opponents units. If neither player is able to do so, the game ends after a 1000 turns. In this case, the player with the highest score wins. If both players have an equal score at the end of 1000 turns, the match is declared a draw.

The game can also end prematurely due to any one player crossing the game instruction limit.
