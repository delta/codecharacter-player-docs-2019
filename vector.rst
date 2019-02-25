======
Vector
======

We've written a handy utility class ``Vec2D`` used to represent 2D Vectors (components with X and Y directions).
You can do almost anything you'd do with a normal data type::

	Vec2D a(1, 0);           // a.x = 1, a.y = 0
	Vec2D b(2, 2);

	Vec2D c = a + b;         // c is 3, 2
	c = a - b;               // c is -1, -2
	c = a + 5                // Scalar addition, each component is added
	                         // to the scalar, c = 6, 5

	c = a - 5                // Scalar subtraction, c = -4, -5
	c = a * 5                // Scalar multiplication, c = 5, 0

	bool t = a == b          // You can compare vectors, their respective
	                         // components are compared, t = false
	bool t = a != b          // t = true

	double d = a.dot(b)      // Dot product
	d = a.magnitude()        // Magnitude of a, d = sqrt(a.x*a.x + a.y*a.y)
	d = a.distance(b)        // Euclidean distance between a and b

	logr << a;               // Prints "(1, 0)" without the quotes

We also have DoubleVec2D, in case you'd like use some floating points::

	DoubleVec2D x(5.0, 3.0)  // You can do anything you could do with Vec2D

	Vec2D x_int = x.to_int() // Round your DoubleVec2D down to a Vec2D

	DoubleVec2D rounded_float = x_int.to_double();
				 // Convert any Vec2D into a DoubleVec2D with ease

These classes are already included in your source file, so prepare yourselves to experience the euphoria of effortless Vector arithmetic :)

Bonus
=====

The Vec2D and DoubleVec2D are simply aliases of the the Vector class, which is a templated type. Vec2D corresponds to `Vector<int64_t>` and DoubleVec2D is `Vector<double>`.

In case you want to use any other numeric type, feel free to do `Vector<your_numeric_type>` but you should be fine using just Vec2D and the occasional DoubleVec2D.
