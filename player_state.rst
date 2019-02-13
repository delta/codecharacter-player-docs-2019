============
Player State
============

This page documents almost everything you'll need to write code.

It contains every data structure we use to describe the state of the game.

*Note:* You can think of two ways to describe position in this game - by counting the tiles in X and Y directions (0-based counting of course, we're civilized people here), and by the actual coordinates (tiles have a size). Whenever we refer to position, we always mean the actual coordinates, not the tile count, unless explicitly otherwise mentioned. **Remember, the X-axis is from left to right, and Y-axis is from top to bottom of the map**.

**Old Stuff**

MapElement
================

.. cpp:class:: MapElement

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



Soldier
=============

.. cpp:class:: Soldier

	Represents a soldier

	.. cpp:member:: long id

		The soldier's ID

	.. cpp:member:: physics::Vector position

		The soldier's position

	.. cpp:member:: long hp

		The soldier's current HP

	.. cpp:member:: bool is_immune

		True if this soldier is currently invulnerable to damage (having respawned recently), false otherwise

	.. cpp:member:: SoldierState state

		An enum describing the state of the soldier. Can be ``SoldierState::IDLE``, ``SoldierState::MOVE``, ``SoldierState::ATTACK``, ``SoldierState::PURSUIT`` or ``SoldierState::DEAD``.

	*Below members are writable, only one may be set per turn per soldier*

	.. cpp:member:: long tower_target

		If you want to attack a tower, set this to the tower's ID.
		Soldier automatically starts moving towards the tower and will attack once it reaches.

	.. cpp:member:: long soldier_target

		If you want to attack a soldier, set this to the soldier's ID.
		Soldier automatically starts moving towards the enemy soldier and will attack once it reaches.

	.. cpp:member:: phyics::Vector destination

		If you want to move to a location, set this to the location's coordinates.

Tower
===========

.. cpp:class:: Tower

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

State
===========

.. cpp:class:: State

	Represents the entire state of the game. You are given this every turn.

	.. cpp:member:: array<array<MapElement, MAP_SIZE>, MAP_SIZE> map

		A 2D array of the tiles in the map. ``map[i][j]`` gives you the :cpp:class:`MapElement` that is the i\ :sup:`th` tile along the X-axis (counting starts from 0) and the j\ :sup:`th` tile along the Y-axis (counting starts from 0).

	.. cpp:member:: array<Soldier, NUM_SOLDIERS> soldiers

		An array of your soldiers

	.. cpp:member:: array<Soldier, NUM_SOLDIERS> enemy_soldiers

		An array of the enemy's soldiers

	.. cpp:member:: array<Tower, MAX_NUM_TOWERS> towers

		An array of your towers. *Caution:* Not all of these entries are valid, use :cpp:member:`num_towers` to check how many towers you actually have. Only elements from ``towers[0]`` to ``towers[num_towers-1]`` contain valid towers.

	.. cpp:member:: array<Tower, MAX_NUM_TOWERS> enemy_towers

		An array of the enemy's towers. *Caution:* Not all of these entries are valid, use :cpp:member:`num_enemy_towers` to check how many towers the enemy actually has. Only elements from ``enemy_towers[0]`` to ``enemy_towers[num_enemy_towers-1]`` contain valid enemy towers.

	.. cpp:member:: long num_towers

		Count of your towers

	.. cpp:member:: long num_enemy_towers

		Count of the enemy's towers

	.. cpp:member:: long money

		Amount of money you have
