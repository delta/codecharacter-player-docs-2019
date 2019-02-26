=========
Constants
=========

These are the magic constants that affect the game logic. You are free to access any of these constants from your code - they are in global scope.

Useful Constants
================

You'll probably be using these constants frequently while writing code.

.. cpp:var:: long MAP_SIZE = 30

	Number of tiles along the side of the map.

.. cpp:var:: long ELEMENT_SIZE = 10

	Side length of each tile on the map.



Some Other Constants
=======================

These values are be good to know, but aren't as important while writing code.

Gold Stuff
-----------

.. cpp:var:: long GOLD_START = 300

	Amount of gold each player has at the start of the game.

.. cpp:var:: long GOLD_MAX = INT64_MAX

	Maximum amount of gold each player can have.

.. cpp:var:: long SOLDIER_COST = 200

	Amount of gold to create one soldier

.. cpp:var:: long VILLAGER_COST = 200

	Amount of gold to create one villager

.. cpp:var:: long FACTORY_COST = 200

	Amount of gold to create one factory

.. cpp:var:: long FACTORY_KILL_REWARD_AMOUNTS = 600

	Rewards for killing one factory.

.. cpp:var:: long SOLDIER_KILL_REWARD_AMOUNT = 200

	Reward for killing one soldier.

.. cpp:var:: long VILLAGER_KILL_REWARD_AMOUNT = 100

	Reward for killing one villager.

.. cpp:var:: long FACTORY_SUICIDE_PENALTY = 200

	Rewards for FACTORY sepukku.

.. cpp:var:: long MINING_REWARD = 10

	Amount of gold increase per villager mining

Soldier Stuff
-------------

.. cpp:var:: long MAX_NUM_SOLDIERS = 30

	Maximum number of soldiers per player.

.. cpp:var:: long SOLDIER_MAX_HP = 200

	Maximum HP for a soldier.

.. cpp:var:: long SOLDIER_SPEED = 5

	Units of distance the soldier covers per turn.

.. cpp:var:: long SOLDIER_ATTACK_RANGE = 5

	Distance from which a soldier can attack.

.. cpp:var:: long SOLDIER_ATTACK_DAMAGE = 10

	Damage dealt by a soldier's attack per turn.

Villager Stuff
--------------

.. cpp:var:: long NUM_VILLAGERS_START = 10

	Number of villagers each player starts with.

.. cpp:var:: long MAX_NUM_VILLAGERS = 30

	Maximum number of villagers per player.

.. cpp:var:: long VILLAGER_MAX_HP = 80

	Maximum HP for a villager.

.. cpp:var:: long VILLAGER_SPEED = 5

	Units of distance the villager covers per turn.

.. cpp:var:: long VILLAGER_ATTACK_RANGE = 5

	Distance from which a villager can attack.

.. cpp:var:: long VILLAGER_ATTACK_DAMAGE = 5

	Damage dealt by a villager's attack per turn.

.. cpp:var:: long VILLAGER_BUILD_EFFORT = 3

	Contribution of villager to building per turn.

.. cpp:var:: long VILLAGER_BUILD_RANGE = 5

	Distance from which a villager can build.

.. cpp:var:: long VILLAGER_MINE_RANGE = 5

	Distance from which a villager can mine.

Factory Stuff
-------------

.. cpp:var:: long MAX_NUM_FACTORIES = 20

	Maximum number of factories per player.

.. cpp:var:: long FACTORY_BASE_HP = 1

	HP of an unbuilt factory.

.. cpp:var:: long FACTORY_MAX_HP = 3000

	Maximum HP for a factory.

.. cpp:var:: long FACTORY_CONSTRUCTION_TOTAL = 300

	Total construction effort needed per factory

.. cpp:var:: long FACTORY_VILLAGER_FREQUENCY = 10

	Frequency with which a factory produces villagers.

.. cpp:var:: long FACTORY_SOLDIER_FREQUENCY = 10

	Frequency with which a factory produces soldiers.
