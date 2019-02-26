============
Player State
============

This page documents almost everything you'll need to write code.

It contains every data structure we use to describe the state of the game.

If you haven't already, you might want to go through the game `overview <overview.html>`_ first, to understand the core game and the various elements that you can control. Once you've got a hang of the game, this page will help you dive deeper into your code.

You might want to checkout `Vector <vector.html>`_ as well.

State
=====

.. cpp:class:: State

	This class represents the state of the game. You are given an instance of this class every round in a parameter called `state`, and you use it to tell the runtime what move you want your units to perform. You have access to view your own units, your opponent units, and the game map.


	.. cpp:member:: array<array<TerrainType, MAP_SIZE>, MAP_SIZE> map

		The map is a 2D array of `TerrainType` elements, which tell you if a particular type is **LAND**, **WATER**, or a **GOLD_MINE**. Remember, your units are not Jesus, and can't walk on Water.

		If you're unfamiliar with `std::array` in C++, simply use map like a standard 2D array in C.

		For example, to check if `(4, 5)` is not water, you could do ::

			if (state.map[4][5] != TerrainType::WATER) {
				...
			}

		You can still go through the entire map using a normal or range based for-loop ::

			for (auto &row : state.map) {
				for (auto &elem : row) {
					// Do something with elem
				}
			}

	.. cpp:member:: vector<Villager> villagers

		A vector of your own villagers. Check down below for more information about the `Villager` object.

	.. cpp:member:: vector<Villager> enemy_villagers

		A vector of the opponent's villagers. Remember, you shouldn't modify this data, and you can't perform moves on an opponent unit.

	.. cpp:member:: vector<Soldier> soldiers

		A vector of your own soldiers. Check down below for more information about the `Soldier` object.

	.. cpp:member:: vector<Soldier> enemy_soldiers

		A vector of the opponent's soldiers. Remember, you shouldn't modify this data, and you can't perform moves on an opponent unit.

	.. cpp:member:: vector<Factory> factories

		A vector of your own factories. Check down below for more information about the `Factory` object.

	.. cpp:member:: vector<Factory> enemy_factories

		A vector of the opponent's factories. Remember, you shouldn't modify this data, and you can't perform moves on an opponent unit.

	.. cpp:member:: vector<Vec2D> gold_mine_offsets

		A vector containing the offsets for the gold mines on the map. You can iterate through the map and check for `TerrainType::GOLD_MINE`, or you can use this vector instead.

		For example, to make the first two villagers each mine at the first two locations on the map, you would do ::

			state.villagers[0].mine(gold_mine_offsets[0]);
			state.villagers[1].mine(gold_mine_offsets[1]);

	.. cpp:member:: int64_t score

		Integer containing your current game score. You can only see your own score, and can't peek at your opponent's!

	.. cpp:member:: int64_t gold

		Integer containing your current gold reserves. Increses as you mine and decreases as you produce and build more units.


Inside the `state` object, we have vectors of Villagers, Soldiers and Factories as shown above. We'll continue with a description of each of those classes.

Soldier
=======

.. cpp:class:: Soldier

	The Soldier is an offensive unit. Use your soldiers to kill your opponent units, and tear down their factories!

	.. cpp:member:: int64_t id

		A unique ID associated with this soldier. It will never change.

	.. cpp:member:: Vec2D position

		The soldier's current position on the map.

	.. cpp:member:: int64_t hp

		The soldier's curent HP. Note that the max value of hp can be accessed from `SOLDIER_MAX_HP`.

	.. cpp:member:: SoldierState state

		The current state of the soldier. This member tells you what the soldier is doing right now, and has values **IDLE**, **MOVE**, and **ATTACK**.

		For example, to check for all your soldiers who are currently battling, you could do ::

			for (auto &soldier : state.soldiers) {
				if (soldier.state == SoldierState::ATTACK) {
					// Do something
				}
			}

	.. cpp:function:: move(Vec2D destination)

		Specify a position to which the soldier should move. Note that you don't need to keep moving your soldier or find a path. The engine handles path finding for you. Simply tell soldier where to go!

		For example, let's say you want the first soldier to move to the position where the first villager is ::

			Vec2D first_villager_pos = state.villagers[0].position;

			state.soldiers[1].move( first_villager_pos );

	.. cpp:function:: attack(Soldier &target)

		Attack the given target. Note that it doesn't have to be a soldier, you can attack factories or villagers too. You don't have to move your villager to your target if far away, the engine will do that for you if you're not in close range to attack.

		Let's say our first three soldiers should each attack the first three soldiers in the other team (Keep in mind, in real code, you'll want to add an `if` statement to make sure the opponent vector has atleast three units!) ::

			state.soldiers[0].attack( state.enemy_soldiers[0] );

			state

