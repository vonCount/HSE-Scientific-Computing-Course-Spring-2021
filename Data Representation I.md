Data representation I

Exercise: Pretend we use a naïve floating-point format with 5bit mantissa and 3bit exponent (base-2). What is the smallest possible positive number representable? What is the largest positive number representable? The first bit of each is used for sign:

	[±****][±**]
	 ^^^^^  ^^^--- exponent
	   |---------- mantissa
One of the many perils of working with floating-point numbers: recall that the fraction 1/3 has an infinitely long decimal expansion, while 1/10 has a finite expansion:

	1/10 = 0.1
	1/3  = 0.333…
In binary, we have a similar problem: powers of 2 have finite expansions, while 1/10 has an infinite expansion:

	1/2  = 0.1₂
	1/10 = 1/16 + 1/32 + 1/256 + ⋯
	     = 0.00011001… ₂
Since our processors use binary floating point, we have to truncate (cut off) this representation, resulting in an imperfect approximation of 1/10.

Exercise: use python to check this:

from decimal import Decimal

print(repr(Decimal(0.1)))
should result in

Decimal('0.1000000000000000055511151231257827021181583404541015625')
Exercise: what is the best approximation of 0.01?

Read the Python floating point tutorial for more information on how this can apply to python.
