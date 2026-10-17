---
title: "MacBook Air (2026)を大西配列化する（Karabinar-Elements on macOS 27）"
emoji: "👋"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [大西配列, macos, karabinerelements]
published: false
---
## 動機
こちらの記事に書いたとおり，最近私は12年もののMacBook Pro (Mid 2014) with Fedora LinuxからMacBook Air (M5, 2026)へ乗り換えました．
https://zenn.dev/itsukikigoshi/articles/new-macbookair-2026

以前のMacBook ProではLinuxのキー配置変換ツール「[keyd](https://github.com/rvaiya/keyd)」で[大西配列](https://o24.works/layout/)を実現していましたが，このたびmacOSに移行したことで別の方法で大西配列を設定する必要が出てきました．

ちなみに，MacBook Air購入後にQWERTY配列をしばらく試したのですが，キーボード上で手を動かす距離が長くとても疲れてしまったので，出来れば新品のMacでキーを壊すリスクを冒したくない（Macのキーは繊細なので外し方を間違えると爪が折れて使えなくなります，おそらくAmazonやiFixitでキーだけ入手可能だけどね）のですが，QWERTYのストレスには耐えられず止むなく大西配列を取り戻すことにしました．

そこで，キーボードを物理的に配置換えした上で，[大西配列公式の導入手順](https://o24.works/layout/#:~:text=%E3%81%93%E3%81%A1%E3%82%89%E3%80%82-,%E5%B0%8E%E5%85%A5%E6%96%B9%E6%B3%95)にもあるKarabinar-Elementsを用いたキー配置リマップを行います．


## 導入手順
*ここからの手順を再現する際は自己責任でお願いします．
### 1. キー配置を考える
ベースとなる大西配列を基に，自身のキーボードや普段の作業内容に合わせてキー配置を考えます．
特に記号キーは人により好みが分かれると思います．
私はUSキーボードモデルを買ったので前回のJISベースに比べて全体的にキー数が少なく記号の配置に迷いました．

以下が主なこだわりです:
- 私は **\[** (open blacket)と **\]** (close blacket)をよく使用するのでその場所が左右に並ぶようにした
- Deleteが右下の押しやすい位置に来るようにした
- fn+Delete（後方文字削除）が片手で操作できるようにした．
  - BackSpace/Deleteに関しては，もう少し検討の余地がありそう
- かな/英数キーを新設し左右に振り分けた
  - JISキーボードだともう少し設定しやすいのですが，今回JISモデルのMacとUSキートップを買ってキーを入れ替えるような手間をかけるつもりはなかったので，USキートップ印刷面のシンプルさを優先したことによるトレードオフとしてかな/英数キーが打ちにくいことは許容します．
### 2. キーの物理的な再配置
#### a. キーを剥がす
まず，キーを剥がします．今回は新品なので必要ありませんが，剥がしたついでに綿棒やエアダスターで掃除をすると良いでしょう．
![Keys Removed](/images/o24-macbookair/removed.webp)
*キーボードを剥がした様子*

こちらのYouTube動画が参考になります．
https://www.youtube.com/watch?v=8dB-vNBXEFQ

基本方針としては，
1. キーの下側からトランプカードほどの少し堅く薄いものを挿入し，キー下半分でロックしている2つの爪を外す
2. キー上部を押さえて持ち上げて外す

という流れです．
このとき，無理に剥がそうとするとこれらの爪が折れて，キーが浮いたり固定されない原因になります．爪が折れるとキーの買い換え以外に選択肢がなくなりとても悲しいので気をつけましょう．

![Removed Keys](/images/o24-macbookair/keys.webp)
*剥がしたキーたち．無くさないようにしよう．*

#### b. キーをセットする
ステップ1で検討したキー配置に基づきキーを並べ，上記手順を逆に行います．

![Completed](/images/o24-macbookair/completed.webp)
*最終的な配置．使いながら少しずつ使いやすいように配置を変更しています*

### 3. ソフトウェアの設定
まず，Karabinar-Elementsがバックグラウンドで動作するようにソフトウェア内「Setup」にしたがってmacOSの権限を与えます．

![Setup](/images/o24-macbookair/setup.webp)

次に，Karabinar-Elementsの「Simple Modifications」から，対応するキーをポチポチ一つ一つ押してキー配置を設定します．

![Simple Modification](/images/o24-macbookair/device.webp)


また，Maintenance --> Misc --> "Copy the current configuration on the system default configuration"を設定してあげることで，Karabinar-Elementsが常駐していなくても，たとえばログイン画面などでも安定的にこの配列が使えるようになります．とても安定して良いです．

![System Default](/images/o24-macbookair/system-default.webp)

ちなみにLinux Keydの場合はほとんどそのままこの設定がテキストファイルで行えるのですが，Karabinar-ElementsではJSONで設定ファイルが管理されているためそのファイルを直接編集することは可読性の観点や構文エラーのリスクからあまりおすすめできません．面倒です．

完成したファイルがこちらです．大西配列だけではなく，F5とF6にキーボードバックライト調整を割り当てる変更などが含まれています．JSONだからそうした意図もコメントアウトに残せず不便です．

@[gist](https://gist.github.com/ItsukiKigoshi/99a7b8d2c9296afa88514f73bc5f8a85)

## 導入後

もともと大西配列を利用していたこともあり，タイピング操作に不便な点はありません．
速度もQWERTYで極めていたときにはまだ及びませんが日常のタイピングに支障は無く，また打ち心地は最高です．
もう半年以上大西配列を使用していますが，QWERTYに戻りたいと思う理由も特になく，これからもこの配列でコーディングや大学の課題を行いたいと思っています．

![Result](/images/o24-macbookair/res.webp)
*大西配列における最新の[e-typing](https://www.e-typing.ne.jp)の結果．これだけ打てれば日常利用に支障はないだろう．*

ありがとうございます，大西さん！

2026/10/17
**木越 斎**

--
![Boy and Hay](/images/o24-macbookair/boy-and-hay.webp)
*干し草と少年; 記事と無関係のスナップ写真*