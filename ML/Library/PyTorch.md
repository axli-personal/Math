# Pytorch

## Torch.Tensor

#### `item()`

Returns the value of this tensor as a standard Python number. This only works for tensors with one element.

## Torch.nn

内部提供了很多实用的方法和类。

### Linear Model

在这个线性的模型中weight和bias一开始是随机的值。

```python
dim_in  = 3
dim_out = 5
linear_module = nn.Linear(dim_in, dim_out)
data = torch.tensor([[1.0, 2.0, 3.0], [5.0, 7.0, 9.0]])
print(linear_module.weight)
print(linear_module.bias)
print(linear_module(data))
```

### Activation Function

ReLU函数可以把所有的负数都变成0。

```python
activation_function = nn.ReLU()
without_activation = torch.tensor([-1, 0, 1])
print(activation_function(without_activation))
```

Tanh函数是双曲正切函数，可以把值映射到(-1, 1)内。

```python
activation_function = nn.Tanh()
without_activation = torch.tensor([-0.4, 1.2])
print(activation_function(without_activation))
```

Sigmoid函数可以把值映射到(0, 1)内，形状为S型。

```python
activation_function = nn.Sigmoid()
without_activation = torch.tensor([-0.4, 1.2])
print(activation_function(without_activation))
```

### Sequential

你可以用利用Sequential把一连串的模型包成一个模型。

```python
dim_in  = 3
dim_hidden = 4
dim_out = 5
data = torch.tensor([[1.0, 2.0, 3.0], [5.0, 7.0, 9.0]])

model = nn.Sequential(
    nn.Linear(dim_in, dim_hidden),
    nn.Tanh(),
    nn.Linear(dim_hidden, dim_out),
    nn.Sigmoid()
)

# print the parms in the model.
for parm in model.parameters():
    print(parm)

print(model(data))
```

### Loss Function

#### `MSELoss()`

```python
MSE = nn.MSELoss()

output = torch.tensor([1.0, 2.0, 3.0, 4.0])
label  = torch.tensor([0.0, 0.0, 0.0, 0.0])

print(MSE(output, label).item()) # 7.5
```

#### `Softmax()`

$$
f(x_i) = \frac{e^{x_i}}{\sum_{j=0}^{bound} e^{x_j}}
$$

```python
data = torch.tensor([-5000.0, 5000.0])
Softmax = nn.Softmax(dim=0)
print(Softmax(data)) # tensor([0., 1.])
```

#### `CrossEntropyLoss()`

由于交叉熵的倒数计算比`Sigmoid()`计算的快，所有常用于分类问题的损失函数。
$$
CrossEntropyLoss(O, T) = -\sum_{i=0}^{bound}T(i)\log_2O(i)
$$

```python
CrossEntropy = nn.CrossEntropyLoss()

output = torch.tensor([[0.4, 0.5, 0.1], [0.9, 0.1, 0.0], [0.6, 0.2, 0.2]])
# for each output target must provide the class it belong to.
target = torch.tensor([1, 0, 0])

# Note: CrossEntorpy will softmax the output before calculate the loss.
print(CrossEntropy(output, target)) # tensor(0.8049)
```

### Linear Regression using GD

```python
model = nn.Linear(1, 1)
optim = torch.optim.SGD(model.parameters(), lr=0.05)
mse = nn.MSELoss()

x = torch.tensor([[1.0], [2.0], [4.0], [5.0]])
y = torch.tensor([[3.0], [5.0], [9.0], [11.0]])

# using all the data, then update.
for i in range(20):
    predict = model(x)
    loss = mse(predict, y)
    optim.zero_grad()
    loss.backward()
    optim.step()
    print(i, loss.item() ,model.weight.view(1).detach().numpy(), model.bias.view(1).detach().numpy())
```

### Linear Regression using SGD

```python
model = nn.Linear(1, 1)
optim = torch.optim.SGD(model.parameters(), lr=0.05)
mse = nn.MSELoss()

x = torch.tensor([[1.0], [2.0], [4.0], [5.0]])
y = torch.tensor([[3.0], [5.0], [9.0], [11.0]])

# using one sample, then update parameters immediately.
for i in range(200):
    index = np.random.choice(4)
    predict = model(x[index])
    loss = mse(predict, y[index])
    optim.zero_grad()
    loss.backward()
    optim.step()
    if i % 10 == 0:
    	print(i, loss.item() ,model.weight.view(1).detach().numpy(), model.bias.view(1).detach().numpy())
```

