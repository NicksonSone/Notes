# Numpy Tutorial

## Basics
**homogeneous multidimensional array**: a table of elements (usually numbers), all of the same type, indexed by a tuple of positive integers.
dimensions are called axes. The number of axes is rank.

[1, 2, 1] is rank 1, with one axis, and of length 3.

    [[ 1., 0., 0.],
    [ 0., 1., 2.]]
rank 2 (2 dimensions), length 2 for 1st dim and length 3 for 2nd dim.

NumPy’s array class is called **ndarray**, alias **array**.

Important attributes of an ndarray object:
* **ndarray.ndim**: the number of axes (dimensions, rank) of the array.
* **ndarray.ndim**: the dimensions of the array, tuple of integers indicating the size of each dimension.
* **ndarray.size**: the total number of elements
* **ndarray.dtype**: an object describing the type of the elements in the array. One can create or specify dtype’s using standard Python types. Additionally NumPy provides types of its own. numpy.int32, numpy.int16, and numpy.float64 are some examples.
* **ndarray.itemsize**: the size in bytes of each element of the array. For example, an array of elements of type float64 has itemsize 8 (=64/8), while one of type complex32 has itemsize 4 (=32/8). It is equivalent to ndarray.dtype.itemsize.
* **ndarray.data**: the buffer containing the actual elements of the array. Normally, we index into elements.

## Creation
array transforms sequences of sequences into two-dimensional arrays, sequences of sequences of sequences into three-dimensional arrays, and so on.
```Python
>>> a = np.array([1,2,3,4])  # RIGHT
>>> b = np.array([(1.5,2,3), (4,5,6)])
>>> b
array([[ 1.5,  2. ,  3. ],
       [ 4. ,  5. ,  6. ]])
>>> c = np.array( [ [1,2], [3,4] ], dtype=complex ) # define type
```
 **growing arrays is an expensive operation.**


create arrays with initial placeholder content
```Python
>>> np.zeros( (3,4) ) # creates an array full of zeros
>>> np.ones( (2,3,4), dtype=np.int16 )  # creates an array full of ones
>>> np.empty( (2,3) )  # create random numbers, depends on the state of the memory
```
create sequences of numbers
```Python
>>> np.arange( 10, 30, 5 ) # better used for integer
array([10, 15, 20, 25])
>>> np.linspace( 0, 2, 9 ) # for float, sepcify number of elements
array([ 0.  ,  0.25,  0.5 ,  0.75,  1.  ,  1.25,  1.5 ,  1.75,  2.  ])
```
For floating points, *np.arange* does **not guarantee the number of elements obtained**, due to the finite floating point precision.

## Printing
If an array is too large to be printed, NumPy automatically skips the central part of the array and only prints the corners:
```Python
>>> print(np.arange(10000))
[   0    1    2 ..., 9997 9998 9999]
>>> np.set_printoptions(threshold='nan')  # disable the skip
>>> np.set_printoptions(threshold=100)  # enable the skip
```
## Basic operation
Elementwise arithmetic operators, including * (multiplication). Use *dot* function for matrix product.
```Python
>>> a = np.array( [20,30,40,50] )
>>> b = np.arange( 4 )
>>> a-b
array([20, 29, 38, 47])
>>> a*b
array([  0,  30,  80, 150])
>>> a.dot(b)
260
```
+= and \*=, modify existing array  
```Python
>>> a *= 3
```
Unary operations
```Python
>>> a.sum()
2.5718191614547998
>>> a.min()
0.1862602113776709
>>> a.max()
0.6852195003967595
>>> b = np.arange(12).reshape(3,4)
>>> b.sum(axis=0)                            # sum of each column
>>> b.min(axis=1)                            # min of each row
>>> b.cumsum(axis=1)                         # cumulative sum along each row
```

## Indexing, Slicing and Iterating
One-dimensional arrays can be indexed, sliced and iterated over, much like lists in Python

