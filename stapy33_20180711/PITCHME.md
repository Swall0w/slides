## Python3で楽しむ小技集

### Python3で出来る便利機能

2018 Jul 11
Masato Fujitake

---?include=common/whoami_stapy.md

---

## ![Moving to require Python 3](http://python3statement.org/)

---?image=stapy33_20180711/images/project.png&size=auto 80%

---

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
           batch=batch, acc_mean=numpy.mean(accuracies)))
    100 accuracy: 0.8021


    >>> print('{:3} accuracy: {:0.4f}'.format(
           batch, numpy.mean(accuracies)))


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
    'Namespaces are one honking great idea -- let's do more of those!'




---
## まとめ
- 強いpathlib
- 使えるアンダースコア
- 簡素なformat構文
- dictの振る舞い
- 色々使えるアンパック

ぜひ使ってみてください

---
## EOF
