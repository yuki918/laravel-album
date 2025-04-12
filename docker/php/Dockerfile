# ベースイメージの指定
FROM php:8.2-fpm

# コンテナ内で作業する際のカレントディレクトリの指定
WORKDIR /var/www/html

# 作成した設定ファイルをコンテナ内にコピー
COPY php.ini /usr/local/etc/php/php.ini

# パッケージのインストール
RUN apt-get update \
    && apt-get -y install git zip unzip vim

# voltaのパスの追加
ENV VOLTA_HOME="/root/.volta"
ENV PATH="$VOLTA_HOME/bin:$PATH"
# voltaを使用して、nodeとpnpmのインストール
RUN curl https://get.volta.sh | bash \
    && volta install node@22.5.1 \
    && volta install pnpm@10.8.0

# PHP拡張モジュールのインストール
RUN docker-php-ext-install pdo_mysql

# composerのインストール（https://hub.docker.com/_/composer）
COPY --from=composer /usr/bin/composer /usr/bin/composer
