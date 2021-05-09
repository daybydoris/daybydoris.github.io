---
title: feature 브랜치를 develop과 master에 merge하기 (gitflow)
date: 2021-05-09 14:31:00 +09:00
tags: [git, gitflow]
description: feature 브랜치를 develop과 master에 merge하기 (gitflow)
---



## 1. feature 따서 작업하기



최신 develop에서 feature 따기

```json
$ git checkout develop // develop으로 이동
$ git checkout -b "feature/브랜치 이름" // 새 feature 브랜치를 만들고 이동
```



~ 작업 ~





## 2. feature를 develop에 merge하기

작업 끝나면 **develop**에 PR 날려서 merge함.

master가 default로 되어있어서 자꾸 master에 pr 날리는데,,, 

default를 바꿔도 되는지 모르겠음.



develop 최신화 해줌

```json
$ git checkout develop // develop으로 이동
$ git pull origin develop // merge한 것을 pull 받음
```





## 3. develop에서 pull 받고 master에 배포하기

```json
$ git checkout master // master로 이동
$ git pull origin develop // 최신화 된 develop을 pull 받음
$ git push origin master // master에 push
```



