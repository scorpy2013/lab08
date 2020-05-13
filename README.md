## Laboratory work VIII

<a href="https://yandex.ru/efir/?stream_id=v0mnBi_R2Ldw"><img src="https://raw.githubusercontent.com/tp-labs/lab08/master/preview.png" width="640"/></a>

Данная лабораторная работа посвещена изучению систем автоматизации развёртывания и управления приложениями на примере **Docker**

```sh
$ open https://docs.docker.com/get-started/
```

## Tasks

- [x] 1. Создать публичный репозиторий с названием **lab08** на сервисе **GitHub**
- [x] 2. Ознакомиться со ссылками учебного материала
- [x] 3. Выполнить инструкцию учебного материала
- [x] 4. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
Cloning into 'lab08'...
remote: Enumerating objects: 73, done.
remote: Counting objects: 100% (73/73), done.
remote: Compressing objects: 100% (49/49), done.
remote: Total 73 (delta 23), reused 73 (delta 23), pack-reused 0
Receiving objects: 100% (73/73), 948.58 KiB | 1.27 MiB/s, done.
Resolving deltas: 100% (23/23), done.
$ export GITHUB_USERNAME=scorpy2013
```

```
$ cd ${GITHUB_USERNAME}/workspace
$ pushd .
~/Documents/GitHub/scorpy2013/lab08 ~/Documents/GitHub/scorpy2013/lab08
$ source scripts/activate
```

```sh
$ git clone https://github.com/${GITHUB_USERNAME}/lab07 lab08
Cloning into 'lab08'...
remote: Enumerating objects: 145, done.
remote: Counting objects: 100% (145/145), done.
remote: Compressing objects: 100% (99/99), done.
Receiving objects:  50% (73/145), 628
Receiving objects: 100% (145/145), 1.29 MiB | 1.62 MiB/s, done.
Resolving deltas: 100% (46/46), done.
$ cd lab08
$ git submodule update --init
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab08
```

```sh
$ cat > Dockerfile <<EOF
FROM ubuntu:18.04
EOF
```

```sh
$ cat >> Dockerfile <<EOF

RUN apt update
RUN apt install -yy gcc g++ cmake
EOF
```

```sh
$ cat >> Dockerfile <<EOF

COPY . print/
WORKDIR print
EOF
```

```sh
$ cat >> Dockerfile <<EOF

RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install
RUN cmake --build _build
RUN cmake --build _build --target install
EOF
```

```sh
$ cat >> Dockerfile <<EOF

ENV LOG_PATH /home/logs/log.txt
EOF
```

```sh
$ cat >> Dockerfile <<EOF

VOLUME /home/logs
EOF
```

```sh
$ cat >> Dockerfile <<EOF

WORKDIR _install/bin
EOF
```

```sh
$ cat >> Dockerfile <<EOF

ENTRYPOINT ./demo
EOF
```

```sh
$ docker build -t logger .
```

```sh
$ docker images
```

```sh
$ mkdir logs
$ docker run -it -v "$(pwd)/logs/:/home/logs/" logger
text1
text2
text3
<C-D>
```

```sh
$ docker inspect logger
```

```sh
$ cat logs/log.txt
```

```sh
$ gsed -i 's/lab07/lab08/g' README.md
```

```sh
$ vim .travis.yml
/lang<CR>o
services:
- docker<ESC>
jVGdo
script:
- docker build -t logger .<ESC>
:wq
```

```sh
$ git add Dockerfile
$ git add .travis.yml
$ git commit -m"adding Dockerfile"
On branch master
Your branch is up to date with 'origin/master'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .travis.yml.swp
        lab08/

nothing added to commit but untracked files present (use "git add" to track)
$ git push origin master
Everything up-to-date
```

```sh
$ travis login --auto
Successfully logged in as scorpy2013!
$ travis enable
Detected repository as scorpy2013/lab08, is this correct? |yes| yes
scorpy2013/lab08: enabled :)
```

## Report

```sh
$ popd
$ export LAB_NUMBER=08
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
Cloning into 'tasks/lab08'...
remote: Enumerating objects: 15, done.
remote: Counting objects: 100% (15/15), done.
remote: Compressing objects: 100% (14/14), done.
remote: Total 73 (delta 4), reused 3 (delta 1), pack-reused 58
Receiving objects: 100% (73/73), 950.66 KiB | 1.34 MiB/s, done.
Resolving deltas: 100% (22/22), done.
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

## Links

- [Book](https://www.dockerbook.com)
- [Instructions](https://docs.docker.com/engine/reference/builder/)

```
Copyright (c) 2015-2019 The ISC Authors
```
