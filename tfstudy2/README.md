# TensorFlow Source Code I/O #2

| 開催日 | 会場 |
|:-:|:-:|
| 2017-04-27 19:00~ | [Studio Geeks](https://www.google.co.jp/maps/place/%E3%82%B3%E3%83%AF%E3%83%BC%E3%82%AD%E3%83%B3%E3%82%B0%E3%82%B9%E3%83%9A%E3%83%BC%E3%82%B9+studio+geeks/@35.7067443,139.7614833,17z/data=!4m12!1m6!3m5!1s0x60188c233f3ed6af:0x12144e940c954ed8!2z44Kz44Ov44O844Kt44Oz44Kw44K544Oa44O844K5IHN0dWRpbyBnZWVrcw!8m2!3d35.70674!4d139.763672!3m4!1s0x60188c233f3ed6af:0x12144e940c954ed8!8m2!3d35.70674!4d139.763672) |

## お題候補

* [Supervisor](https://www.tensorflow.org/programmers_guide/supervisor) が裏で何をしているかを調べる
* [Session](https://www.tensorflow.org/api_docs/python/tf/Session) のコードを読んで分散処理の仕組みを追う
* 分散処理で Variable や queue を共有するのに暗躍してるっぽい [resource container](https://www.tensorflow.org/api_docs/python/tf/Graph#container) について調べる

## 眺めるコード

* MonitoredSession
  - https://github.com/tensorflow/tensorflow/blob/master/tensorflow/python/training/monitored_session.py

## 議事録
