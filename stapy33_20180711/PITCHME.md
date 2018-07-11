## Python3へ移行しよう

### Python3で出来る便利機能

2018 Jul 11
Masato Fujitake

---?include=common/whoami_stapy.md

## ![Moving to require Python 3](http://python3statement.org/)

---?image=stapy33_20180711/images/project.png&size=auto 60%

---

## 1. pathlib
os.pathに変わるデフォルトモジュール

    from pathlib import Path

    dataset = 'wiki_images'
    datasets_root = Path('/path/to/datasets/')

    train_path = datasets_root / dataset / 'train'
    test_path = datasets_root / dataset / 'test'

    for image_path in train_path.iterdir():
        with image_path.open() as f: # note, open is a method of Path object
            # do something with an image

---

## Pytorchとは

- Torch7 & Chainerを元に作られた
- Define by Run
- Pythonicなコードでそこそこ抽象化
- FacebookやUber, 有名大学が開発してる
![pytorchhome](stapy33_20180307/images/pytorch_home.png)

--- 
## Pytorchのいい理由

- Tutorialが強い
- 新しいネットワークのリポジトリがたくさん
- コミニュティでの情報交換が凄い

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
