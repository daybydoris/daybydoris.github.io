---
layout: post
title: 프로세스 관리 (1)
categories: OS
tags: [OS]
---

[이화여대 반효경 교수님 강의](http://www.kocw.net/home/search/kemView.do?kemId=1046323)를 듣고 정리한 내용
<br><br>

## 프로세스 생성

![image](https://user-images.githubusercontent.com/60416981/150637072-6fc7e355-7d55-4d30-ab2e-b07238693688.png)

![image](https://user-images.githubusercontent.com/60416981/150637080-c709b17c-0ec2-46c6-9d31-49ac480a76f3.png)


- 자식은 부모의 공간을 복제 => 그 공간에 새로운 프로그램을 올림

- fork() 나 exec() 는 시스템 콜로, 운영체제의 도움을 받아야만 프로세스 생성 가능



- copy-on-write : write가 발생했을 때 copy를 하는 것. 그 이전까지는 부모 프로세스를 그대로 공유하고 있는 것.

<br>

## 프로세스 종료
![image](https://user-images.githubusercontent.com/60416981/150637085-1d7ef0ef-daab-4cb4-89c0-ca2d0a995cf1.png)


- exit => 프로세스가 스스로 종료하는 것
- abort => 자식 프로세스의 수행을 종료시킴 

