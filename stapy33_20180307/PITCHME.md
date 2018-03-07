## Pytorchのすすめ

### Pytorchを使ってみよう

2018 Mar 07 
Masato Fujitake

※Tensorflowの話はしません．
---?include=common/whoami_stapy.md
---
# 深層学習歴
- 学校：物体検出
- バイト：文字認識
- 趣味：One-shot learningなど
- フレームワークはCaffe→Chainer→Pytorch

---
## 深層学習フレームワーク使ってMnistで手が止まる

- Examplesがソースコードだけでは分かりづらい
- 抽象化され過ぎてて変え場所が分からない
- そもそもどういうことが出来るか分からない

---
## Pytorchで解決できます
![pytorch](stapy33_20180307/images/pytorch-logo-flat.png)

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
