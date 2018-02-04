=========
Constants
=========

Useful Constants
================

You'll probably be using these constants frequently while writing code.

.. cpp:var:: long MAP_SIZE = 30

	Side length of map.

.. cpp:var:: long MAP_ELEMENT_SIZE = 50

	Side length of each tile on the map.

Not So Useful Constants
=======================

These values are be good to know, but aren't as important while writing code.

Money Stuff
-----------

.. cpp:var:: long MONEY_START = 300

	Amount of money each player has at the start of the game.

.. cpp:var:: long MONEY_MAX = INT64_MAX

	Maximum amount of money each player can have.

.. cpp:var:: vector<long> TOWER_KILL_REWARD_AMOUNTS = {300, 500, 700}

	Rewards for killing towers. Indexed by tower level - 1.

.. cpp:var:: long SOLDIER_KILL_REWARD_AMOUNT = 200

	Reward for killing one soldier.

.. cpp:var:: vector<long> TOWER_SUICIDE_REWARD_AMOUNT = {150, 250, 400}

	Rewards for tower sepukku. Indexed by tower level - 1.

Soldier Stuff
-------------

.. cpp:var:: long NUM_SOLDIERS = 20

	Number of soldiers per player.

.. cpp:var:: long SOLDIER_MAX_HP = 100

	Maximum HP for a soldier.

.. cpp:var:: long SOLDIER_SPEED = 50

	Units of distance the soldier covers per turn.

.. cpp:var:: long SOLDIER_ATTACK_RANGE = 60

	Distance from which a soldier can attack.

.. cpp:var::long SOLDIER_ATTACK_DAMAGE = 50

	Damage dealt by a soldier's attack per turn.

.. cpp:var:: long SOLDIER_TOTAL_TURNS_TO_RESPAWN = 10

	Number of turns a soldier takes to respawn.

Tower Stuff
-----------

.. cpp:var:: vector<long> TOWER_HPS = {7000, 10000, 15000}

	Maximum HP of towers. Indexed by tower level - 1.

.. cpp:var:: vector<long> TOWER_BUILD_COSTS = {500, 300, 300}

	Amount of money building and upgrading a tower costs.

	0th element is build cost, 1st and 2nd elements are for 1st and 2nd upgrades respectively.

.. cpp:var:: vector<long> TOWER_RANGES = {2, 3, 4}

	Amount of territory a tower controls. Indexed by tower level - 1.

	A tower range of 2 means that from the center of the tower, a tower controls 2 squares in
	each direction in a square shape, so it would control 2+1+2 times 2+1+2 = 25 squares.

.. cpp:var:: long MAX_TOWER_LEVEL = 3

	The highest possible level a tower can attain.

.. cpp:var:: long MAX_NUM_TOWERS = 15

	Maximum number of towers per player allowed.
