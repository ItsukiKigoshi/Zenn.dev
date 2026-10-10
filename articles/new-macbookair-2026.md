---
title: "新しいMacBook Airのセットアップ備忘録"
emoji: "🦎"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [mac,macbookair]
published: true
---
![New MacBook Air](/images/new-macbookair-2026/air.webp)
*MacBook Air; 名前に反してあまり軽くない*
## 新しいMacBook Airを買いました
### 愛しきFedora on Macbook Pro
私はメインのコンピュータとしてMacBook Pro (Mid 2014)にFedoraを入れたものを使っており，スリープからの復帰が若干遅い，画面に線が入っている，ヒンジが壊れて画面が自立してくれないなどの問題点を抱えつつも日常的に快適に利用していました．
https://zenn.dev/itsukikigoshi/articles/fedora-macbook

### フラストレーション
しかし，このたび3ヶ月超に及ぶ山小屋生活から帰京後に大学のWPA Enterprise認証を必要とするWi-Fiに接続を試みたところBroadcomのwlというドライバと7系のLinuxカーネルの間で同規格のWi-Fiへの接続にバグがあるのかどうやっても接続できず，とてもフラストレーションがたまりました，
そもそもFedoraは最新のカーネルやパッケージに追従する点でCoolですが，Broadcom-wlのようにカーネルに同梱されていないドライバ類は最新のカーネルに対応していないことが多く，Fedoraのアップデートのたびにビルドエラーでパソコンが起動しなくなる/Wi-Fiに接続できなくなるという事象が数ヶ月に一度のペースで起きていました，

### Wi-Fiワークアラウンド
ドングル（Wi-Fi子機）の購入も検討し，実際に一つ買ってみましたが，Wi-FiチップがLinuxカーネルに同梱されているドライバで動作するものなのか判断するのはなかなか難しく，また子機本体がUSBマウスのレシーバほどの小ささであれば耐えられますが，長い棒を立てるタイプは不格好だし持って行き忘れそうなので，それでもストレスがたまりそうでした，

### 買ったもの
FedoraとGNOMEの組み合わせはCoolでmacOSのMissionControl（開いているウィンドウ一覧）とLaunchpad（アプリ一覧）にあたる機能が三本指スワイプでシームレスにデスクトップと繋がっているシンプルなデザイン哲学やdnfによる一括したパッケージ管理など，今でも使えるなら使いたいのですが，もうここらが買い換え時だろうと判断したので，今日Apple Storeの店頭で **MacBook Air (Apple M5; 16GB Memory; 512GB Storage; US Keyboard)** モデルを学生価格（¥206,800）で購入しました．LenovoでFedoraを使うことへの憧れもあり検討しましたが，プリインストールでUNIXライクなOS(macOS)が入っていて，何より筐体のデザインが美しいMacBook Airが20万円で買えるのに，同等かそれ以上の額を出してCopilotキー付きでFedoraとの相性もわからない（Wi-FiチップがドライバなしでもLinuxカーネル/NetworkManagerに認識されるのか？）Lenovoを買うのには気が引けてこのような選択をしてしまいました．MacBook Airは安直な選択でちょっと悲しい．でもきっと他（Framework with Fedora, Lenovo with Fedora）などと比べてサポートやデバイスの強度が一番確からしいであろうから良いとするのだ．

## 本題: MacBook Airセットアップ備忘録
というわけで実際に行ったセットアップをまとめます．半分は将来の自分のため．

### パッケージマネージャ
- [Homebrew](https://brew.sh/)
  - `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`

Fedoraでdnf（パッケージマネージャ）経由でソフトウェアを管理することにすっかり慣れきってしまったので，なるべく.dmgを使ったマニュアルインストールは避けたいところです．

### 日本語入力
- [ATOK](https://www.atok.com/)
  - `brew install --cask atok`
  - Linuxでネットワークの次にフラストレーションが溜まった項目が日本語入力でした，おかえりATOK!

### ブラウザ
- [Firefox](https://www.firefox.com/)
  - `brew install --cask firefox`
  - 最近月300円と少額ですがMozilla Foundationに寄付を始めました．Chrome以外の選択肢をくれてありがとう，Gecko/SpiderMonkey!

### エディタ
- [Zed](https://zed.dev/)
  -  `brew install --cask zed`
  - シンプルな見た目と軽快な動作はどのエディタにも負けない魅力があると思います．

### パスワードマネージャ
- [Bitwarden](https://bitwarden.com/)
  - `brew install --cask bitwarden`
  - Firefox Extensionの設定も忘れずに．
  - SSH Agentを使う場合はそのPATHも通しておきましょう．
    - `echo 'export SSH_AUTH_SOCK=~/.bitwarden-ssh-agent.sock' >> ~/.zshrc`
    - `source ~/.zshrc`


### Web開発
- [Bun](https://bun.com/)
  - `brew install oven-sh/bun/bun`

### その他ユーティリティ系
- [AltTab](https://alt-tab.app/)
  - `brew install --cask alt-tab`
  - ⌘+Tabの挙動を修正し，ウィンドウ単位でアプリケーションの切り替えができるようにするものです．Macの⌘+Tabはシンプルすぎるのでこれがあると便利
- [Rectangle](https://rectangleapp.com/)
  - `brew install --cask rectangle`
  - ショートカットでウィンドウの右寄せ，左寄せ，全画面等を切り替えるために必要です．
このあたりはGNOMEであればデフォルトの設定で出来たものがmacOSではこのようにバックグラウンドでいくつものアプリケーションを立ち上げておかなければなりません:(
GNOMEが恋しいです...いつかこいつもmacOSのアップデートが止まったらAsahiLinux+Fedora化してやります．

- [AppCleaner](https://freemacsoft.net/appcleaner/)
  - `brew install --cask appcleaner`
  - .appを消すときにシステム内の関連ファイルまで消してくれるアプリです．Homebrewでソフトウェアを管理するようになってもこのソフトウェアが必要かは不明です．

## 変化
正直前のFedora on MacBook Proに概ね満足したのでこの新しいMacBook Airで変化はあまり感じません．使うアプリケーションも変化はほとんどありません．
あえて変わったことを挙げるならば以下のようなところでしょうか．
### ポジティブ👍
- Touch IDが使えるようになった
- とても静か！（ファンレス）
- バッテリー持ちがとても良い
### ネガティブ👎
- リンゴが光らない😭
- 大西配列が使えない（組み替える予定は今のところないがQWERTYはとても使いにくい）

といったところでしょうか．

正直一番使うのがFirefoxでのネットサーフィンで，次がZedでのコーディングでしょうから，マシンパワーを使う場面が少ないのです．少なくとも何か映像を再生しながらコーディングするときに以前のように動画が途切れ途切れにならないようになったのは良い変化かもしれません．

あと10年はこのマシンと一緒に過ごせるように大切に使用したいと思います．

みなさまお元気で，
木越 斎

---
*本記事の執筆に当たり，以下の箇所に生成AIを使用しました:
- Bitwarden SSH AgentのPATHを通す際の作業をechoで行う方法の検索