Multidimensional arrays
```Python
>>> def f(x,y):
...     return 10*x+y
...
>>> b = np.fromfunction(f,(5,4),dtype=int)
>>> b
array([[ 0,  1,  2,  3],
       [10, 11, 12, 13],
       [20, 21, 22, 23],
       [30, 31, 32, 33],
       [40, 41, 42, 43]])
>>> b[2,3]
23
>>> b[0:5, 1]                       # each row in the second column of b
array([ 1, 11, 21, 31, 41])
>>> b[ : ,1]                        # equivalent to the previous example
array([ 1, 11, 21, 31, 41])
>>> b[1:3, : ]                      # each column in the second and third row of b
array([[10, 11, 12, 13],
       [20, 21, 22, 23]])
```
The dots (...) represent as many colons as needed to produce a complete indexing tuple
* ```x[1,2,...]``` is equivalent to ```x[1,2,:,:,:]```,
* ``x[...,3]`` to ``x[:,:,:,:,3]`` and
* ``x[4,...,5,:]`` to ``x[4,:,:,5,:]``.

Iterating over multidimensional arrays is done with respect to the first axis. However, one can use the *flat* attribute to perform an operation on each element:
```Python
>>> for row in b:
...     print(row)
...
>>> for element in b.flat:
...     print(element)
...
```

### indexing with arrays of indices
**A single array of indices** always refers to the **first dimension** of ```a```. The indexed values is change to the shape of indices array.


```Python
>>> a = np.arange(12).reshape(3,4)
array([[ 0,  1,  2,  3],
       [ 4,  5,  6,  7],
       [ 8,  9, 10, 11]])
>>> i = np.array([0, 2])    # refers to the first dim
>>> a[i]
array([[ 0,  1,  2,  3], # 0
       [ 8,  9, 10, 11]]) # 2

>>> b = np.arange(12)**2 # [0, 1^2, 2^2, 3^2, ...., 11^2]
>>> j = np.array( [ [ 3, 4], [ 9, 7 ] ] )
>>> b[j]
array( [ [ 9, 16], [ 81, 49 ] ] )
```

An array of indexes for each dim (**shapes of each array must be the same**)
```Python
>>> a = np.arange(12).reshape(3,4)
>>> i = np.array( [ [0,1],                        # indices for the first dim of a
...                 [1,2] ] )
>>> j = np.array( [ [2,1],                        # indices for the second dim
...                 [3,3] ] )
>>> a[i,j]                                     # i and j must have equal shape
array([[ 2,  5],
       [ 7, 11]])

>>> m = [i,j]       
>>> n = (i,j)       
>>> o = np.array([i, j])
>>> a[m] # right
>>> a[n] # right
>>> a[o] # wrong: interpreted as indexing with only one array

```
Time series example
```Python
>>> time = np.linspace(20, 145, 5)                 # time scale
>>> data = np.sin(np.arange(20)).reshape(5,4)      # 4 time-dependent series
>>> time
array([  20.  ,   51.25,   82.5 ,  113.75,  145.  ])
>>> data #　the 1st dim is time, 2nd dim is values
array([[ 0.        ,  0.84147098,  0.90929743,  0.14112001],
       [-0.7568025 , -0.95892427, -0.2794155 ,  0.6569866 ],
       [ 0.98935825,  0.41211849, -0.54402111, -0.99999021],
       [-0.53657292,  0.42016704,  0.99060736,  0.65028784],
       [-0.28790332, -0.96139749, -0.75098725,  0.14987721]])
>>>
>>> ind = data.argmax(axis=0)                   # index of the maxima for each series
>>> ind
array([2, 0, 3, 1])
>>>
>>> time_max = time[ ind]                       # times corresponding to the maxima
>>>
>>> data_max = data[ind, xrange(data.shape[1])] # => data[ind[0],0], data[ind[1],1]...
>>>
>>> time_max
array([  82.5 ,   20.  ,  113.75,   51.25])
>>> data_max
array([ 0.98935825,  0.84147098,  0.99060736,  0.6569866 ])
```
### indexing with boolean arrays
```Python
>>> a = np.arange(12).reshape(3,4)
>>> b = a > 4
>>> a[b]

>>> a = np.arange(12).reshape(3,4)
>>> b1 = np.array([False,True,True])             # first dim selection
>>> b2 = np.array([True,False,True,False])       # second dim selection

>>> a[b1,:] # equivalent to a[b1]
>>> a[:,b2]
>>> a[b1,b2]                                  # a weird thing to do
array([ 4, 10])
```


## Shape Manipulation
### Changing the shape of an array
Return a modified array

```Python
>>> a.ravel()  # returns a new array, flattened
>>> a.T  # returns a new array, transposed
>>> a.resize((2,6)) modify the array itself
```

