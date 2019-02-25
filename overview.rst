========
Overview
========

Hello, and welcome to the player documentation for Code Character!

Code Character is a programming strategy game where you control troops in a turn-based game with code you write - in our favorite language C++ :)

Let's get started with a quick tutorial on how to get started. If you'd rather start with the rules and documentation, you can start `here <rules.html>`_ instead.

Quick Start
===========

Dashboard Interface
-------------------

Once you log in, you'll see your dashboard, as shown in the image below

**TODO: Insert image here**

**On the left is the editor**, where you can type your code. You'll notice on logging in, that you're provided some default code. It doesn't do much in terms of strategy, but it uses most of the important elements of the code API, so a quick read through it will help.

**On the bottom right is the debug window**. It shows your compilation errors at compile time and your debug logs and errors at runtime.

**On the top right is the renderer window**, which actually displays your game. Use the Arrow Keys to pan and the '+' and '-' keys to zoom in and out of the window. Use 'F' to toggle fullscreen mode. The reset button will restart the game view.

We'll begin with a quick run through of the concepts.

Quick Game Rules
----------------

Code Character is a game of strategic .. . The objective of the game is to expand your empire and eliminate your opponent.

Your empire consists of villagers, soldiers and factories. Factories are stationary units that produce soldiers and villagers which are capable of moving and attacking other units. Ofcourse, soldiers are more powerful than villagers.

In addition, villagers can mine gold from the goldmines and build factories. Factories can toggle between producing villagers and soldiers.

The map has three types of terrain - Land, Water and Goldmines. Water is inaccessible to all units. 

**TODO: Insert image of map**

You are given a fixed number of instructions you can execute every turn. Exceeding the limit on a turn makes you skip the turn. Exceeding the limit by an excessive amount makes you lose the entire match, so ensure that you keep your code as short and efficient as possible!

This is probably enough for you to get a start, but you might want to take the time to read the complete rules in the rules section.

Quick Code Guide
----------------

The way you interact with the game is through your code for the ``Update`` function, which is called every turn of the game. Here, you can issue commands to your soldiers, and build, upgrade, or destroy your towers.

All the data about the current state of the game is stored in a variable called ``state``. This is variable is simply a struct, and so you can read any of its members. The ``state`` is also how you'll represent the output of your code, which will be in the form of command variables that you set each turn.

Let's look at a few examples - ::

	// Getting the id of the first soldier.
	// Notice that you can use the auto keyword in place of a concrete type.
	auto soldier_id = state.soldiers[0].id;

	// Checking if the last tile of the map is valid to build a factory on
	// Notice how constants like MAP_SIZE exist for your ease
	if (state.map[MAP_SIZE - 1][MAP_SIZE - 1] == TerrainType::LAND) ...

	// Issuing a command to your first soldier to attack the first enemy soldier.
	state.soldiers[0].attack( state.enemy_soldiers[0] );

	// Issuing a command to send a villager to mine in the first goldmine
	// Notice the usage of Vec2D, a utility class we have defined.
	Vec2D gold_mine_offset = state.gold_mine_offsets[0];
	state.villagers[0].mine( gold_mine_offset );

	// Issuing a command to set the production state of a factory
	state.factories[0].toggle_production();

	// Issuing a command to all villagers to build factory at (2, 10).
	// We specify what we want the factory to produce using the second parameter.
	// Notice that range-based for loops can be used.
	// Remember to add the reference while iterating, otherwise you'll
	// be modifying a copy of the villager!
	for (auto &villager : state.villagers)
		villager.build( Vec2D(2,10), FactoryProduction::SOLDIER );

	// Return the state you've issued commands to at the END of your code.
	return state;

For more information about ``state``, check the `player state <player_state.html>`_ page.

Quick Competition Guide
-----------------------

Ultimately, Code Character is a game of competition! The objective is to challenge other players and fight your way to the top of the leaderboard. To help you along this process, we offer pre-programmed AIs, against which you can test your code. Additionally, you can also try testing your code against itself!

This is done through the opponent selection interface in **Run Code**

**TODO - Insert images after each para/line **

.. figure:: images/runcode.jpg
  :width: 500px
  :alt: Dashboard

  Buttons to **Run code** for testing, and **Submit Code** for competition

Once you're satisfied with your code and want to compete on the leaderboard, hit **Submit Code**. This will freeze the current version of your code and let you challenge anyone who has also submitted code to the leaderboard. To challenge another player, simply click the challenge button next to their nickname on the leaderboard.

Note that once you submit code, anyone can challenge you at anytime, and a match will automatically be simulated between you and the opposing player. You will receive a notification once the match ends, and you can view it in the **Matches** tab.

After submitting code, you can continue editing it. Only the submitted version of your code will be used for challenges. You can update your submitted code simply by submitting again.

The leaderboard evaluates your position using your rating, which is based purely on the outcomes of your matches with other players. The stronger your opponent, the better your reward. The Elo ranking mechanism is used to calculate ranks.
