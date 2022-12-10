# Summary
- 教育用コンテンツ（講義使用）
- 手書き文字を認識する。
- 各種概念には立ち入らず、実装をスコープとする。
  - ex. 係数推定値とは、平均二乗誤差とはについては立ち入らない。

# Design
- Notebook作成
  - データの読み込み
    - sklearnのdatasetsモジュールからload_digits関数を呼び出し、返り値を変数（digits）に代入する。
  - データの確認
    - digitsのキーであるimagesの0番目の要素を表示する。
    - 0番目の要素を下記関数を使用して、画像として表示する。
      ```
      def output_fig(image: np.ndarray, label: int) -> None:
          fig = plt.figure(figsize=(3, 3))
          ax = fig.add_subplot(111)
          ax.set_axis_off()
          ax.imshow(image, cmap=plt.cm.gray_r)
          ax.set_title("Training: %i" % label)
          plt.show()
      ```
    - 4枚の画像を下記関数を使用して、表示する。
      ```
      def output_figs(images: np.ndarray, targets: np.ndarray, slices: int) -> None:
          _, axes = plt.subplots(nrows=1, ncols=slices, figsize=(10, 3))
          for ax, image, label in zip(axes, images, targets):
              ax.set_axis_off()
              ax.imshow(image, cmap=plt.cm.gray_r)
              ax.set_title("Training: %i" % label)
      ```
  - データを前処理する。
    - 画像の次元を変換する。
      - 1797枚の8x8という2次元の画像(digits.images)を、1797枚の1次元の画像に変換する。 
  - モデルを作成する。
    - サポートベクターマシンモデル(SVC)を作成する。決定境界を単純にするために、gammaを0.001に設定する。
    - 1次元に変換した画像と、それに対応するラベルをそれぞれX, y、テストサイズ0.5としてデータを分割する。
    - 作成したモデルで学習する。
    - テストデータを使用して、画像の数字を予測しなさい。
  - 学習結果を評価する。
    - output_figsを使用して、予測結果とテストデータの画像を表示する。

# Data
- sklearn.datasets.load_digits()

# Lesson
- Must
  - Designの項目の実装
- Want
  - 関数化
  - テストコード
