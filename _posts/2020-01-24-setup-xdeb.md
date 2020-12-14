---
title: Setup Xdebug in Docker container on Linux
author: PipisCrew
date: 2020-01-24
categories: [php,docker]
toc: true
---

We are on Linux (Fedora v30), as Stanislas guide us (using Macintosh) @ :
https://github.com/angristan/php-xdebug-docker

seems that Xdebug loaded at phpinfo(); 

but there is no communication with the out world except container. In detail, setuping Xdebug into a container means that we doing **remote debugging**. The problem in his example is that provide the DockerIP using the const **host.docker.internal**, where is **not exists** on linux.

> On Docker for Windows (and Mac), there is a magic hostname host.docker.internal that containers can use to connect to services on the host. There's no direct equivalent in Linux Docker.

 [src](https://www.reddit.com/r/docker/comments/8xeqe6/hostdockerinternal_on_linux_sort_of/)

This easily can be validated by searching Docker Docs
https://docs.docker.com/search/?q=host.docker.internal
returns only these two
https://docs.docker.com/docker-for-mac/networking/
https://docs.docker.com/docker-for-windows/networking/

* * *

There are different ways getting the DockerIP

1) As Stanislas guide linked us :
https://github.com/docker/for-linux/issues/264

2) executing out of container :
```js
# src - https://github.com/angristan/php-xdebug-docker/issues/4#issuecomment-528418403
sudo docker network inspect bridge
```

find out the "Config > Gateway“ IP
![alt](https://i.imgur.com/HwuUDHO.png)

3) executing out of container :
```js
ip a
```

find out the "inet“ for docker0
![alt](https://i.imgur.com/tZGmOxo.png)

4) If you expect that IP address might change you could go the extra mile and do something like :

```js
docker container run -e "DOCKER_HOST=$(ip -4 addr show docker0 | grep -Po 'inet \K[\d.]+')"
```

this way every time you run your container, it’ll have the **IP address** available inside the container set to the **DOCKER_HOST environment** variable.  [src](https://nickjanetakis.com/blog/docker-tip-65-get-your-docker-hosts-ip-address-from-in-a-container)

* * *

So we know the DockerIP^. **Dockerfile** part, for Xdebug is :
```js
# Install xDebug [start]
RUN pecl install xdebug \
 && docker-php-ext-enable xdebug \
 && echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
 #here replace your DockerIP
 && echo "xdebug.remote_host=172.17.0.1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

#An IDE key has to be set, but anything works, at least for PhpStorm and VS Code...
ENV XDEBUG_CONFIG="xdebug.idekey=''"
# Install xDebug [end]
```

At Docker, in a general routine, the mandatory file is the **Dockerfile** and nothing else, meaning that all various commands using others in a **docker-compose.yml** file, can be done through commandline. If finally we have a **docker-compose.yml** file, we proceed with the image build & run, by executing :
```js
sudo docker-compose up --build -d
```

Now all setted.

* * *

Setup php.ini for Xdebug

inside container, we have to add the following lines at **php.ini** 

```js
[XDebug]
xdebug.remote_enable = 1
xdebug.remote_autostart = 1
```

the common path for php.ini is at /usr/local/etc/php, when doesnt exist, locate it using one of the following :

-do a phpinfo() and check the 'Configuration File (php.ini) Path'
-outside docker exec 'sudo docker inspect laravel-phpx' to find the **PHP_INI_DIR** environment variable (Config > Env > PHP_INI_DIR)

* * *

Steps might we take, when no **docker-compose.yml** file is present.
```js
# install dependencies - https://hub.docker.com/_/composer
sudo docker run --rm -v $(pwd):/app composer install

# create network - https://docs.docker.com/engine/reference/commandline/network_create/
sudo docker network create --driver bridge laravelX

# build the image - https://docs.docker.com/engine/reference/commandline/build/
sudo docker build -t laravel-php-imgx -f Dockerfile .

# run the image - https://docs.docker.com/v17.12/engine/reference/commandline/run/
sudo docker run --name laravel-phpx --network laravelX -p 8080:80 -v $PWD:/var/www/html laravel-php-imgx

# if you want also mysql run on the same 'network‘ (new container will be created) :
sudo docker run --name laravel-dbX --network laravelX -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -d mysql:5.7
ref (mysql:5.7) - https://hub.docker.com/_/mysql?tab=tags
```

after all, make sure is up and running by exec 'list containers' command. Various commands :
```js
# list containers
sudo docker ps -a

# delete the container
sudo docker rm --force laravel-phpx

# list bridges
sudo docker network ls

# get in container
sudo docker exec -it laravel-phpx bash

# remove container (force)
sudo docker rm -f laravel-phpx

# start docker service
sudo service docker start

# start a container
sudo docker start laravel-phpx

# inspect properties
sudo docker inspect laravel-phpx
```

When container is up and running, make a test php file to see if Xdebug module is there.
```js
phpinfo();
```

![alt](https://i.imgur.com/tm1QOXz.png)

alternatively :
```js
# src - https://gist.github.com/joseluisq/d7586c9e5bd52012e0cf

php -r 'echo (extension_loaded("xdebug") ? "xdebug up and running!" : "xdebug is not loaded!");'
```

* * *

At Visual Studio Code (VSCode), add this addon https://marketplace.visualstudio.com/items?itemName=felixfbecker.php-debug

make sure the addon configuration (launch.json) is setted as (**the port doesnt matter**, if shows that is in use, use 9001 and so on), the various line here is the **pathMappings**) :
```js
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for XDebug",
            "type": "php",
            "request": "launch",
            "port": 9000,
            "pathMappings": {
                "/var/www/html/": "${workspaceFolder}"
            },
        }
    ]
}
```

[XDebug - Debug context lost on multiple connections](https://github.com/felixfbecker/vscode-php-debug/issues/301)
try to clear @ IDE the watch variable(s) first and restart container and try again!

--

## Laravel & Xdebug by Jonathan

By default Laravel will encrypt, and subsequently also decrypt, all cookies on a request.

When using Xdebug to debug your application from a browser, a cookie called "XDEBUG_SESSION" is set. As this cookie was not set, and thus not encrypted, by the Laravel framework, an error will be thrown when the framework automatically detects and tries to decrypt the cookie.

merge this to xdebug addon configuration (launch.json)
```js
,
"ignore": [
"**/vendor/**/*.php"
]
```

src - https://stackoverflow.com/a/55340395/1320686

* * *

On Fedora, the docker images exist at :
/var/lib/docker/overlay2    [more](https://stackoverflow.com/a/25978888/1320686)

refs :
https://xdebug.org/docs/all_settings

[Docker for Beginners: Full Course (video)](https://www.youtube.com/watch?v=zJ6WbK9zFpI)

[2017 - After moving from linux to macOS I bumped into looping back to host issue](https://medium.com/@yuliakostrikova/configure-remote-debugging-with-xdebug-for-php-docker-container-on-macos-8edbc01dc373)

#docker

origin - https://www.pipiscrew.com/?p=16420 setup-xdebug-in-docker-container-on-linux