.. figure:: images/villagerGuide.png
	:width: 200px
	:alt: Player Villagers.soldiers[1].attack( state.enemy_soldiers[1] );

			state.soldiers[2].attack( state.enemy_soldiers[2] );
	
	.. cpp:function:: Vec2D closest_gold_mine(Vec2D position)

		A helper function to find the closest_gold_mine to the given position. This method does not guarantee that the gold mine is accessible.

		For more information, check down below in the Helpers section.


Villager
========

.. cpp:class:: Villager

	The Villager is a resource managing unit. Your villagers can mine gold, build factories, and even attack other enemy units if necessary. To make your villager perform actions, you issue it various commands like *move*, *attack*, *build*, and *mine*.

	.. cpp:member:: int64_t id

		A unique ID associated with this villager. It will never change.

	.. cpp:member:: Vec2D position

		The villager's current position on the map.

	.. cpp:member:: int64_t hp

		The villager's curent HP. Note that the max value of hp can be accessed from `VILLAGER_MAX_HP`.

	.. cpp:member:: VillagerState state

		The current state of the villager. This member tells you what the villager is doing right now, and has values **IDLE**, **MOVE**, **BUILD**, **ATTACK**, and **MINE**.

		For example, to check for all your villagers who are idle, you could do ::

			for (auto &villager : state.villagers) {
				if (villager.state == VillagerState::IDLE) {
					// Do something
				}
			}

	.. cpp:function:: void move(Vec2D destination)

		Specify a position to which the villager should move. Note that you don't need to keep moving your villager or find a path. The engine handles path finding for you. Simply tell villager where to go!

		For example, let's say you want the first villager to move to the position where the second villager is ::

			Vec2D first_villager_pos = state.villagers[0].position;

			state.villagers[1].move( first_villager_pos );

	.. cpp:function:: void attack(Soldier &target)

		Attack the given target. Note that it doesn't have to be a soldier, you can attack factories or villagers too. You don't have to move your villager to your target if far away, the engine will do that for you if you're not in close range to attack.

		Let's say our first three villagers should each attack the first villager, soldier, and factory in the other team (Keep in mind, in real code, you'll want to add an `if` statement to make sure each vector has atleast one element!) ::

			state.villagers[0].attack( state.enemy_villagers[0] );

			state.villagers[1].attack( state.enemy_soldiers[0] );

			state.villagers[2].attack( state.enemy_factories[0] );
		
	.. cpp:function:: void build(Vec2D offset, [FactoryProduction production_state])

		This villager will build a factory at the given offset. If the factory already exists, this villager will continue building. If it doesn't exist, this villager will move to create it.

		You can _optionally_ supply an additional parameter to set which type of unit the factory should produce once its construction has been completed. This defaults to `FactoryProduction::VILLAGER`.

		For example, to have the first five villagers build a new factory that will produce Soldiers at (7,10), you could do ::

			for (int i = 0; i < state.villagers.size(); ++i) {
				state.villagers[i].build( Vec2D(2,10), FactoryProduction::SOLDIER );
			}

	.. cpp:function:: void build(Factory &factory)

		An alternative of the above. If construction of a factory has already begun, you'll already see the new factory in your `factories` vector. You can pass it directly to a villager to send that villager to continue building.

		For example, if you want your first villager to continue building the last factory::

			auto &villager = state.villagers.front();
			auto &factory = state.factories.back();

			villager.build( factory );

	.. cpp:function:: void mine(Vec2D gold_mine_offset)

		Makes this villager move towards the given gold mine offset, and begin mining.

		For example, to make all the villagers to to the first gold mine, you can do ::

			Vec2D gold_mine_offset = state.gold_mine_offsets[0];

			for (auto &villager : state.villagers) {
				villager.mine( gold_mine_offset );
			}

Factory
=======

