# docker-for-php-framework

Extract from laradock, for small start.


```
$ git clone https://github.com/ta-toshio/docker-for-php-framework
$ cd docker-for-php-framework
$ docker-compose up -d

if application project not exists,
    $ docker-compose exec -ume workspace bash
    create cakephp project
    $ composer create-project --prefer-dist cakephp/app cakeapp

    your host machine
    sudo vim /etc/hosts
    #  add below
    127.0.0.1      cakeapp.test
```