The order of the elements in the array resulting from ravel() is normally **“C-style”**, that is, the rightmost index “changes the fastest”, **so the element after a[0,0] is a[0,1].** The functions ravel() and reshape() can also be instructed, using **an optional argument**, to use **FORTRAN-style arrays**, in which the leftmost index changes the fastest.

### Stacking together different arrays
np.vstack (vertical stack) stacks along first axes.
np.hstack （horizontal stack） stacks along second axes.
 ```Python
 >>> np.vstack((a,b))
array([[ 8.,  8.],
       [ 0.,  0.],
       [ 1.,  8.],
       [ 0.,  4.]])
>>> np.hstack((a,b))
array([[ 8.,  8.,  1.,  8.],
       [ 0.,  0.,  0.,  4.]])
 ```
np.column_stack:
1. stacks 1D arrays as columns into a 2D array. It first changes 1D arrays into 2D columns. (**length of arrays mush match**)
2. equivalent to hstack only for 2D arrays (**rows of arrays must match**)

newaxis:

```Python
>>> np.column_stack(([1, 2, 3], [4, 5, 6])) #  stacks 1D arrays as columns
array([[1, 4],
       [2, 5],
       [3, 6]])
>>> np.vstack(([1, 2], [3, 4])) # different from vstack for 1D array
array([[1, 2],
      [3, 4]])
>>> np.hstack(([1, 2], [3, 4]))
array([1, 2, 3, 4])


>>> a = np.floor(10*np.random.random((2,2)))
>>> b = np.floor(10*np.random.random((2,2)))
>>> np.column_stack((a,b))   # With 2D arrays, equivalent to hstack
array([[ 8.,  8.,  1.,  8.],
       [ 0.,  0.,  0.,  4.]])

>>> from numpy import newaxis
>>> a[:,newaxis]  # This allows to have a 2D columns vector a = [4, 2]
array([[ 4.],
       [ 2.]])
```

### Splitting one array into several smaller ones
hsplit: split an array along its horizontal axis
vsplit: split an array along its vertical axis
array_split: split an array along any axis
```Python
>>> np.hsplit(a,3)   # Split a into 3
>>> np.hsplit(a,(3,4))   # Split a after the third and the fourth column
```
## Copies and Views
1. Simple **assignments** make **no copy** of array objects or of their data.
2. **function calls** make **no copy**.
```Python
>>> b = a            # no new object is created
>>> b is a           # a and b are two names for the same ndarray object
True
```
3. creating a view or **slicing an array, makes new object, but shares data**
```Python
>>> a = np.arange(12)
>>> c = a.view()
>>> c is a
False
>>> s = a[ : , 1:3]     # create a view
>>> s[:] = 10           # s[:] create one more view, then changes all element to 10, which in turn modify original data in a.
```
**s[:] create one more view, then changes all element to 10, which in turn modify original data in a.**

4. The copy method makes a complete copy of the array and its data.

## ix_() function
This function takes N 1-D sequences and returns N outputs with N
dimensions each, such that the shape is 1 in all but one dimension
and the dimension with the non-unit shape value cycles through all
N dimensions.

Can be used to implement Reduce function(mapreduce).

``` Python
>>> a = np.array([2,3,4,5])
>>> b = np.array([8,5,4])
>>> c = np.array([5,4,6,8,3])
>>> ax,bx,cx = np.ix_(a,b,c)

>>> ax
array([[[2]],
       [[3]],
       [[4]],
       [[5]]])
>>> bx
array([[[8],
        [5],
        [4]]])
>>> cx
array([[[5, 4, 6, 8, 3]]])
>>> ax.shape, bx.shape, cx.shape
((4, 1, 1), (1, 3, 1), (1, 1, 5))

>>> bx * cx             # uses broadcast
array([[[40, 32, 48, 64, 24],
        [25, 20, 30, 40, 15],
        [20, 16, 24, 32, 12]]])
>>> result = ax+bx*cx
>>> result
array([[[42, 34, 50, 66, 26],
        [27, 22, 32, 42, 17],
        [22, 18, 26, 34, 14]],
       [[43, 35, 51, 67, 27],
        [28, 23, 33, 43, 18],
        [23, 19, 27, 35, 15]],
       [[44, 36, 52, 68, 28],
        [29, 24, 34, 44, 19],
        [24, 20, 28, 36, 16]],
       [[45, 37, 53, 69, 29],
        [30, 25, 35, 45, 20],
        [25, 21, 29, 37, 17]]])
```
