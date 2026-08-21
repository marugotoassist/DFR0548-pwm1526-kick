# DFR0548-pwm1526-kick

DFRobot micro:Driver(DFR0548)用の MakeCode スケッチ雛形。
[marugotoassist/pxt-motor](https://github.com/marugotoassist/pxt-motor)(DFRobot/pxt-motor のフォーク、日本語ブロック付き)を
拡張機能として導入済み。

**PWM 周波数 1526Hz(PCA9685 上限)+ 起動ブースト + 最低速度補正** を「最初だけ」で設定済み。

| ブロック | 設定値 | 意味 |
|---|---:|---|
| `PWM周波数を設定 … Hz` | 1526 | PCA9685 の上限。低速時の脈動・回転ムラを抑える |
| `起動ブーストを設定 デューティ … 時間 …ms` | 200 / 100ms | 停止(または逆転)からの起動時だけ、目標速度より強い 200/255 を 100ms 与えて静止摩擦を越える。目標速度が 200 以上のときは何もしない |
| `最低速度を設定 …` | 150 | 速度 1〜255 を 150〜255 に線形リマップ(デッドバンド補正)。実負荷で回転を維持できる実測値 |

姉妹repo: [DFR0548-pwm50](https://github.com/marugotoassist/DFR0548-pwm50)(既定50Hz)/
[DFR0548-pwm1526](https://github.com/marugotoassist/DFR0548-pwm1526)(1526Hzのみ)

> このページを開く [https://marugotoassist.github.io/DFR0548-pwm1526-kick/](https://marugotoassist.github.io/DFR0548-pwm1526-kick/)

## このプロジェクトを編集します

MakeCode でこのリポジトリを編集します。

* [https://makecode.microbit.org/](https://makecode.microbit.org/) を開く
* **読み込む** をクリックし、 **URLから読み込む...** をクリックしてください
* **https://github.com/marugotoassist/DFR0548-pwm1526-kick** を貼り付けてインポートをクリックしてください

## 注意

* **左右の車輪は `モーター M1 … とモーター M2 …`(デュアルブロック)で指令してください。**
  `モーター` ブロック2個を並べると、ブーストが直列に走って2個目の起動がブースト時間分
  (200ms)遅れ、起動時に車体の向きが変わります。デュアルブロックは左右を同時にブーストします。
* ブーストは「指令を出した瞬間」にしか働きません。走行中に失速しても自動では再ブーストしません
  (回転を検出するセンサーがないため)。
* 同じ PCA9685 をサーボと共用しているため、**この設定では RC サーボは正常動作しない**(サーボは 50Hz 前提)。
* 各値の調整方針は robotcar リポジトリ `2026/pxt-motor-pwmfreq/README.md` の
  「センサー追加なしでの低速改善策」を参照。

## 拡張機能について

`pxt.json` の `motor` 依存は marugotoassist/pxt-motor の特定コミットに固定してある。
フォーク側を更新したら、ハッシュを新しいコミットに差し替えること。

## 関連

* 実験計画: robotcar リポジトリ `2026/pxt-motor-pwmfreq/README.md`
* 参考にした雛形: [scramble-robot/DFR0548-Japanese](https://github.com/scramble-robot/DFR0548-Japanese)
