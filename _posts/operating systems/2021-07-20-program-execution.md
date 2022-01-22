---
title: 프로그램 실행
date: 2021-07-20 21:30:00 +09:00
tags: [OS]
category: [posts]
description: 프로그램 실행
---

## 프로그램의 실행

![image](https://user-images.githubusercontent.com/60416981/126901283-e171763f-5571-4a41-b24d-998b9a8653db.png)



디스크에 실행파일로 저장되어 있는 프로그램을 실행시키면

메모리에 올라가서 **프로세스**가 된다.


<br>
<br>

![image](https://user-images.githubusercontent.com/60416981/126901329-6bf586ca-dd1f-41b6-82f3-4f150c7f8f66.png)



> 버추얼 메모리 : 프로그램이 실행될 때 만들어지는, 그 프로그램만의 **독자적인 주소 공간**



당장 필요한 부분은 메모리에 올라가서 실행이 되고, 당장 필요하지 않은 부분은 Swap area에 저장되게 된다.

그리고 일부 code는 디스크에 실행 파일로 저장되어 있기도 하다.



이때 버추얼 메모리 주소와 실제 물리적인 메모리 주소는 다른 주소이기 때문에, **주소 변환 과정**이 필요하다.

<br>
<br>

버추얼 메모리는 세 가지로 구성된다.

- stack : 함수 호출과 리턴 등의 정보를 차곡차곡 쌓아놓는 공간
- data : 전역 변수나 프로그램이 실행될 때부터 종료될 때까지 남아있는 데이터들이 위치하는 공간
- code : 코드, 즉 cpu에서 실행될 기계어들이 위치하는 공간


<br>
<br>

## 운영체제 커널 주소 공간

![image](https://user-images.githubusercontent.com/60416981/126901582-56a3fca2-7543-4c30-b4e7-3b1316b34d1f.png)

- PCB (Process Control Block)

  > 시스템 안의 프로세스를 관리하기 위한 자료구조

- stack은 프로세스 별로 별도로 관리됨



<br><br>

## 함수

![image](https://user-images.githubusercontent.com/60416981/126901859-9b37ba3c-278b-44af-93db-40403e4bf717.png)



사용자 정의 함수, 라이브러리 함수는 사용자 프로그램 코드에 포함되어 있다.

그러나 커널 함수는 운영체제 커널에 포함되어있는 함수이다.



<br><br>

## 프로그램 실행 과정

![image](https://user-images.githubusercontent.com/60416981/126901930-5aaf55ec-30a0-4d5b-b21e-0d32649645fe.png)



유저 모드와 커널모드를 왔다갔다 하면서 프로그램이 실행되고 종료하게 된다.

