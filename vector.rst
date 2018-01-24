======
Vector
======
We've written a handly utility class ``physics::Vector`` used to represent 2D Vectors (components with X and Y directions).
You can do almost anything you'd do with a normal data type::

	using namespace physics;

	Vector a(1, 0);        // a.x = 1, a.y = 0
	Vector b(1.2, 1.3);    // You can use floats

	Vector c = a + b;      // c is 2.2, 1.3
	c = a - b;             // c is -0.2, -1.3
	c = a + 5              // Scalar addition, each component is added to the scalar, c = 6, 5
	c = a - 5              // Scalar subtraction, c = 1, -5
	c = a * 5              // Scalar multiplication, c = 5, 0
	c = a / 5.0            // Scalar division, c = 0.2, 0

	bool t = a == b        // You can compare vectors, their respective
	                       // components are compared, b = false
	bool t = a != b        // t = true

	double d = a.dot(b)    // Dot product
	d = a.magnitude()      // Magnitude of a, d = sqrt(a.x*a.x + a.y*a.y)
	d = a.distance(b)      // Euclidean distance between a and b

	std::cout << a;        // Prints "(1, 0)" without the quotes

This class is already included in your source file, so prepare yourselves to experience the euphoria of effortless Vector arithmetic :)

