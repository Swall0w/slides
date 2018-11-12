@title[torchstat Model Analyzer in PyTorch]

## @color[gray](torchstat<br> Model Analyzer in PyTorch)

[Start Python Club #39](https://startpython.connpass.com/event/101476/) LT


2018 Nov 14
Masato Fujitake

---?include=common/whoami_stapy_en.md

---

## @color[white](Deep Learning in PyTorch)

+++?image=stapy39_20181114/images/pytorch_home.jpg&size=auto 100%

+++?color=lavender
@title[Model Code Block]

```python
class Net(nn.Module):
    def __init__(self):
        super(Net, self).__init__()
        self.conv1 = nn.Conv2d(1, 10, kernel_size=5)
        self.conv2 = nn.Conv2d(10, 20, kernel_size=5)
        self.conv2_drop = nn.Dropout2d()
        self.fc1 = nn.Linear(320, 50)
        self.fc2 = nn.Linear(50, 10)

    def forward(self, x):
        x = F.relu(F.max_pool2d(self.conv1(x), 2))
        x = F.relu(F.max_pool2d(self.conv2_drop(self.conv2(x)), 2))
        x = x.view(-1, 320)
        x = F.relu(self.fc1(x))
        x = F.dropout(x, training=self.training)
        x = self.fc2(x)
        return F.log_softmax(x, dim=1)
```
@[1-8](Initialization of parameters)
@[10-17](Foward Computation: How to flow the input)

@snap[north-west]
Example of Model
@snapend

@snap[north-east template-note text-gray]
Please refer to [the example of MNIST](https://github.com/pytorch/examples/blob/master/mnist/main.py).
@snapend


+++

@snap[north]
I want to know... :worried:
@snapend

@snap[west list-content-verbose span-100]
<br>
@ul[](false)
- the befaviour of the model.
    - How will the tensors change
- the Computation Cost.
    - FLOPs (FLoating-point Operations Per Second)
    - Amount of memory read and write
@ulend
@snapend


---?image=stapy39_20181114/images/torchstat_pypi.jpg&size=auto 100%

## What can you do with torchstat?
+++

## How to Use

- python module
- bash

---
## Example of estimating cost

---
## Future Works
- UI(detail, layer-wise)
- Export result table
- Arbitrary input shape
- GPU time

---
## Conclusion

torchstat is a tool for
- visualizing your model
- estimating computational cost of models
    - Total number of network parameters
    - Theoretical amount of floating point arithmetics (FLOPs)
    - Theoretical amount of multiply-adds (MAdd)
    - Memory usage


Its is available on PyPI and new features will be available soon.

I hope you enjoy debugging your model:laughing:

---
## EOF
