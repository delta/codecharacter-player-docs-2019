============
Player State
============

This page documents almost everything you'll need to write code.

It contains every data structure we use to describe the state of the game.

*Note:* You can think of two ways to describe position in this game - by counting the tiles in X and Y directions (0-based counting of course, we're civilized people here), and by the actual coordinates (tiles have a size). Whenever we refer to position, we always mean the actual coordinates, not the tile count, unless explicitly otherwise mentioned.

PlayerMapElement
================

.. cpp:class:: PlayerMapElement

	Represents a tile on the map

	.. cpp:member:: bool territory

		True if you own this tile, false otherwise

	.. cpp:member:: bool enemy_territory

		True if your enemy owns this tile, false otherwise

	.. cpp:member:: bool valid_territory

		True if you can build a tower on this tile, false otherwise

	*Below member is writable*

	.. cpp:member:: bool build_tower

		Set this to true if you want to build a tower at this tile. The tower will be built at the tile's center



PlayerSoldier
=============

.. cpp:class:: PlayerSoldier

	Represents a soldier

	.. cpp:member:: long id

		The soldier's ID

	.. cpp:member:: physics::Vector position

		The soldier's position

	.. cpp:member:: long hp

		The soldier's current HP

	*Below members are writable, only one may be set per turn per soldier*

	.. cpp:member:: long tower_target

		If you want to attack a tower, set this to the tower's ID.
		Soldier automatically starts moving towards the tower and will attack once it reaches.

	.. cpp:member:: long soldier_target

		If you want to attack a soldier, set this to the soldier's ID.
		Soldier automatically starts moving towards the enemy soldier and will attack once it reaches.

	.. cpp:member:: phyics::Vector destination

		If you want to move to a location, set this to the location's coordinates.

PlayerTower
===========

.. cpp:class:: PlayerTower

	Represents a tower

	.. cpp:member:: long id

		The tower's ID

	.. cpp:member:: physics::Vector position

		The tower's position

	.. cpp:member:: long hp

		The tower's current HP

	.. cpp:member:: long level

		The tower's current level. Can be 1 (not upgraded), 2 (upgraded once) or 3 (upgraded twice, maximum level).

	*Below members are writable, only one may be set per turn per tower*

	.. cpp:member:: bool upgrade_tower

		If you want to upgrade this tower by one level, set this to true

	.. cpp:member:: bool suicide

		If you want to nuke (suicide) this tower, set this to true

PlayerState
===========

.. cpp:class:: PlayerState

	Represents the entire state of the game. You are given this every turn.

	.. cpp:member:: array<array<PlayerMapElement, MAP_SIZE>, MAP_SIZE> map

		A 2D array of the tiles in the map

	.. cpp:member:: array<PlayerSoldier, NUM_SOLDIERS> soldiers

		An array of your soldiers

	.. cpp:member:: array<PlayerSoldier, NUM_SOLDIERS> opponent_soldiers

		An array of the enemy's soldiers

	.. cpp:member:: array<PlayerTower, MAX_NUM_TOWERS> towers

		An array of your towers. *Caution:* Not all of these entries are valid, use :cpp:member:`num_towers` to check how many towers you actually have.

	.. cpp:member:: array<PlayerTower, MAX_NUM_TOWERS> opponent_towers

		An array of the enemy's towers. *Caution:* Not all of these entries are valid, use :cpp:member:`num_opponent_towers` to check how many towers you actually have.

	.. cpp:member:: long num_towers

		Count of your towers

	.. cpp:member:: long num_opponent_towers

		Count of the enemy's towers

	.. cpp:member:: long money

		Amount of money you have
