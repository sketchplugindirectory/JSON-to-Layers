# JSON to Layers

![JSON to Layers HERO](http://creative-tweet.net/img/github/json-to-layers-hero.png)

Fireworks PNGの構造をJSONファイルとして書き出し、Sketch（ver.41）へインポートする機能拡張およびプラグインです。

動画: [Fireworks to Sketch — QuickCast.](http://quick.as/pk7yuzz8b)

**古いバージョンをお使い方**
- [Sketch 3.8](https://github.com/littlebusters/JSON-to-Layers/archive/forSketch3.8.zip)
- [Sketch 39-40](https://github.com/littlebusters/JSON-to-Layers/archive/forSketch39.zip)

## インストール

[ZIPファイルをダウンロード](https://github.com/littlebusters/JSON-to-Layers/archive/master.zip)・伸張し、JSON to Layers.sketchpluginをダブルクリックでインストールしてください。

このプラグインを有効活用するには、Fireworksへ"[Fw to JSON](https://github.com/littlebusters/Fw-to-JSON)"コマンドをインストールしてください。

## 使い方

1. Sketchで新規ドキュメントを作成します。
1. プラグインを実行すると、JSONファイルを選択するようにダイアログが表示されるので、Fw to JSONコマンドで書き出したJSONファイルを選択します。
1. 変換が始まります。JSONファイルが大きいと、時間がかかり固まったように見えるため、少し待ってみてください。

## JSONからSketchへの読み込み・変換

### ページとステート

アートボードとして変換し、カンバスへ水平に並べます。ページ共有やマスターページ機能は無視します（内容自体は変換します）。

ステートはカンバスへ垂直に並べます。

### 長方形

長方形ツールで作成したオブジェクトを変形していない場合、SketchでもRectangleレイヤーとして作成します。変形している場合は、ベジェのオブジェクトとして作成します。

### 長方形以外のシェイプ

ベジェオブジェクトとして作成します。

### レイヤーおよびサブレイヤー

レイヤーおよびサブレイヤーは、Sketchのグループとして作成します。レイヤーが元になったグループでは、"Click-through when selecting"を有効化します。

### 「エッジをぼかす」（塗り・線）

Fireworksの「エッジをぼかす」は変換されません。

### グラデーション

直線はLinear Gradientとして、円形・楕円はRadial Gradientとして、円錐はAngular Gradientに変換します。ただし、Sketch上でAngular Gradientの中心を変更できないため、円錐に関しては完全に変換できていません。また、それ以外は直線に変換します。

### パターン

パターンを適用した状態の形状をビットマップとして書き出し、SketchのPattern Fillとして適用します。元のパターンファイルは書き出ししないため、必要に応じて個別に書き出してください。

### Stroke

変換される項目は次の通りです。

- 線幅
- ストロークの整列位置
- 角丸
- 破線
- チップの形状（角 or 丸）

つまり線は「基本→エッジが堅い線（角）」または「基本→エッジが堅い線（丸）」以外は変換できません。「基本→エッジが堅い線（角）」相当でBorderを適用します。

Fireworksでは破線の設定を線分と間隔の組み合わせを3つまで設定できますが、Sketchでは2つまでしか設定できないため、3つめの設定は破棄します。

### ブレンドモード

Sketchで適用できるブレンドモードのみ変換します。Sketchにない場合は、Normalを適用します。

### フィルター

次のフィルターは変換しません。

- カラーを調整
  - カーブ
  - レベル補正
  - 反転
  - 明るさ・コントラスト
  - 自動レベル補正
  - 色相・彩度
- ベベルとエンボス
- ぼかし
  - ぼかし
  - ぼかし（強）
  - ぼかし（放射状）
- その他
- シャープ
- Photoshop ライブエフェクト
  - ベベルとエンボス
  - サテン
  - パターンオーバーレイ

### テキスト

内部的な処理が異なるため、位置や行間などがずれます。

### Symbol

シンボルはSymbolとして変換します。

シンボルインスタンスをFireworks上で変形している場合、異なるSymbolとして作成します。これはSketchのSymbolが、インスタンスの変形に対応していないためです。

### オートシェイプ

通常のパスとして生成します。

### テクスチャー

内蔵テクスチャーは、ビットマップとして書き出しを行い、SketchのPattern Fillとして適用します。

ユーザが独自に適用しているテクスチャーは、元にあった場所にファイルが存在すれば、書き出しを行い内蔵テクスチャーと同様に処理を行います。テクスチャーファイルが存在しなかった場合は、レイヤー名に「 [texture not found]」と追加します。

### ビットマップによるマスク

Sketchではビットマップをマスクとして使用できません。そのため、ビットマップと同じ大きさのRectangleを作成し、マスクとして使用します。

ビットマップが必要であれば手動で配置し、ブレンドモードなどを用いて再現してください。

## バグ報告

動作しないなどバグかなと思ったら、次のステップでissueを立ててください。

1. `/Applications/Utilities/`にある、コンソール.appを開きます。
1. 右上のフィルターへ "Sketch Plugin" と入力します。
1. プラグインを実行してください。
1. エラーメッセージとお使いのSketchのバージョンをissuesへ送ってください。

## Lisence

MITライセンスです。詳しくは、LICENSEをご確認ください。