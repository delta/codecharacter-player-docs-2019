=====
Rules
=====

Game Board/Map
==============

The map is a square 30x30 grid of tiles. The origin is at the top-left corner. The X-axis moves from left to right, and the Y-axis from top to bottom.

Units
=====

There are two types of units - towers and soldiers.

Towers
------

Towers can be built with money. They have high HP but cannot attack. They can be upgraded, and once destroyed are gone forever.

A tower can also control 'territory', which is a number of tiles of the map around it. Each tower has a 'range' that measures their power of control. The 'range' is a number. A tower with range 1 controls the tile on the map it is on, and the 8 adjacent tiles around it. You can also think of this as the 3x3 grid around the tower.

Similarly, a tower with range 2 controls the 5x5 grid around the tower, and so on. Once destroyed, a tower loses control of its territory.

Soldiers
--------

Each player has a fixed number of soldiers that cannot be increased. Soldiers have low HP, and can attack enemy soldiers and towers. Once dead, they respawn after a fixed number of turns that cannot be decreased. Soldiers are invulnerable to all damage for a small number of turns immediately after they respawn.

Starting the Game
=================

Each player begins with a tower, called the Base Tower, in their corner of the map and 20 soldiers at the tower. The Base Tower is invincible, and cannot be attacked. Soldiers, once dead, respawn back here 10 turns after their death.

The API we provide is such that you need not worry about which side of the map you are on - it will always appear as if you are on the top-left corner and the enemy on the bottom right.

Goal
====

The goal is to control the most tiles on the map with your towers at the end of the game.

A Turn
======

Players take turns giving commands to their troops. Each turn consists of the following:

1. Commands to soldiers
2. Building towers
3. Upgrading towers
4. Nuking your own towers (suicide)

All of the above can be performed on the same turn.

Soldier Commands
----------------

You can issue exactly one command to each of your soldiers in a turn (that is, each soldier can do one thing). You can either order your soldier to move to a location on the map, or to attack a tower or soldier. Killing towers and soldiers gives you money.

Building Towers
---------------

You can build towers *only on your own map tiles*. If a tile on the map is controlled by both you and your foe, you *cannot* build there, as you require exclusive ownership of the tile. Building a tower requires a fixed amount of money, and occurs instantly (the tower is visible the very next turn).

Each player can only own 15 towers each. You can build as many towers as you want in a turn, as long as you have the money and your final number of towers does not exceed 15.

Upgrading Towers
----------------

Any of your existing towers can be upgraded for a fixed amount of money. You can upgrade each tower twice. Upgrading a tower results in it being able to control more tiles on the map, increases its maximum HP and sets its current HP to the new max HP. You can upgrade as many of your towers as you like each turn, as long as you have the money and they haven't already been upgraded twice. Similar to building, tower upgrade is instant (visible the next turn).

Tower Suicide
-------------

You can mark as many of your towers for suicide as you please. The suicide is instant (visible the next turn), and you get back roughly a third of the money you spent on building and upgrading it.

Since there is a cap on the number of towers you can build, this can be done to gain an advantage by 'moving' your tower to a more advantageous position.

Scoring
=======

The score is simply the number of tiles you control. If a tile is controlled by both you and your opponent, you both get it added to your score.

Instruction Limit
=================

The number of instructions executed by each player's code per turn is counted while the match is being simulated. This is because there is a limit on the number of instructions that a player can execute per turn.

There are two instruction limits - a turn limit and a game limit. Crossing the turn limit on any turn makes that particular turn invalid. Crossing the game limit (even once) makes the player lose the entire match.

End of the Game
===============

The game ends after a 1000 turns. As has been mentioned, the player with the most tiles in control is the winner. If both players have an equal number of tiles, the match is declared a draw.

The game can also end prematurely due to any one player crossing the game instruction limit.
