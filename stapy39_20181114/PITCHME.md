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
[the example of MNIST](https://github.com/pytorch/examples/blob/master/mnist/main.py).
@snapend


+++?image=assets/images/bg/white.jpg&position=left&size=25% 100%

@snap[west split-screen-heading span-30 text-white]
I want<br>to know
@snapend

@snap[east span-60]
<br>
@ul[split-screen-list](false)
- the befaviour of the model.
    - How will the tensors change
- the Computation Cost.
    - FLOPs
    - Amount of memory read and write
@ulend
@snapend


---?image=stapy39_20181114/images/torchstat_pypi.jpg&size=auto 85%

+++

## What can you know with torchstat?
@ul[squares]

- Total number of network parameters
- Theoretical amount of FLOPs and MAdd
- Memory usage

@ulend
---

## How to Use

- bash
- python module
+++
## As a CLI
```bash
$ torchstat --file main.py --model Net --size 1x28x28
[MAdd]: Dropout2d is not supported!
[Flops]: Dropout2d is not supported!
[Memory]: Dropout2d is not supported!
      module name  input shape output shape   params memory(MB)       MAdd      Flops  MemRead(B)  MemWrite(B) duration[%]  MemR+W(B)
0           conv1    1  28  28   10  24  24    260.0       0.02  288,000.0  149,760.0      4176.0      23040.0      57.31%    27216.0
1           conv2   10  12  12   20   8   8   5020.0       0.00  640,000.0  321,280.0     25840.0       5120.0       6.13%    30960.0
2      conv2_drop   20   8   8   20   8   8      0.0       0.00        0.0        0.0         0.0          0.0       9.10%        0.0
3             fc1          320           50  16050.0       0.00   31,950.0   16,000.0     65480.0        200.0      27.03%    65680.0
4             fc2           50           10    510.0       0.00      990.0      500.0      2240.0         40.0       0.43%     2280.0
total                                        21840.0       0.03  960,940.0  487,540.0      2240.0         40.0     100.00%   126136.0
=====================================================================================================================================
Total params: 21,840
-------------------------------------------------------------------------------------------------------------------------------------
Total memory: 0.03MB
Total MAdd: 960.94KMAdd
Total Flops: 487.54KFlops
Total MemR+W: 123.18KB
```
@[1](Assign module classs and define input size)
@[5-11](Details computational cost of networks)
@[13-18](Summary report of networks)

+++
## As a module
For more complicated model

```python
from torchstat import stat
import torchvision.models as models

model = models.resnet18()
stat(model, (3, 224, 224))
```

---
@snap[north-west]
Example
@snapend

Computing an image of MNIST on the model takes

- 487KFlops
- 123KB on memory.

On GTX1080Ti (#1), it'll take

- 0.046[ms] in foward computing.
- 0.00025[ms] in memory read and write.

So, total time is about 0.046 micro second.

@snap[south-west span-100]
@size[0.5em](1. GTX 1080Ti has computational ability of 10.6TFLOPs on FP32, data-transfer rate of 484GB/s!)
@snapend

---
## Future Works
- UI(detail, layer-wise)
- Export result table
- Arbitrary input shape
- GPU time

---
## Conclusion

[torchstat](https://github.com/Swall0w/torchstat) is a tool for

- visualizing your model
- estimating computational cost
    - network parameters
    - FLOPs and MAdd
    - Memory usage

Its is available on PyPI

```bash
$ pip install torchstat
```

---
## EOF

---
## 公開してから
### Github star

@ul[squares]

- 1日目：  3
- 2日目： 15
- 3日目：170
- 今：   338

@ulend

### Findy score
@ul[squares]

- Before: 62
- After: 86 (+24)

@ulend
