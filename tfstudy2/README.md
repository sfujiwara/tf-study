# TensorFlow Source Code I/O #2

| 開催日 | 会場 |
|:-:|:-:|
| 2017-04-27 19:00~ | [Google Japan](https://www.google.co.jp/maps/place/Google+Japan/@35.6601447,139.7272358,17.91z/data=!3m1!5s0x60188b77a7f6fcf5:0x571df4600f51bdfb!4m5!3m4!1s0x60188b770913970d:0xccc3467fcb15b353!8m2!3d35.6604105!4d139.7292645) |

## お題候補

* [Supervisor](https://www.tensorflow.org/programmers_guide/supervisor) が裏で何をしているかを調べる
* [Session](https://www.tensorflow.org/api_docs/python/tf/Session) のコードを読んで分散処理の仕組みを追う
* 分散処理で Variable や queue を共有するのに暗躍してるっぽい [resource container](https://www.tensorflow.org/api_docs/python/tf/Graph#container) について調べる

## 眺めるコード

* MonitoredSession
  - https://github.com/tensorflow/tensorflow/blob/master/tensorflow/python/training/monitored_session.py

## 議事録

* [memo.md](memo.md)
