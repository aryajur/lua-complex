lua-complex
===========

Introduction
------------
"complex.lua" is a simple library for complex numbers written in pure lua. If you want to use it, just download the file "complex.lua" and put it somewhere in your LUA_PATH. You can byte compile it using luac in order to obtain a "complex.luac" file. Then start lua using lua -l complex or add a require "complex" in your lua file.

Tutorial
--------

If you want to create the complex number 3+4i, type

	> x1=3+4*math.i

If you are lazy, you can also type

	>I=math.i
	>x1=3+4*I

As you can notice, "complex.lua" add an new entry in the math table. This entry is the complex number i itself and since "complex.lua" use the lua arithmetic metamethods, everything build from math.i will be a lua complex number (there is no need of a complex.new function). Just to check, type

	> =type(math.i)
	complex

	> =type(x1)
	complex

Let us create a second complex number

	> x2=2-3*math.i

Let us try some basic arithmetic

	> =-x2
	-2+3i
	
	> =x1+10
	13+4i
	
	> =x2*10
	20-30i
	
	> =x1-5*math.i
	3-i

	> =x1*x2
	18-i

	> =x1/x2
	-0.46153846153846+1.3076923076923i

	> =x1^(3/2)
	2+11i

	> =x1^x2
	-398.06079344495-67.457050438711i

If you want to compute the complex conjugate of x1, you can type

	> =complex.conj(x1)
	3-4i

But I do prefer the more compact OO notation

	> =x1:conj()
	3-4i

If you want to make a copy of the complex numbers x1 and x2, use

	> x3=x1:copy()
	> x4=x2:copy()

Now you have

	> =x3
	3+4i

	> =x4
	2-3i

If you want to compare two complex numbers, the lua relational metamethod allows you to use ==. For instance, if you want to compare x1 and x3

	> =x1==x3
	true

and what about x1 and x4?

	> =x1==x4
	false

If you want to access the real and the imaginary part of x1, just use

	> =x1:real()
	3

	> =x1:imag()
	4

These functions can also be used to modify a complex number. For example, if I want to modify the real part of x3

	> x3:real(-30)
	> =x3
	-30+4i

If I want to modify the imaginary part of x4 and add 1

	> =x4:imag(20)+1
	3+20i

If you want to print complex numbers, you can simply type

	> print(x1,x2)
	3+4i 2-3i

or, if you want to have more control on what you print, you can do something like

	> =string.format("%s complex = %3.1f%+3.1fi\n%s complex = %4.2f%+4.2fi\n","1st",x1,"2nd",x2)
	1st complex = 3.0+4.0i
	2nd complex = 2.00-3.00i

As you can see, the string.format function has been modified in order to take complex numbers into account. For each complex number in the list, you have to define two consecutive numerical formats (one for the real part, one for the imaginary part).

If you want to compute the argument of x1, just type

	> =complex.arg(x1)
	0.92729521800161

or

	> =x1:arg()
	0.92729521800161

If you want to compute the modulus (or absolute value) of x1, just type

	> =complex.abs(x1)
	5

	or

	> =x1:abs()
	5

or even

	> =math.abs(x1)
	5

As you can see, the original math.abs function has been modified in order to handle complex numbers. If the argument is a real number, then you get the usual absolute value and if the argument is a complex number, you get the complex absolute value, i.e. the modulus.

All the following math functions work with complex numbers:
pow
exp, log, sqrt
cos, sin, tan
acos, asin, atan
cosh, sinh, tanh
acosh, asinh, atanh

You can use them using the "complex." form, the ":" form or the "math." form. For instance, the sin of x2 can be computed by any of these forms

	> =complex.sin(x2)
	9.1544991469114+4.1689069599666i

	> =x2:sin()
	9.1544991469114+4.1689069599666i

	> =math.sin(x2)
	9.1544991469114+4.1689069599666i

Using the "math." form allows to use the same function for both real and complex numbers. For instance, you can type

	> =math.cos(math.pi)
	-1

and it works as usual, but you can also use it for a complex number

	> =math.cos(x1)
	-27.034945603074-3.8511533348118i

In the case where the argument is a real number but the function is not defined for this real value, the "math." form yields a complex result. For example

	> =math.log(1)
	0

but

	> =math.log(-1)
	3.1415926535898i

while, without "complex.lua", you get

	> =math.log(-1)
	nan

Finally, if you want to compute the n-th roots of a complex number, where n >= 1 is an integer, use the complex.roots function. For instance, if you want to compute the 4-th roots of x1, type

	> r=x1:roots(4)
	> for i=1,4 do print(i,r[i]) end
	1 1.4553466902254+0.34356074972251i
	2 -0.34356074972251+1.4553466902254i
	3 -1.4553466902254-0.34356074972251i
	4 0.34356074972251-1.4553466902254i

As you can see, r is a table containing 4 complex numbers 4-th roots of x1. Let us check if it work

	> for i=1,4 do print(r[i]^4) end
	3+4i
	3+4i
	3+4i
	3+4i

Looks OK!

