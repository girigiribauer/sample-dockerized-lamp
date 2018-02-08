FROM centos:7

# タイムゾーン設定
RUN ln -sf  /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

# 各パッケージのアップデート
RUN yum -y update

# remi リポジトリの追加（remi を入れるには epel も必要）
RUN yum -y install epel-release
RUN rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm

# Apache(httpd), PHP のインストール
RUN yum -y --enablerepo=remi,remi-php72 install \
    httpd \
    php \
    php-cli \
    php-common \
    php-devel \
    php-gd \
    php-mbstring \
    php-mysqli \
    php-mysqlnd \
    php-pecl-apcu \
    php-xml \
    php-xmlrpc

# httpd.conf のログを stdout, stderr に繋ぐ
RUN ln -sf /dev/stdout /var/log/httpd/access_log && \
    ln -sf /dev/stderr /var/log/httpd/error_log

# mime タイプのファイル追加
RUN ln -sf /etc/mime.types /etc/httpd/conf/mime.types

# PHP 設定ファイル
COPY php.ini /etc/php.ini

CMD ["/usr/sbin/httpd","-D","FOREGROUND"]
