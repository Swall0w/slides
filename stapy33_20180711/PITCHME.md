## Python3へ移行しよう

### Python3で出来る便利機能

2018 Jul 11
Masato Fujitake

---?include=common/whoami_stapy.md

---

## ![Moving to require Python 3](http://python3statement.org/)

---?image=stapy33_20180711/images/project.png&size=auto 60%

---

## 1. pathlib
os.pathに変わるデフォルトモジュール

    >>> from pathlib import Path

    >>> dataset = 'images'
    >>> datasets_root = Path('/path/to/datasets/')

    >>> train_path = datasets_root / dataset / 'train'
    >>> test_path = datasets_root / dataset / 'test'

    >>> for image_path in train_path.iterdir():
            with image_path.open() as f: 
                pass

+++

glob関係も楽に扱える

    # Python 2
    >>> import glob
    >>> found_images = \
            glob.glob('/path/*.jpg') \
          + glob.glob('/path/*/*.jpg') \
          + glob.glob('/path/*/*/*.jpg')

    # Python 3 with pathlin
    >>> found_images = pathlib.Path('/path/').glob('**/*.jpg')

    # Python 3
    >>> found_images = glob.glob('/path/**/*.jpg', recursive=True)

---

## 数字のアンダースコア

    # 千単位をアンダースコアで区切る
    >>> one_million = 1_000_000
    <class 'int'>

    # 16進数も可能
    >>> addr = 0xCAFE_F00D
    >>> type(addr)
    <class 'int'>

--- 
## f-strings

format構文がもっと楽に！
    # Python 2
    >>> print('{batch:3} accuracy: {acc_mean:0.4f}'.format(
           batch=batch, acc_mean=numpy.mean(accuracies)))
    100 accuracy: 0.8021

    >>> print('{:3} accuracy: {:0.4f}'.format(
           batch, numpy.mean(accuracies)))

    # Python 3
    >>> print(f'{batch:3} accuracy: {numpy.mean(accuracies):0.4f}')


+++
### [Tutorial](http://pytorch.org/tutorials/)が強い
[Fine-Tune](http://pytorch.org/tutorials/beginner/transfer_learning_tutorial.html#sphx-glr-beginner-transfer-learning-tutorial-py)もチュートリアルである
![tutorial](stapy33_20180307/images/pytorch_tutorial.png)

+++
### コミュニティが凄い
Stack overflow風の質問サイトがある
![discuss](stapy33_20180307/images/pytorch_discuss.png)

---
## Pytorch使いやすいです
ぜひ使ってみてください

`conda install pytorch torchvision -c pytorch`

---
## EOF
