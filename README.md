 # Crescent-docker
## About
https://github.com/AkashiAkatsuki/Crescent の環境をコンテナにしたものです
postgresサーバとunicornサーバ(本体)、nginxサーバの３つで動いてます

## Usage
gitとdocker、docker-compose(v3が動く1.13以降)の環境を入れておく
```
git clone https://github.com/AkashiAkatsuki/Crescent-docker
cd Crescent-docker
# crescent/config/profile.ymlを自由に編集
# crescent/config/twitter-auth.ymlにTwitterのAPI認証キーを書いておく
docker-compose up -D
docker exec -it Crescent-docker_crescent_1 # コンテナ内シェルに入る

rake db:table # データベースのテーブル初期化用

ruby main.rb # CUIで起動
ruby main.rb -t # Twitterで稼働
bundle exec unicorn -c config/unicorn.rb # unicornサーバを起動
```
モニタリング用のホームページはデフォルトでは http://localhost:81 で確認できます
公開する際はdocker-compose.ymlやweb/nginx.confをいじって良い感じにしてください

### profile.ymlについて

``` crescent/config/profile.yml
name: Sample            #人工無脳の名前
learning_rate: 0.3      # 価値観の変化しやすさ(0~1)
moody_rate: 0.8         # 機嫌値の変化しやすさ(0~1)
max_trends: 100         # 頻出単語判定時の単語のスタック量。長すぎると数時間前の話題を持ってきたりする
max_speak_wait: 10      # TLの人数に合わせて呟く頻度を変える際の最大待ちツイート数
none_reply: Zzz         # 言葉に詰まった時に返すリプライ
love_rate_response: 0.6 # リプによる好感度の変わりやすさ
love_rate_listen: 0.3   # TLのツイートによる好感度の変わりやすさ

# TLで頻出しても反応しない単語を設定。でも文中では平気で使うので注意
ignore_trends:
  - の
  - ん
  - ー

# 価値観パラメータの初期設定用。単語の好き嫌いを設定できる
values:
  - name: 良い
    value: 1
  - name: 悪い
    value: -1
```
