# dtdl_json
dtdl_json

#　これは完全に自分用メモ

DTDLの仕様
https://learn.microsoft.com/ja-jp/azure/digital-twins/concepts-models

テスト定義書→テスト用JSONファイル
https://github.com/takuoki/testmtx/blob/main/README.md
https://medium.com/veltra-engineering/a-tool-to-generate-test-json-files-from-a-test-definition-sheets-c36b77ab886f

testmtx_sample のコピーしてsample.xlsxとしてローカルに置く・・・[手順1]
https://docs.google.com/spreadsheets/d/1BhE4zmjB9cTZFP3Bl2A5ZQjLfeDtAhrOjBbQBt7vqKo/edit#gid=0

credentials.jsonの作成・・・[手順2]
GCPコンソール
https://console.cloud.google.com/home/dashboard
[APIとサービス] - [認証情報]でOAuth同意画面の設定とOAuthクライアントIDの作成
https://blog.serverworks.co.jp/2021/01/08/130956
一応作成したけど、いらないかも？認証時にGoogleログインを1回したけど、社内ルールではダメだと思う

--**---
クライアント ID	keepメモ参照
クライアント シークレット	keepメモ参照
作成日	2024年3月16日 11:29:17 GMT+9
--**--

(1) WindowsにGo言語開発環境をインストールする
https://qiita.com/suke_masa/items/0c45c92934b9a2807ddb

*C:\Goにインストールすること

(2) コマンドプロンプトで go version コマンドを実行してください。インストールしたGoのバージョンが表示されれば成功です。

Visual Studio Codeの導入
https://qiita.com/suke_masa/items/91fddf0728a290b72fc4

(3) Visual Studio CodeのGo Extension
拡張機能(Ctrl+Shift+X)
https://qiita.com/melty_go/items/c977ba594efcffc8b567
(4) Extensionの検索画面を開いて「go」で検索→[Go Team at Google]のGoエクステンションをInstallしてください。

(5) [View]-[Command Palette]（またはCtrl+Shift+P）でコマンドパレットを開いてください。
(6) コマンドパレットに「go update」と入力すると、[Go: Install/Update Tools]という項目が出てくるので、これをクリックしてください。
 [gocode]・[gopkgs]にチェック（出ないときは下記の２つを実施）

 ・Goの環境構築からHello Worldまで
 https://zenn.dev/collabostyle/articles/762a357f01201e
 ・ターミナルに入力するコマンド
 https://github.com/qt-luigi/vscode-go-docs-jp

*gocode: go get -u -v github.com/nsf/gocode
godef: go get -u -v github.com/rogpeppe/godef
gogetdoc: go get -u -v github.com/zmb3/gogetdoc
golint: go get -u -v github.com/golang/lint/golint
go-outline: go get -u -v github.com/lukehoban/go-outline
goreturns: go get -u -v sourcegraph.com/sqs/goreturns
gorename: go get -u -v golang.org/x/tools/cmd/gorename
*gopkgs: go get -u -v github.com/tpng/gopkgs
go-symbols: go get -u -v github.com/newhook/go-symbols
guru: go get -u -v golang.org/x/tools/cmd/guru
gotests: go get -u -v github.com/cweill/gotests/...

(7) testmtx
https://github.com/takuoki/testmtx?tab=readme-ov-file
インストール
Go 環境がある場合は、 を使用してこのツールをインストールできますgo get。インストールする前に、Go モジュール機能を有効にしてください。

go install github.com/takuoki/testmtx/tools/testmtx@v1.1.1
そうでない場合は、リリース ページからダウンロードしてください。
https://github.com/takuoki/testmtx/releases

(8) Googleスプレッドシートを使用する場合
このツールはGoogle OAuth2.0を使用しています。したがって、ツールを実行する前に、 credentials.jsonを準備する必要があります

テストデータファイルの出力
1. テストケースを作成する
サンプル シートをコピーし、必要に応じて記入します。Microsoft Excelを使用する場合は、同じ形式でシートを作成してください。

C:\Go\testmtx-1.1.1にダウンロードしてきたリソースを展開しておく
ここまで来たら、C:\Go\go-appも存在するはず

>設定ファイル
構成ファイルを使用していくつかの追加機能を使用できます。これらの機能を使用する場合は、コマンドライン引数として設定ファイルを指定します。
config.jsonがsampleフォルダにあること
"C:\Go\testmtx-1.1.1\sample\config.json"

ターミナルで次の入力をする
$ testmtx -c config.json conf

>以下のようなテスト データの Go タイプがすでにある場合は、このツールを使用してプロパティ リストを生成できます。
sample.goがsampleフォルダにあること
"C:\Go\testmtx-1.1.1\sample\sample.go"

ターミナルで次の入力をする
testmtx prop -f sample/sample.go -t Request

>2. コマンドを実行する
サブコマンドを使用するとout、シートでテストデータを生成できます

ケース: Microsoft Excel
$ testmtx -c config.json out -x sample.xlsx

*config.jsonとsample.xlsxがC:\Go\testmtx-1.1.1\sampleに入っていないと動かない
