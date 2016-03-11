# debian-tomcat8

debian-tomcat8

## 1.git clone

```sh
$ git clone git@github.com:hidetarou2013/debian-tomcat8.git
```

## 2.docker build

```sh
$ cd debian-tomcat8
$ docker build -t hidetarou2013/debian-tomcat8 .
$ docker build -t hidetarou2013/debian-tomcat8:1.0 .
$ docker build -t hidetarou2013/debian-tomcat8:JDBC .
$ docker build -t hidetarou2013/debian-tomcat8:MySQL .
$ docker build -t hidetarou2013/debian-tomcat8:MySQL_workbook .
$ docker build -t hidetarou2013/debian-tomcat8:deploy_jaxrs-sample .
```

## 3.docker run


## 3.1 sample1

```sh
$ docker run --name debian-tomcat8 -d -p 8080:8080 hidetarou2013/debian-tomcat8:1.0
```


## 3.2 sample2 : with mysql-server

■前提条件：
MySQLで workbook スキーマを利用することを前提
少なくとも、以下のtagを指定してください。

```
docker pull hidetarou2013/debian-tomcat8:MySQL_workbook
docker pull hidetarou2013/debian-tomcat8:deploy_jaxrs-sample
```

※サンプルとして、MySQLで workbook スキーマ、kenshuu/kenshuu ユーザをJNDI設定しています。
※スキーマは利用するスキーマ情報に編集しなおして、再度ビルドしなおせば、使いまわせます。
conf/server.xml
conf/context.xml


■WEBアプリケーションの配置：共有フォルダへ配置する
※ここでは、サンプルとして「jaxrs-sample.war」を配備するとして説明します。

sample war file jaxrs-sample.war in /webapps folder

■コンテナ側へWEBアプリケーションをデプロイしてからコンテナ起動

```
$ docker run --link mysql-server:mysql -it -d -p 8080:8080 --name debian-tomcat8 -v "$PWD"/webapps/jaxrs-sample.war:/usr/local/tomcat8/apache-tomcat-8.0.30/webapps/jaxrs-sample.war hidetarou2013/debian-tomcat8:deploy_jaxrs-sample
```

## 4.docker-enter

```
$ docker-enter debian-tomcat8
```

