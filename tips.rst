============
Tips and Tricks
============

Here's some more stuff that you might find useful, not covered in the other sections


Persisting Variables
--------------------

If you need a variable that retains it's value over multiple turns, you can either make it a global variable, outside your update function, or make it a ``static`` variable.

For example, a common requirement is to know what the current turn is. Let's do this two different ways:

**Global Variable** ::

	int turn = 0;
	
	State PlayerCode::Update(State state) {
		turn++;
		logr << "Turn : " << turn << std::endl;
	}

**Static Variable** ::

	State PlayerCode::Update(State state) {
		static int turn = 0;
		turn++;
		logr << "Turn : " << turn << std::endl;
	}

Use the Standard Library!
-------------------------

The C++ Standard Library is immense and powerful. Use it to your advantage! Just make sure you ``#include`` the right headers. Anything upto C++14 is available.

Let's say for whatever reason, you'd like to sort your villagers by hp. Since ``state.villagers`` is a ``std::vector``, we can use ``std::sort`` with a custom comparator to achieve this. ::

	// Remember to make a COPY of the villagers. Don't mess up the original state!
	auto my_villagers = state.villagers;

	// Use a custom comparator lambda to sort by HP
	std::sort(my_villagers.begin(), my_villagers.end(), 
		[](const auto &a, const auto &b) -> bool { 
			return a.hp < b.hp; 
		}
	); 

	// Log the villagers

Vec2D has several methods
-------------------------

``Vec2D`` has several common operations, like calculating distance and scalar multiplication programmed in. Use these methods to avoid writing more code.::

	Vec2D position1(3, 5);
	Vec2D position2(4, 23);

	double distance = position1.distance(position2);

Check out the `Vec2D <vec2d.html>`_ page if you haven't already.
