---
title: 운영체제 개요 (2)
date: 2021-07-04 15:30:00 +09:00
tags: [OS]
category: [posts]
description: 운영체제 개요
---

[이화여대 반효경 교수님 강의](http://www.kocw.net/home/search/kemView.do?kemId=1226304)를 듣고 정리한 내용
<br><br>

# 운영체제의 구조

![operating system structure](https://user-images.githubusercontent.com/60416981/150637630-75b6017c-63bf-4570-9240-73a347160af7.png)


<br>

- 어떤 프로그램에게 CPU 사용권을 줄까? **CPU 스케쥴링**
- 한정된 메모리를 어떻게 나누어 쓸까? **메모리 관리**
- 디스크에 들어온 요청을 어떤 순서로 처리할까? **디스크 스케줄링**
- 느린 입출력장치와 빠른 CPU 간에 어떻게 정보를 주고 받게 할까? **인터럽트, 캐싱**
- 컴퓨터 안에서 실행되는 프로그램들을 어떻게 관리할까? **프로세스 관리**
- 그외 - **보호 시스템**, **네트워킹**, **명령어 해석기**

<br><br>

# CPU 스케쥴링

## 1. FCFS (First-Come First-Served)

  > 먼저 요청을 한 프로그램에게 먼저 CPU를 사용하게 해주는 방식

  - 형평성은 있는 것 같지만, 효율적이지 않음.

  - 어떤 프로세스가 먼저 도착하느냐에 따라 효율성이 달라짐.<br>
    

  ![CPU Scheduling](https://user-images.githubusercontent.com/60416981/150637685-780fad9b-b67d-46c1-9802-eb1d6da3fcf4.png)



## 2. SJF (Shortest-Job-First)

  > CPU 사용 시간이 가장 짧은 프로세스를 제일 먼저 CPU를 사용하게 해줌

  - 기아 현상 (Starvation) : 사용시간이 긴 프로세스는 CPU를 사용할 수 없는 상황이 올 수 있음<br>

  

  ![SJF](https://user-images.githubusercontent.com/60416981/150637721-10e46419-303c-4df8-8a95-d22cf3e95986.png)



## 3. RR (Round Robin)

  >각 프로세스에 동일한 크기의 CPU 할당 시간을 부여하고, 할당시간이 끝나면 해당 프로세스는 CPU 큐의 제일 뒤에 줄을 서게 됨.

  - 대기 시간이 프로세스의 CPU 사용 시간에 비례함
  - 어떤 프로세스도 (n-1)*할당시간 이상 기다리지 않음
  - 프로세스의 사용시간이 긴 경우 계속 CPU 큐 뒤로 가서 줄을 서면 됨.<br>

  ![Round Robin](https://user-images.githubusercontent.com/60416981/150637734-e53d36bf-98f2-4c24-ad32-8516de3b3664.png)


<br><br>


# 메모리 관리

![메모리 관리](https://user-images.githubusercontent.com/60416981/150637754-1c86bccb-3807-4040-9c47-3e2561f8d26a.png)


<br>

## 프로세스가 메모리에 할당되는 순서

1. 디스크에 있는 실행파일을 실행시킨다.
2. 해당 프로그램만이 가지는 논리적인 주소 공간(가상메모리)이 만들어진다.
3. 이 가상메모리가 dRam(메모리)에 할당된다.
4. 메모리 공간이 부족할 경우 메모리의 연장공간인 디스크(스왑 메모리)에 프로세스가 저장된다.



> 스왑 메모리:  물리메모리가 부족할 경우를 대비해 사용하는 공간. 디스크의 공간을 메모리처럼 사용한다.

<br><br>

## LRU vs. LFU

![LRU vs. LFU](https://user-images.githubusercontent.com/60416981/150640327-0de6e161-5b61-4a7d-847c-1b9114e7d62c.png)

- 메모리에 프로세스가 꽉 찼을 경우 어떤 프로세스를 내보내고 새로운 프로세스를 할당할 것인가?
  - 과거를 보고 가까운 미래에 사용될 확률이 낮은 프로세스를 내보낸다.

- LRU: 가장 오래 전에 참조된 페이지를 삭제 => 페이지 1
- LFU: 참조 횟수가 가장 적은 페이지를 삭제 => 페이지 4
- 두 방식 모두 단점이 있기 때문에 LRU와 LFU를 보완한 방법이 필요

<br><br>


# 디스크 스케줄링

> 먼저 요청이 들어온 순서대로 처리한다면, 디스크 헤드의 이동 거리가 길어진다.

![디스크 스케줄링](https://user-images.githubusercontent.com/60416981/150640332-15f610ca-a85a-47a6-aad9-16efbf0c55cc.png)

<br>

## 디스크 스케쥴링의 목표

> Seek Time을 줄이고, 디스크 헤드의 이동거리를 줄여 효율성을 극대화하자

![디스크 스케줄링의 목표](https://user-images.githubusercontent.com/60416981/150640345-5a7623c0-e687-4f56-ba8c-949fb3268b81.png)

<br>

## 1. FCFS (First-Come First-Served)

> 먼저 요청이 들어온 순서대로 처리

- 헤드의 이동거리가 길어 효율성이 떨어져 사용하지 않음!

![FCFS](https://user-images.githubusercontent.com/60416981/150640362-c1ed23d8-14fc-44ff-b926-17c71402eacc.png)

<br>

## 2. SSTF (Shortest Seek Time First)

>  탐색 시간이 가장 짧은 요청을 먼저 처리

- Starvation 문제 발생

![SSTF](https://user-images.githubusercontent.com/60416981/150640370-d508cab8-91d4-4eba-a707-7286e58718ff.png)



<br>

## 3. SCAN

> 요청 큐에 상관없이 헤드가 이동하는 길목에 있는 요청을 처리하는 방법

- Starvation 문제가 발생하지 않음
- 헤드의 이동 거리가 짧아짐

![SCAN](https://user-images.githubusercontent.com/60416981/150640376-17a2b67e-b574-410f-95b1-0093f04c944d.png)



<br>

# 저장장치 계층구조과 캐싱(caching)

> I/O 장치와 CPU 사이의 속도차이를 완충하기 위해 캐싱을 사용함

- 캐싱: 빠른 저장장치에 정보를 복사해놓아 빠르게 가져다쓸 수 있게 하는 것
  - 처음에는 제일 밑 계층의 디스크에서  파일을 읽어오지만, 다시 요청한다면 중간 단계에 있는 복사본을 사용하면 되기 때문에 시간이 절약됨
  - 용량이 한정되어 있기 때문에 모든 정보를 복사해놓을 수는 없음

![Caching](https://user-images.githubusercontent.com/60416981/150640407-2d34f7f2-0baa-403f-869d-7131aa5da6d5.png)

- Speed
  - 위로 올라갈수록 빠르고, 아래로 내려올수록 느림

- Cost
  - 위로 올라갈수록 비싸고, 아래로 내려올수록 저렴함

- Volatility (휘발성)
  - 메모리는 휘발성, 디스크는 비휘발성


<br>


## 플래시메모리

![플래시메모리](https://user-images.githubusercontent.com/60416981/150640418-fbc7188e-4f4c-428c-979b-de60f3d59b72.png)

- 플래시메모리의 단점
  - 데이터 변형이 일어날 가능성이 있음(시간이 지나면 전하가 조금씩 빠져나가므로)
  - 쓰기 횟수가 제약되어 있음

