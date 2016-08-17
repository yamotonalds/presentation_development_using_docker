% Dockerで開発したい
% yamotonalds
% 2016-08-17

#

## 新しいプロジェクトに参加

開発環境を構築する必要がある

前のプロジェクトの開発環境も維持

## 開発環境構築のつらみ

- 環境構築方法が口伝
- wikiに書いてあるけど内容が古い

. . .

構築してみたらMySQLにdatabaseが数十個できた…

## 

Docker使おう٩( 'ω' )و 

# メリット(ﾟ∀ﾟ )

## すぐに動く

<img src="images/ready.jpg" height="250px" />

ちゃんと作られてればほぼ1コマンドで動くはず

## 環境構築に何が必要なのかわかりやすい

<img src="images/wakaru.jpg" height="250px" />

Dockerfileやdocker-compose.ymlに書いてある

## おかしくなったら簡単に最初からやり直せる

<img src="images/restart.jpg" height="250px" />

コンテナは使い捨て

## 複数プロジェクトを共存させやすい

<img src="images/kyozon.jpg" height="250px" />

片方の環境構築したらもう片方が動かなくなるとか困る(´・ω・｀)

# デメリット('A`)

## コマンドが長い

<img src="images/long.jpg" height="250px" />

```
dcoker-compose run --rm servicename rails c
```

pecoがあればコマンド履歴で大丈夫

## ポート番号が変わる

<img src="images/kawaru.jpg" height="250px" />

自動的に空いてるポートを割り当てるのでコンテナを立ち上げる度にポート番号が変わる

`docker exec` やPCのスリープでは変わらない

固定もできるけど複数のプロジェクトでかち合うのは嫌

## save_and_open_page が使えない

saveはできるからホスト側から開けば見える

通知とかホスト側と連携してるやつと相性が悪い

## Macの人

Docker for Macだとボリュームマウントしたディレクトリのパフォーマンスが悪い

[https://docs.docker.com/docker-for-mac/troubleshoot/#known-issues](https://docs.docker.com/docker-for-mac/troubleshoot/#known-issues)

## unison

双方向ファイル監視同期

ボリュームマウントしたディレクトリで動かさずに専用のディレクトリで動かして同期する

双方向なのでrails gとかで生成されたファイルもホスト側に反映される

## unisonの問題点

- 同期する分だけコンテナ起動に時間がかかる
    - bundle installしたgemのコードまで同期するとヤバい
        - gem追加時はbuild
- 編集が競合すると変更が反映されない
- コンテナ側の意図しないファイルがローカルに入ってくることがある

# おわりに

##

より良い開発環境になってきてはいる気がする

DBやredisだけとか部分的に始めるもの良いかも
