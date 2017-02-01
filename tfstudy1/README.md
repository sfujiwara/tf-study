# tfstudy 1

| 開催日 | 会場 |
|:-:|:-:|
| 2017-02-02 19:00~ | [Google Japan](https://www.google.co.jp/maps/place/Google+Japan/@35.6601447,139.7272358,17.91z/data=!3m1!5s0x60188b77a7f6fcf5:0x571df4600f51bdfb!4m5!3m4!1s0x60188b770913970d:0xccc3467fcb15b353!8m2!3d35.6604105!4d139.7292645) |

## お題

TF-Slim で VGG 16 のような学習済み既存モデルを提供するコードを眺めて、モデルの保存のし方とか、それを元に転移学習する場合どう書くのが良さそうかとか考えよう。

## 眺めるコード

* https://github.com/tensorflow/models/blob/master/slim/nets/vgg.py
