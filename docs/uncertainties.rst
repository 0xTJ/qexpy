Uncertainties Module
====================

This module is the core of the QExPy package, this is where the Measurement
class of objects is created and the methods which allow for derivatives to be
calculated and the names and units of values to be stored and propagated.

Creating Measurement Objects
----------------------------

The method that will be used most commonly is the Measured class. This object
can store the mean, standard deviation, original data, name, units, and other
attributes which can be used by other elements of this package.

.. autoclass:: QExPy.uncertainties.Measured

The arguments, or *args, of this class can be in several forms:

A mean and standard deviation can be entred directly.

.. code-block:: python
   
   import QExPy.uncertainties as u
   x = u.Measured(10, 1)
   # This would create an object with a mean of 10 and a standard
   # deviation of 1.

A list or numpy array of values can be provided, from which the mean and
standard deviation of the values can be taken.

.. code-block:: python
   
   x = u.Measured([9, 10, 11], name='Data')
   # This would also produce an object with a mean of 10 and a standard
   # deviation of 1.

If the list of values has errors associated with each measurement, the
data can be entered either as pairs of a value and error, or as two lists
of data and error respectivly.

.. code-block:: python
   
   x = u.Measured([10, 1], [9, 0.5], [11, 0.25])
   y = u.Measured([10, 9, 11], [1, 0.5, 0.25])
   # The mean and standard deviation of x and y are the same

The optional arguments *name* and *units* can be used to include strings
for both of these parameters as shown below:

.. code-block:: python

   x = u.Measured(10, 1, name='Length', units='cm')

Working with Measurement Objects
--------------------------------

Once created, these objects can be operated on just as any other value:

.. code-block:: python
   
   import QExPy.uncertainties as u

   x = u.Measured(10, 1)
   y = u.Measured(3, 0.1)
   z = x-y
   f = u.sin(z)

   print(z)
   >> 10 +/- 1

Elementary functions such as the trig functions, inverse trig functions,
natural logarithm and exponential function can also be used:

.. code-block:: python

   f = u.sin(z)
   print(f)
   >> 0.7 +/- 0.8

Furthermore, the use of Measured objects in equations also allows for the
calculation of the derivative of these expressions with respect to any of the
Measured objects used.

.. code-block:: python

   d1 = f.derivative(x)

   # This can be compared to the analytic expression of the derivative
   d2 = m.cos(10+3)*3
   print(d1, d2)
   >> VALVALVAL
   
   


This will produce an object with a mean of 10 and a standard deviation of 1.

.. autoclass:: QExPy.uncertainties.Measurement

This class is not used by the user directly; however, it is used by subclasses,
as shown above, which can be used by the user.