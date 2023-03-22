docker-mirakurun-epgstation-recpt1-nvenc
====

----

### ⚠️ 𝑫𝑰𝑺𝑪𝑶𝑵𝑻𝑰𝑵𝑼𝑬𝑫 ⚠️ 

NVENCを使うのをやめたので、このリポジトリのメンテナンスは終了しました  
QSV(VA-API)版は [docker-mirakurun-epgstation-recpt1-vaapi-qsv](https://github.com/mohemohe/docker-mirakurun-epgstation-recpt1-vaapi-qsv) から入手できます

----

[nns779/px4_drv](https://github.com/nns779/px4_drv)で[PX-Q3U4](http://www.plex-net.co.jp/product/px-q3u4/)を[Chinachu/Mirakurun](https://github.com/Chinachu/Mirakurun)+[l3tnun/EPGStation](https://github.com/l3tnun/EPGStation)で動かしつつNVEncでエンコードするための構成

## 準備

- Docker v19.03以降が必要
- Docker Compose v1.28.0以降が必要
- GeforceなどのNvidia系GPUがホストに正しく認識されていること
- ホストに [nns779/px4_drv](https://github.com/nns779/px4_drv) をインストールしておく
- 録画用ディレクトリとしてホストに `/rec`, `/grec` が存在するのを期待しているので、ディレクトリを作成しておく

## clone

以下のリポジトリをsubmoduleに含めています

- [stz2012/libarib25](https://github.com/stz2012/libarib25)
- [stz2012/recpt1](https://github.com/stz2012/recpt1)

```bash
git clone --recursive https://github.com/mohemohe/docker-mirakurun-epgstation-recpt1-nvenc.git
```

## 環境変数

```bash
cp sample.env .env
```

して、 `.env` を書き換えてください  
特に、 `mariadb` の設定は変更を推奨します

## config

以下のファイルのみ同梱しています

- epgstation
    - config
        - config.sample.yml
        - enc3.js
- mirakurun
    - config
        - server.yml
        - tuners.yml

  
その他のファイルは環境に合わせて自身で作成してください

環境変数で `mariadb` の設定を変更していない場合かつホスト名が`dtv`の場合は `epgstation/config/config.sample.yml` を使い回せます  
変更した場合はエンコード周りの設定をコピペor参考にしてください

```bash
cp epgstation/config/config.sample.yml epgstation/config/config.yml
```

## 起動

最初に

- `nvidia/cuda` イメージベースのEPGStationのビルド
- `chinachu/mirakurun` イメージベースのMirakurunのビルド

が行われます

```bash
docker-compose up -d
```

## Raspberry Pi

 `raspi_mirakurun_only/docker-compose.yml` を使うと、MirakurunのみRaspberry Piで動かせます  
 Raspberry Pi 4 8GB + Ubuntu 21.04 arm64で動作確認しています  
 設定ファイルの変更は自分でなんとかしてください
