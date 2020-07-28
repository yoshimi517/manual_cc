## 製品マニュアルを執筆環境構築手順
環境構築資材は、下記パスに保存してあります。  
`\\ami-central\Units\E10_CTI事業部\開発\開発管理\共有ドキュメント\製品マニュアル執筆環境構築資材`  

### atom 環境を整える

**不明点は、中道さん、坂巻さんに聞いてください。**  

1. atom をインストールする  
atom は不具合が多いので安定版を使ってください。こちらで確認できている安定版は  
    - 1.44（AtomSetup_1.44-x64.exe）  
    - 1.46（AtomSetup_1.46-x64.exe）  

    です。
    <br />
    独自に準備したい方は [atom のホームページ](https://atom.io) を確認してください。  

1. github にアカウントを作る  
[github のホームページ](https://github.com/) に行き、サインアップしてください。  
その後、メールアドレスに github からメールがくるので Verify してください。  

1. git をインストールする  
インストーラは ↓ です。  
    - Git-2.27.0-64-bit.exe  

    独自に準備したい方は [git のホームページ](https://gitforwindows.org/)

1. git のセットアップ  
プログラムメニューから git bash 起動して、以下のコマンドを実行してください。  

    ```
    git config --global user.name "登録したユーザ"
    git config --global user.email "登録したメアド"
    ```
1. atom 設定を同期する  
    1. メニューバー → ファイル → settings → install → 検索テキストボックスに sync-settings と入力してください。  
    1. sync-settings というパッケージが表示されるので、その install ボタンをクリックしてください。
    1. sync-settings パッケージを設定します。  
画面右上に変な赤いダイアログが表示されたら消して大丈夫です。  
    1. atom  の 設定画面の Package に移動して以下を実行してください。  
       - sync-settings の setting ボタンを押すと下に設定欄が表示されますので、  
         - Personal Access Token = 7efd6c692a7186b2d4b35d2e887a255b2b4fdfc3  
         - gist-id = a4b627dbe1ddbdc7efd59de9b1713109  

        を入力してください。  

    1. メニューバーの パッケージ → Synchronized settings → restore を選択してください。  
       - ダイアログが表示されるので、新規作成的なリンクをクリックしてください。
       - Web ページが立ち上がります。
       - description に適当に文字を入力してください。
       - gist にチェックをしてください。（多分デフォルトでチェック済みのはず。。）
       - generate ボタンを押します → 画面遷移 → コードをコピーしてください。
       - atom に戻ります → Access コードを入力する的なボタンをクリックしてください。
       - ダイアログに Web 画面でコピーしたコードをペーストしてエンターキーを押して下さい。
    1. 設定の同期が始まるのでしばらく待ちます。待ってる間に以下に進む。
1. github リポジトリに参加する  
user.name を以下にメールして、メールしたーと教えてください。  

     ```
     y-takagi@advanced-media.co.jp
     k-nakamichi@advanced-media.co.jp
     t-sakamaki@advanced-media.co.jp
     ```  

1. github からメールがくるので you can Accept or decline 的なリンクをクリックしてください。  
ブラウザにて github の画面が表示されるので **Accept** ボタンをクリックしてください。  

1. メニューバー → ファイル → 設定 → パッケージ → 検索テキストボックスに sync-settings と入力してください。  
sync-settings を Disable にしてください。  

### その他ツール編
1. TeXインストーラ 3 で Tex をインストールします。  
.\abtexinst_0_91\abtexinst.exe  
[tex 3 のホームページ？](https://www.ms.u-tokyo.ac.jp/~abenori/soft/bin/abtexinst_0_91.zip)  
  全部 default でインストールしてください。（時間がかかるので昼食前などに！）
1. Pandoc をインストールしてください。  
pandoc-2.9.2.1-windows-x86_64.msi  
[Pnadoc のホームページ](https://pandoc.org/installing.html)  
※ Pnadoc-crossref を最新にする場合には、Pandoc のバージョンも合わせてください。  
1. Pandoc-crossref を配置してください。  
pandoc-crossref.exe  
`C:\Program Files\Pandoc` に pandoc-crossref.exe を配置してください。  
[Pnadoc-crossref ダウンロードページ](https://github.com/lierdakil/pandoc-crossref/releases/)  
※ Pandoc を最新にする場合には、Pandoc-crossref のバージョンも合わせてください。  
1. Graphviz をインストールしてください。  
graphviz-2.38.msi  
“Just me" は "Everyone" に変更してください。  
[Graphviz のホームページ](https://graphviz.gitlab.io/)  
1. Chocolatey をインストールしてください。  
    - PowerShell を管理者権限で起動して、
    ```
    Set-ExecutionPolicy Bypass -Scope Process -Force;[System.Net.ServicePointManager]::SecurityProtocol =[System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
    ```
      を実行します。
1. JDK をインストールしてください。  
PowerShell を管理者権限で起動して、  
`cinst jdk8 -y`  
を実行します。  
1. 環境変数を設定してください。  
環境変数設定のためのシステムプロパティを開くには、  
ファイル名を指定して実行から `%windir%\system32\sysdm.cpl` を実行 → 詳細設定タブ → 環境変数 ボタン  
    - システム環境変数 JAVA_HOME を追加します。  
JAVA_HOME=C:\Program Files\Java\jdk1.8.0_211  
    - システム環境変数 path を修正します。  
path に C:\Program Files\Java\jdk1.8.0_211\bin  
を追加します。  

### GitBook 環境を構築する

1. Node.js をインストールしてください。  
node-v12.18.2-x64.msi  
Node.js もバグが多いので安定版（LTS）必須です。それでも最新だと動かない。。  
インストールの手順は [ココ](https://qiita.com/gisuyama7/items/4c2ef852095d220e312c) の通りに！  
[Node.js ホームページ](https://nodejs.org/ja/)
1. gitbook-cli をインストールしてください。  
PowerShell を管理者権限で起動して、  
`npm install -g gitbook-cli`  
を実行します。  
1. gitbook をインストールしてください。  
Windows の スタートメニュー → プログラム → Node.js → Node.js cmmand prompt を起動して、  
`gitbook help`  
を実行します。  
1. ローカルに作業フォルダを作成する  
例） c:\work\GitBook\manual_cc\
1. atom が起動していたら再起動してください。
1. atom 起動したら、  
パッケージ → コマンドパレット → clone と入力 → Github:Clone が候補表示されるので選択
1. Clone ダイアログで以下を入力してください。  
    - Clone from = https://github.com/ytakagi-ponkotsu/manual_cc  
    - to Directry = 上の 4 で作った作業フォルダ  

      → ログインダイアログが表示されたら、github アカウントでログインする。  
1. atom で メニューバー → 表示 → GitHub タブの切替 をクリックします。  
GitHub タブが atom IDE 上に表示されるので、  
    - ログインボタン が表示されていたらログインボタンを押します。  
    → Accessコードの生成的なものがでたら実施します。（新規クリエイト的な）
    - ブラウザで画面が開くので、生成してコードをコピーします。  
    - atom に戻ってコードを貼り付けます。  

### 動作確認

1. github の動作確認  
    - 画面左に表示されているツリービューから、docs/HELP.md を選択します。  
    - エディタで docs/HELP.md が開くので、一番下の、編集者セクションの番号リストの編集者となっている行を自分の名前で更新して保存します。  
    - Git タブ（**GitHub タブじゃない**）を開くと Unstaged Changes に docs/HELP.md が表示されているので、右クリックから Stage します。  
    - docs/HELP.md が Staged Changes に移動します。
    - Commit message とかかれた黒い欄に、test とか適当な文字を入力して、欄の下の Commit to master という青いボタンをクリックします。  
    - Git タブ上のどこかを右クリック → Git → Pull All します。  
    - Git タブ上のどこかを右クリック → Git → Push All します。  
    - エラーがでなければおｋです。  

1. GitBook の動作確認  
    - atom の パッケージ → platformio-ide-terminal → Toggle をクリックすると、atom 上にコマンドプロンプト的なものが表示されます。  
    - cd で、上で作成した作業フォルダに移動します。  
cd c:\work\GitBook\manual_cc
    - gitbook build を実行します。  
エラーが出て実行出来ない場合、  
コマンドプロンプトを管理者として起動して、  
      ```
      PowerShell Set-ExecutionPolicy RemoteSigned
      ```
を実行します。  
    - gitbook build が成功した場合、エクスプローラで作業フォルダを開きます。  
    - 作業フォルダの直下に `_book` というフォルダが作られます。  

以上で終了です。
