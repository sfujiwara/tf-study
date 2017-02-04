# 議事録

## 学習モデルの選定

* 同じようなサンプルコードや学習済みモデルを探す --> 無ければ似たような論文を探す、みたいな順番
  - 特に英語の論文を読むのは嫌がる人が多い
  - それに抵抗が無い人でも論文を漁って上手くいくかはギャンブル性高いので可能ならば避けたい
  - 学習済みモデルが沢山公開されて転移学習で楽するみたいな流れが TensorFlow でももっと進んでくれれば嬉しい
    + Keras はその辺りそこそこまとまっている印象: https://keras.io/applications/
    + Chainer も Caffe のモデルをある程度読み込めるらしい？
  - こんな感じのサンプルコード集もある
    + https://github.com/aymericdamien/TensorFlow-Examples

## TensorFlow で提供されている既存の学習済みモデル

* 何となく雑多に公開されている感じ: https://github.com/tensorflow/models

### Inception

* 提供されているけど何故か wight や bias が全て `Variable` ではなく `constant` になっていた気がする
  - 転移学習で使うには不便だしデモ用っぽい？
  - 学習させたときは当然 `Variable` だったはずなのに、何故 `constant` に変換して保存してしまったのか
  - 保存したグラフが公開されているだけなので、グラフを構築するコードが含まれていないの悲しい

### VGG 16

* TF-Slim に含まれているが TF-Slim 自体 `tf.contrib.layers` とぶつかっているし、ちゃんと残るのかという不安がある

## 高レベルな API と低レベルな API

* 高レベルな API はまだまだ変更が入りそうなのでユーザー的には何を使えば良いかわからないところがある
  - Keras が取り込まれる予定だけど `tf.contrib.layers` とか TF-Slim とかとぶつかるよね
  - `tf.contrib.learn.RNNRegressor` とか前はあったけど何故か無くなったらしい？
* 行列から自分で定義する書き方は流石に大きく変更されることが無さそうで安心ではある

## ローカルと Cloud ML でコードを書き換えずに済ますには？
[@shuhei_fujiwara](https://twitter.com/shuhei_fujiwara) はこんな感じでやっているという一例

* Cloud ML 上で分散処理できるように書いておいて、ローカルでは嘘のクラスタ構成を渡す

```python
# Get environment variable for Cloud ML
tf_conf = json.loads(os.environ.get("TF_CONFIG", "{}"))
# For local
if not tf_conf:
    tf_conf = {
      "cluster": {"master": ["localhost:2222"]},
      "task": {"index": 0, "type": "master"}
}
```

* Google の人々はそもそもローカルで走らせることが無いので気にしていないのでは説

## TensorFlow でモデルを作るときクラスを作る？

* ニューラルネットのモデルに対応するクラスを作る人もいれば関数だけで済ます人もいる
  - [TF-Slim の VGG 16](https://github.com/tensorflow/models/blob/master/slim/nets/vgg.py#L125) なんかは関数だけ
* Chainer の場合はチュートリアルでも基本的にクラスを作ってるよね
* クラスを作ったとして何の情報を持たせておくか微妙
  - Google 側からこれ使えっていうスーパークラスの実装が出ればあるいは？
* まあいずれにせよベストプラクティスは無いのでデザインパターンっぽいものになりそう

## 学習済みモデルの読み込み

* ファイル側に存在しない `Variable` が含まれるグラフ上で restore しようとするとエラーを吐く
  - 回避するためには `tf.train.Saver` に restore する `Variable` のリストを明示的に渡す必要がある
  - `Variable` の定義が高レベルの API で隠蔽されている場合、結構面倒くさい
  - 既存モデルのグラフの上流に `Variable` を追加したい場合とかつらい
    + 画風変換のアルゴリズムとかが実際にそうなる例    
* restore するときに存在しないものは無視するオプションがあれば解決するのでは
  - 書いて PR 送れば良いんじゃね！？
  - 追加の `Variable` が無い状態で restore --> その後名前だけ合わせたダミーの `Variable` を作って save し直す --> 本来作りたかったグラフを作って restore し直すという荒業
    + さすがにやりたくない

## その他

### Cloud ML で立ち上がるクラスタの構成

* 料金体系から察するに STANDARD_1 とか BASIC とかの設定毎でノード数は固定されているっぽい
* Parameter server とか worker の個数が固定されているかは不明だが、多分固定されている気がする