.. cpp:class:: Factory

	.. cpp:member:: int64_t id

		A unique ID associated with this factory. It will never change.

	.. cpp:member:: Vec2D position

		The factory's current position on the map. Note that this position the *center* of where the factory is located. A factory however occupies the space of the entire offset grid, and you cannot build another factory in this offset.

	.. cpp:member:: int64_t hp

		The factory's curent HP. Note that the max value of hp can be accessed from `FACTORY_MAX_HP`.

	.. cpp:member:: bool built

		Boolean to check if this factory's construction is finished

	.. cpp:member:: bool stopped

		Boolean to check if this factory has been stopped. If false, the factory is running.

	.. cpp:function:: void stop()

		This will stop the factory from producing units.  Note that factories will automatically stop themselves if you run out of gold. You need to restart the factory by calling `start()`

	.. cpp:function:: void start()

		Start the factory in case it has been stopped. If called on an already running factory, this is ignored.

		For example, to stop and restart the first factory in case you're low on gold::

			if (state.gold < 1000) {
				state.factories[0].stop();
			}
			else {
				state.factories[0].start();
			}

	.. cpp:function:: void produce_villagers()

		Makes this factory produce villagers. If the factory is already producing villagers, this is ignored.

	.. cpp:function:: void produce_soldiers()

		Makes this factory produce soldiers. If the factory is already producing soldiers, this is ignored.

		For example, to make all your factories produce soldiers if you have a lot of money (20 times your starting amount maybe), but produce villagers otherwise, you could do ::

			if (state.gold > 20 * GOLD_START) {
				for (auto &factory : state.factories) {
					factory.produce_soldiers();
				}
			}
			else {
				for (auto &factory : state.factories) {
					factory.produce_villagers();
				}
			}

	.. cpp:function:: void toggle_production()

		If factory is producing villagers, this makes it produce soldiers instead, and vice versa.

		For example, to toggle the production state of the first factory::

			state.factories[0].toggle_production();

Helpers
=======

Along with the game state, we've included some helper methods to make it easier for you to implement your logic. One common operation that you'd need to perform is converting between positions and offsets. For example, a factory is build using an offset, but when examined, it's position will be in *position* units, and **not** *offsets*.

So, we have some simple methods to convert between positions and offsets.

	.. cpp:function:: Vec2D PositionToOffset(Vec2D position)

		Returns the offset (i.e the grid) inside which the given position is located.

		.. figure:: images/positionToOffset.png
			:width: 400px
  			:alt: Positions to Offset Diagram


	.. cpp:function:: Vec2D OffsetToPositon(Vec2D offset)

		Returns the center position of the given offset. Note that factories and gold mines are actually point objects, situated at the center of the offset that they are represented by.

		.. figure:: images/offsetToPosition.png
			:width: 400px
  			:alt: Offset to Position Diagram

	.. cpp:function:: Vec2D State::closest_gold_mine(Vec2D position)


		As previously stated in the ``State`` section, this is a member function that gives you the closest_gold mine to a given location. You can use it like this ::

			auto &villager = state.villagers[0];
			if (!state.gold_mine_offsets.empty()) {
				villager.mine(state.closest_gold_mine( villager.position );
			}

		If you're interested, here's how this helper is implemented. You might get an idea of how to incorporate some more of the Code Character API into your code. ::

			Vec2D State::closest_gold_mine(Vec2D position) {
				// Initialize min distance and the closest gold mine (if it exists)
				double min_distance = std::numeric_limits<double>::max();
				Vec2D closest_gold_mine = gold_mine_offsets.size() ? gold_mine_offsets[0] : Vec2D::null;

				// For each gold mine...
				for (auto &gold_mine : gold_mine_offsets) {

					// If there's a closer gold mine, set it
					auto gold_mine_position = OffsetToPosition(gold_mine);
					auto distance_to_gold_mine = gold_mine_position.distance(position);

					if (distance_to_gold_mine < min_distance) {
							min_distance = distance_to_gold_mine;
							closest_gold_mine = gold_mine;
					}
				}

				return closest_gold_mine;
			}
		
		Note that you can do things like ``position1.distance(position2)``, where both positions are ``Vec2D`` objects, to find Euclidean distance. 
}


Other
=====

Note that *everything* shown above is printable. You can log any of this to output and view it in your game log. (Remember to use ``logr`` and not ``cout``!)

For example, if you want to print out the properties of a particular Villager, you could do::

	logr << state.villagers[0] << '\n';

*Output* ::

	Villager(id: 0) {
		position: (5, 5)
		hp: 80
		state: IDLE
	}

You can even log the entire `state` variable. Keep in mind, your output will be quite large.
