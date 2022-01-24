---
layout: post
title: 컴퓨터 시스템의 구조 (2)
categories: OS
tags: [OS]
---
 
 > 인터럽트가 운영체제를 구동시키는 원리와 인터럽트의 한 종류인 시스템콜에 대해 알아본다. 동기식/비동기식 입출력에서의 인터럽트, DMA를 이용한 인터럽트 조절에 대해 알아본다. 계층구조에 의해 I/O에서 입출력명령어가 다름을 이해한다.


## 인터럽트

> 일반적인 의미의 인터럽트는 하드웨어 인터럽트를 의미한다.

![image](https://user-images.githubusercontent.com/60416981/126026772-9d44e0ee-d6c4-4873-a8fa-fca1d8295514.png)

![image](https://user-images.githubusercontent.com/60416981/126325912-e7a7e22c-91dd-4286-ab80-e2f8e24926bf.png)

<br>

## Trap (소프트웨어 인터럽트)

### Exception

> 개별 프로그램이 사용권한이 없는 기계어를 읽으려고 할 때, 오류를 범할 때 인터럽트 라인에 인터럽트를 세팅.
>
> 

### 시스템 콜

> 개별 사용자 프로그램이 운영체제의 서비스를 받기 위해 커널 함수를 호출하는 것



i/o 장치에게 무언가를 요청하는 기계어는 **특권명령**에 포함되어있다.

따라서 사용자 프로그램은 요청을 보낼 수가 없어서 운영체제에게 부탁해야한다.

=> 이 때 운영체제로 제어권을 넘기기위해서 인터럽트를 거는 것이 **시스템 콜**.



![image](https://user-images.githubusercontent.com/60416981/126026730-8f742475-c39c-4c72-a6bf-69cba5e23df7.png)

시스템콜이 실행되면 메모리에서 사용자 프로그램의 기계어가 실행되다가, 운영체제로 이동되게 된다.

<br>

## Device Controller

![image](https://user-images.githubusercontent.com/60416981/150637215-61be59f2-abc9-43c0-9ebc-40e69d81d4d5.png)


- Device Driver  (software)
  - OS가 Device controller에게 요청을 보낼 때 사용하는 각 장치별 처리루틴
- Device Controller (hardware)
  - I/O 디바이스를 통제하는 작은 CPU

- 펌웨어
  - Device controller가 실행하는 기계어



<br>

##  동기식 입출력과 비동기식 입출력

![image](https://user-images.githubusercontent.com/60416981/126326203-af2059b5-4146-4719-a9ac-f4aef9eb5b9c.png)

동기식 입출력 - i/o 작업이 완료된 후에 사용자 프로그램에게 cpu 가 넘어가는 방식

비동기식 입출력 - i/o 작업이 완료되는 걸 기다리지 않고 cpu가 사용자 프로그램에게 넘어가는 방식




<br>

## DMA (Direct Memory Access)

![image](https://user-images.githubusercontent.com/60416981/126328119-edcd0793-67f0-49bc-b000-b6112801a053.png)

DMA로 좀 덜 빈번하게 인터럽트를 발생시킬 수 있다.


<br>


## 서로 다른 입출력 기계어

![image](https://user-images.githubusercontent.com/60416981/126901042-cc87ff30-a015-44f5-abd4-a068091491b9.png)



기계어로 I/O를 수행하는 방법

1. I/O를 전담하는 기계어를 두는 법 (special instruction)
   - 메모리에 접근하는 기계어 따로, I/O 접근하는 기계어 따로

2. 메모리 주소를 I/O 장치에도 연장해서 매겨지게 해놓고 메모리 접근하는 기계어를 통해 (Memory mapped) I/O에 접근
   - 메모리에 접곤하는 기계어로 I/O도 접근함

