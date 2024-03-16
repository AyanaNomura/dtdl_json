# dtdl_json
dtdl_json

#　これは完全に自分用メモ

DTDLの仕様
<p>https://learn.microsoft.com/ja-jp/azure/digital-twins/concepts-models</p>

テスト定義書→テスト用JSONファイル
<p>https://github.com/takuoki/testmtx/blob/main/README.md</p>
<p>https://medium.com/veltra-engineering/a-tool-to-generate-test-json-files-from-a-test-definition-sheets-c36b77ab886f</p>

testmtx_sample のコピーしてsample.xlsxとしてローカルに置く・・・[手順1]
<p>https://docs.google.com/spreadsheets/d/1BhE4zmjB9cTZFP3Bl2A5ZQjLfeDtAhrOjBbQBt7vqKo/edit#gid=0</p>

<p>credentials.jsonの作成・・・[手順2]</p>
GCPコンソール
<p>https://console.cloud.google.com/home/dashboard</p>
<p>[APIとサービス] - [認証情報]でOAuth同意画面の設定とOAuthクライアントIDの作成</p>
<p>https://blog.serverworks.co.jp/2021/01/08/130956</p>
<p>一応作成したけど、いらないかも？認証時にGoogleログインを1回したけど、社内ルールではダメだと思う</p>

--**---
<p>クライアント ID	keepメモ参照</p>
<p>クライアント シークレット	keepメモ参照</p>
<p>作成日	2024年3月16日 11:29:17 GMT+9</p>
--**--

(1) WindowsにGo言語開発環境をインストールする
<p>https://qiita.com/suke_masa/items/0c45c92934b9a2807ddb</p>

*C:\Goにインストールすること

(2) コマンドプロンプトで go version コマンドを実行してください。インストールしたGoのバージョンが表示されれば成功です。

Visual Studio Codeの導入
<p>https://qiita.com/suke_masa/items/91fddf0728a290b72fc4</p>

(3) Visual Studio CodeのGo Extension
拡張機能(Ctrl+Shift+X)
<p>https://qiita.com/melty_go/items/c977ba594efcffc8b567</p>
(4) Extensionの検索画面を開いて「go」で検索→[Go Team at Google]のGoエクステンションをInstallしてください。

(5) [View]-[Command Palette]（またはCtrl+Shift+P）でコマンドパレットを開いてください。
(6) コマンドパレットに「go update」と入力すると、[Go: Install/Update Tools]という項目が出てくるので、これをクリックしてください。
<p> [gocode]・[gopkgs]にチェック（出ないときは下記の２つを実施）</p>

 ・Goの環境構築からHello Worldまで
 <p>https://zenn.dev/collabostyle/articles/762a357f01201e</p>
 ・ターミナルに入力するコマンド
 <p>https://github.com/qt-luigi/vscode-go-docs-jp</p>

<p>*gocode: go get -u -v github.com/nsf/gocode</p>
<p>godef: go get -u -v github.com/rogpeppe/godef</p>
<p>gogetdoc: go get -u -v github.com/zmb3/gogetdoc</p>
<p>golint: go get -u -v github.com/golang/lint/golint</p>
<p>go-outline: go get -u -v github.com/lukehoban/go-outline</p>
<p>goreturns: go get -u -v sourcegraph.com/sqs/goreturns</p>
<p>gorename: go get -u -v golang.org/x/tools/cmd/gorename</p>
<p>*gopkgs: go get -u -v github.com/tpng/gopkgs</p>
<p>go-symbols: go get -u -v github.com/newhook/go-symbols</p>
<p>guru: go get -u -v golang.org/x/tools/cmd/guru</p>
<p>gotests: go get -u -v github.com/cweill/gotests/...</p>

(7) testmtx
<p>https://github.com/takuoki/testmtx?tab=readme-ov-file</p>
インストール
<p>Go 環境がある場合は、 を使用してこのツールをインストールできますgo get。インストールする前に、Go モジュール機能を有効にしてください。</p>

<p>go install github.com/takuoki/testmtx/tools/testmtx@v1.1.1</p>
そうでない場合は、リリース ページからダウンロードしてください。
<p>https://github.com/takuoki/testmtx/releases</p>

(8) Googleスプレッドシートを使用する場合
<p>このツールはGoogle OAuth2.0を使用しています。したがって、ツールを実行する前に、 credentials.jsonを準備する必要があります</p>

テストデータファイルの出力
1. テストケースを作成する
<p>サンプル シートをコピーし、必要に応じて記入します。Microsoft Excelを使用する場合は、同じ形式でシートを作成してください。</p>

<p>C:\Go\testmtx-1.1.1にダウンロードしてきたリソースを展開しておく</p>
ここまで来たら、"C:\Go\go-app"も存在するはず

>設定ファイル
<p>構成ファイルを使用していくつかの追加機能を使用できます。これらの機能を使用する場合は、コマンドライン引数として設定ファイルを指定します。</p>
config.jsonがsampleフォルダにあること
<p>"C:\Go\testmtx-1.1.1\sample\config.json"</p>

ターミナルで次の入力をする
<p>$ testmtx -c config.json conf</p>

>以下のようなテスト データの Go タイプがすでにある場合は、このツールを使用してプロパティ リストを生成できます。
sample.goがsampleフォルダにあること
<p>"C:\Go\testmtx-1.1.1\sample\sample.go"</p>

ターミナルで次の入力をする
<p>testmtx prop -f sample/sample.go -t Request</p>

>2. コマンドを実行する
サブコマンドを使用するとout、シートでテストデータを生成できます

ケース: Microsoft Excel
<p>$ testmtx -c config.json out -x sample.xlsx</p>

<p>*config.jsonとsample.xlsxがC:\Go\testmtx-1.1.1\sampleに入っていないと動かない</p>

