# NumPy

## `ndarray`

```python
arr = np.array([[1.0, 2.0, 3.0], [4.0, 5.0, 6.0], [7.0, 8.0, 9.0]])
arr = np.empty([3, 3])          # Fill specific value: zeros(), ones(). 
arr = np.arange(50, 100, 2)   # Get values in [50, 100) with step size 2.
arr = np.linspace(50, 100, 6) # Get 6 values in [50, 100].

print(arr.dtype) # float64
print(arr.shape) # (6,)
print(arr.T)     # [ 50.  60.  70.  80.  90. 100.]
```

## `random`

```python
rng = np.random.default_rng() # Default Random Numeral Generator.

print(rng.permutation(np.arange(1, 11, 2))) # Get permutation on the first dimension of the ndarray.
```

## Math Function

~~~python
print(np.degrees(np.pi/4))

print(np.sin(np.pi/4))
print(np.cos(np.pi/3))
print(np.tan(np.pi/4))

print(np.arcsin(0.707)/np.pi)
print(np.arccos(0.5)/np.pi)
print(np.arctan(1)/np.pi)

print(np.around(1.357, 2))
print(np.floor(1.357))
print(np.ceil(1.357))
~~~

## 四则运算

四则运算可以用于数组与数和数组与数组，可以与`=`缩写提高运算效率。

NumPy中数组的四则运算是元素级别的运算，矩阵乘积可以用@来完成。

