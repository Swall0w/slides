@title[torchstat Model Analyzer in PyTorch]

## @color[gray](torchstat<br> Model Analyzer in PyTorch)

[Start Python Club #39](https://startpython.connpass.com/event/101476/) LT


2018 Nov 14
Masato Fujitake

---?include=common/whoami_stapy_en.md

---

## @color[white](Deep Learning in PyTorch)

+++?image=stapy39_20181114/images/pytorch_home.jpg&size=auto 100%

+++

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


+++

@snap[north]
Things developers do for modeling
@snapend

@snap[west list-content-verbose span-100]
<br>
@ul[](false)
- Build Neural Networks Architecture.
- Debug the model.
- Estimate its Computation Cost.
- Check the befaviour of the model.
@ulend
@snapend

+++

@snap[north]
Things developers do for modeling
@snapend

## 1. pathlibが便利

os.pathに変わるデフォルトモジュール

    >>> from pathlib import Path

    >>> dataset = 'images'
    >>> datasets_root = Path('/path/to/datasets/')

    >>> train_path = datasets_root / dataset / 'train'
    >>> test_path = datasets_root / dataset / 'test'

    >>> for image_path in train_path.iterdir():
    ...     with image_path.open() as f: 
    ...         pass

+++

glob関係も楽に扱える

    # Python 2
    >>> import glob
    >>> found_images = \
    ...     glob.glob('/path/*.jpg') \
    ...   + glob.glob('/path/*/*.jpg') \
    ...   + glob.glob('/path/*/*/*.jpg')

    # Python 3 with pathlin
    >>> found_images = pathlib.Path('/path/').glob('**/*.jpg')

    # Python 3
    >>> found_images = glob.glob('/path/**/*.jpg', recursive=True)

---

## 2. アンダースコアで見やすく

    # 千単位をアンダースコアで区切る
    >>> one_million = 1_000_000
    >>> one_million
    1000000
    >>> type(one_million)
    <class 'int'>

    # 16進数も可能
    >>> addr = 0xCAFE_F00D
    >>> addr
    3405705229
    >>> type(addr)
    <class 'int'>

--- 
## 3. f-stringsで綺麗に！

format構文がもっと楽に！

    # Python 2
    >>> print('{batch:3} accuracy: {acc_mean:0.4f}'.format(
    ...    batch=batch, acc_mean=numpy.mean(accuracies)))
    100 accuracy: 0.8021


    >>> print('{:3} accuracy: {:0.4f}'.format(
    ...    batch, numpy.mean(accuracies)))


    # Python 3
    >>> print(f'{batch:3} accuracy: {numpy.mean(accuracies):0.4f}')


---
## 4. 実はdictがOrderedDict
CPython3.7+ではdictがOrderedDictのように振る舞う

    >>> x = {str(i):i for i in range(5)}

    # Python 2
    >>> x
    {u'1': 1, u'0': 0, u'3': 3, u'2': 2, u'4': 4}

    # Python 3
    >>> x
    {'0': 0, '1': 1, '2': 2, '3': 3, '4': 4}

---

## 5. 拡張されたアンパッキング
アンパッキングでこれが出来る

    >>> a, b = range(2)
    >>> a
    0
    >>> b
    1

    >>> a, b, *rest = range(10)
    >>> a
    0
    >>> b
    1
    >>> rest
    [2, 3, 4, 5, 6, 7, 8, 9]

+++

ちなみに*restはどこにでもおける

    >>> a, *rest, b = range(10)
    >>> a
    0
    >>> b
    9
    >>> rest
    [1, 2, 3, 4, 5, 6, 7, 8]

    >>> *rest, b = range(10)
    >>> rest
    [0, 1, 2, 3, 4, 5, 6, 7, 8]
    >>> b
    9
+++
危ないけど使える？使い方
    >>> with open('this.txt') as f:
    ...    first, *_, last = f.readlines()
    # 全部読み込まれるので注意！
    >>> first
    'Beautiful is better than ugly.'
    >>> last
    "Namespaces are one honking great idea -- let's do more of those!"

---
## まとめ
- 強いpathlib
- 使えるアンダースコア
- 簡素なformat構文
- dictの振る舞い
- 色々使えるアンパック


ぜひ使ってみてください

---
## References
- [PEP 0 -- Index of Python Enhancement Proposals (PEPs)](https://www.python.org/dev/peps/)
- [Python 3 for Scientists](http://python-3-for-scientists.readthedocs.io/en/latest/)
- [10 awesome features of Python that you can't use because you refuse to upgrade to Python 3](https://www.asmeurer.com/python3-presentation/slides.html#1)
- [Migrating to Python 3 with pleasure](https://github.com/arogozhnikov/python3_with_pleasure)

---
## EOF
