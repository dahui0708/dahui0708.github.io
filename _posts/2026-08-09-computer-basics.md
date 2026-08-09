---
title: "컴퓨터 기초 핵심 개념"
date: 2026-08-09 16:47:00 +0900
categories: [강의 학습, 컴퓨터 기초]
tags: [computer-basics, computer-architecture, operating-system]
---

# 컴퓨터 기초

정보보안을 공부하기 위해서는 공격 기법이나 보안 도구를 배우기 전에 컴퓨터가 어떤 구조로 동작하는지 이해하는 것이 중요함

보안에서 다루는 공격과 취약점 역시 결국 컴퓨터의 정상적인 동작 구조를 이용하거나 그 구조의 허점을 노리는 것이기 때문

예를 들어 다음과 같은 내용을 공부할 때 컴퓨터 기초가 계속 등장함

- 리버싱 → CPU, Register, Memory, Assembly
- 시스템 해킹 → Process, Memory, Stack, Heap, Permission
- 디지털 포렌식 → File, File System, Metadata, Timestamp
- 악성코드 분석 → Process, Memory, Operating System
- 침해사고 대응 → Process, User, Permission, Log

따라서 모든 내용을 암기하기보다는 각 개념이 무엇이며 서로 어떻게 연결되는지 이해하는 것이 중요

## 1. 컴퓨터의 기본 구조

컴퓨터는 데이터를 입력받고 처리한 뒤 결과를 저장하거나 출력하는 장치

기본적인 동작 과정은 다음과 같음

```text
입력(Input)
    ↓
처리(Process)
    ↓
저장(Storage)
    ↓
출력(Output)
```

예를 들어 메모장에 `Hello`를 입력하고 저장하는 경우

```text
키보드
↓
문자 입력

CPU
↓
명령과 데이터 처리

RAM
↓
현재 작업 중인 데이터 임시 저장

SSD
↓
파일을 장기간 저장

모니터
↓
현재 작업 결과 출력
```

컴퓨터의 구성 요소는 크게 **Hardware, Software, Data**로 구분 가능

### Hardware

컴퓨터를 구성하는 실제 물리적인 장치

대표적인 Hardware

- CPU
- RAM
- SSD / HDD
- GPU
- Motherboard
- Keyboard
- Mouse
- Monitor

즉, 실제로 만질 수 있는 컴퓨터 부품에 해당

### Software

Hardware 위에서 실행되는 프로그램

대표적인 Software

- Windows
- Linux
- Chrome
- VS Code
- Python
- 게임

Hardware만 존재해서는 사용자가 원하는 작업을 수행하기 어려움

Software가 Hardware에게 어떤 작업을 수행할 것인지 명령하는 구조

### Data

컴퓨터가 저장하고 처리하는 정보

예시

- 문자
- 숫자
- 사진
- 영상
- 음악
- 문서
- 프로그램

사람에게는 사진과 문자와 프로그램이 서로 전혀 다른 것처럼 보이지만 컴퓨터 내부에서는 결국 **0과 1로 구성된 데이터**로 저장됨

## 2. Bit와 Byte

컴퓨터가 데이터를 어떻게 표현하는지 이해하기 위한 가장 기본적인 개념

### Bit

**Bit = Binary Digit**

컴퓨터에서 사용하는 가장 작은 정보 단위

하나의 Bit는 두 가지 상태를 표현할 수 있음

```text
0
1
```

컴퓨터 내부의 전자 회로가 두 가지 상태를 구분하기 쉬운 특성을 이용하여 데이터를 0과 1로 표현

### Byte

여러 Bit를 묶어서 사용하는 데이터 단위

일반적으로

```text
8 Bit = 1 Byte
```

예를 들어

```text
01000001
```

은 총 8개의 Bit로 구성되어 있으므로 1Byte

### 데이터 크기 단위

```text
Bit
↓
Byte
↓
KB
↓
MB
↓
GB
↓
TB
```

저장장치 제조사 등에서는 주로 1000 단위를 사용

```text
1 KB = 1000 Byte
1 MB = 1000 KB
1 GB = 1000 MB
```

컴퓨터 시스템에서는 1024 단위를 사용하는 경우도 존재

이 경우 정확한 표기는 다음과 같음

```text
1 KiB = 1024 Byte
1 MiB = 1024 KiB
1 GiB = 1024 MiB
```

입문 단계에서는 KB, MB, GB 등의 크기 관계를 이해하는 것이 우선

## 3. 2진수, 10진수, 16진수

컴퓨터에서는 같은 숫자를 여러 진법으로 표현할 수 있음

### 10진수 Decimal

사람이 일상적으로 사용하는 숫자 체계

사용하는 숫자

```text
0 1 2 3 4 5 6 7 8 9
```

10개의 숫자를 사용하기 때문에 10진수라고 부름

### 2진수 Binary

컴퓨터에서 데이터를 표현하는 기본적인 숫자 체계

사용하는 숫자

```text
0
1
```

예를 들어

```text
10진수 10

2진수 1010
```

두 값은 표현 방법만 다를 뿐 같은 숫자

### 16진수 Hexadecimal

16개의 값을 사용하는 숫자 체계

```text
0 1 2 3 4 5 6 7 8 9 A B C D E F
```

A부터 F는 다음 값을 의미

```text
A = 10
B = 11
C = 12
D = 13
E = 14
F = 15
```

16진수라는 것을 표시하기 위해 일반적으로 `0x`를 앞에 붙임

```text
0x10
0x41
0xFF
```

### 16진수를 사용하는 이유

2진수는 컴퓨터가 데이터를 표현하기에는 적합하지만 사람이 읽기에는 너무 길어지는 문제가 존재

예를 들어

```text
2진수
01000001

16진수
41
```

4개의 Bit를 16진수 한 자리로 표현 가능

```text
0100 = 4
0001 = 1

01000001
↓
0x41
```

따라서 Memory Address, Machine Code, File Data 등을 분석할 때 16진수를 많이 사용

정보보안에서는 특히

- Reverse Engineering
- Digital Forensics
- System Hacking
- Malware Analysis

등에서 자주 사용

## 4. 문자는 컴퓨터에 어떻게 저장되는가

컴퓨터는 문자 자체를 이해하는 것이 아니라 문자를 숫자와 연결하여 저장

예를 들어 문자 `A`를 특정 숫자 값과 연결하는 방식

### ASCII

**ASCII = American Standard Code for Information Interchange**

영문자, 숫자, 특수문자 등을 숫자와 연결한 문자 코드 체계

예를 들어 문자 `A`

```text
문자
A

ASCII 10진수
65

16진수
0x41

2진수
01000001
```

즉 다음 값들은 같은 데이터를 서로 다른 방식으로 표현한 것

```text
A
65
0x41
01000001
```

### Unicode

ASCII만으로는 한글, 중국어, 일본어 등 전 세계의 다양한 문자를 충분히 표현하기 어려움

이를 해결하기 위해 만들어진 문자 표준이 Unicode

Unicode는 각 문자에 고유한 값을 지정

예를 들어

```text
영어
한글
일본어
중국어
특수문자
이모지
```

등을 하나의 표준으로 표현할 수 있도록 설계

### Encoding

문자 정보를 실제 Byte 데이터로 어떻게 저장할 것인지 결정하는 방식

대표적인 Encoding

- UTF-8
- UTF-16
- UTF-32

웹과 Linux를 비롯한 많은 환경에서는 UTF-8을 널리 사용

문자가 깨지는 현상 역시 저장된 데이터와 이를 해석하는 Encoding 방식이 서로 맞지 않을 때 발생할 수 있음

## 5. CPU

**CPU = Central Processing Unit**

프로그램에 포함된 명령어를 실제로 실행하는 컴퓨터의 핵심 장치

쉽게 생각하면 컴퓨터의 계산과 명령 처리를 담당하는 장치

프로그램에서 다음과 같은 명령이 존재한다고 가정

```text
숫자 두 개 더하기
값 비교하기
특정 조건이면 다른 위치로 이동하기
메모리에서 데이터 가져오기
```

이러한 명령을 CPU가 수행

### CPU의 기본 동작

CPU는 단순화하면 다음 과정을 반복

```text
명령어 가져오기
Fetch
↓
명령어 해석
Decode
↓
명령어 실행
Execute
```

이를 **Fetch - Decode - Execute Cycle**이라고 부름

### ALU

**ALU = Arithmetic Logic Unit**

CPU 내부에서 산술 연산과 논리 연산을 담당

예

```text
덧셈
뺄셈
비교
AND
OR
XOR
```

### Control Unit

CPU 내부에서 명령어 실행 과정을 제어하는 부분

어떤 명령어를 실행해야 하는지 판단하고 CPU의 여러 구성 요소를 제어

## 6. Register

Register는 CPU 내부에 존재하는 **매우 작고 매우 빠른 저장 공간**

CPU가 명령을 처리하는 과정에서 바로 사용할 값들을 잠시 저장

예를 들어

```text
10 + 20
```

이라는 계산을 수행한다면 CPU는 계산에 필요한 값과 결과를 Register에 저장하여 사용할 수 있음

속도를 기준으로 단순화하면

```text
Register
가장 빠름 / 매우 작음

↓
Cache

↓
RAM

↓
SSD / HDD
가장 느림 / 매우 큼
```

Register는 Reverse Engineering과 System Hacking에서 매우 중요

x86-64 환경에서는 다음과 같은 Register 이름을 만나게 됨

```text
RAX
RBX
RCX
RDX
RSP
RBP
RIP
```

현재 단계에서는 Register 이름을 모두 암기할 필요 없음

우선

> Register = CPU가 연산 과정에서 직접 사용하는 매우 빠른 작은 저장 공간

이라는 개념 이해가 중요

## 7. CPU Core

Core는 CPU 내부에서 실제 명령어를 처리할 수 있는 실행 단위

예를 들어

```text
4 Core CPU
8 Core CPU
16 Core CPU
```

등의 표현 사용

여러 Core를 가진 CPU는 여러 작업을 동시에 처리하는 데 유리

### Hardware Thread

하나의 CPU Core가 여러 실행 흐름을 처리할 수 있도록 하는 기술과 관련된 개념

컴퓨터 사양에서

```text
8 Core / 16 Thread
```

와 같은 표현을 확인 가능

이때의 Hardware Thread와 프로그램에서 사용하는 Software Thread는 관련은 있지만 동일한 개념은 아님

## 8. Clock

CPU가 동작하는 속도와 관련된 신호

일반적으로 GHz 단위로 표현

예

```text
3.5 GHz
4.2 GHz
```

다만 CPU 성능은 Clock만으로 결정되지 않음

다음 요소가 함께 영향을 미침

- CPU Architecture
- Core 수
- Cache
- 명령 처리 효율
- 전력 및 발열 관리

따라서 GHz가 높다고 항상 더 빠른 CPU라는 의미는 아님

## 9. Cache Memory

CPU는 RAM보다 훨씬 빠르게 동작

CPU가 필요한 데이터를 매번 RAM에서 가져오면 기다리는 시간이 많아질 수 있음

이 속도 차이를 줄이기 위해 사용하는 것이 Cache Memory

대표적인 Cache

```text
L1 Cache
L2 Cache
L3 Cache
```

일반적으로 CPU에 가까운 Cache일수록

- 더 빠름
- 용량이 작음

현재 단계에서는

> Cache = CPU가 자주 사용하는 데이터에 빠르게 접근하기 위해 사용하는 고속 메모리

정도로 이해하면 충분

## 10. RAM

**RAM = Random Access Memory**

현재 실행 중인 프로그램과 프로그램이 사용하는 데이터를 임시로 저장하는 공간

예를 들어 Chrome을 실행하면

```text
SSD
Chrome 프로그램 저장

↓ 실행

RAM
Chrome 실행에 필요한 코드와 데이터 저장

↓

CPU
RAM에 있는 명령어와 데이터 사용
```

### RAM의 특징

일반적인 RAM은 **휘발성 메모리**

컴퓨터의 전원을 끄면 저장된 내용이 사라짐

```text
전원 ON
RAM에 데이터 존재

↓

전원 OFF

↓

RAM 데이터 사라짐
```

따라서 RAM은 파일을 장기간 보관하기 위한 저장장치가 아니라 현재 작업을 위한 공간

Digital Forensics에서는 RAM에 남아 있는 정보를 분석하는 **Memory Forensics**도 존재

## 11. ROM

**ROM = Read Only Memory**

전원이 꺼져도 데이터가 유지되는 비휘발성 메모리 계열과 관련된 개념

과거에는 이름 그대로 읽기 전용 메모리의 의미가 강했지만 현대 컴퓨터에서는 수정 가능한 Flash Memory 형태가 Firmware 저장 등에 사용되는 경우가 많음

현재 단계에서는

```text
RAM
→ 전원이 꺼지면 일반적으로 데이터 소멸

ROM 계열 비휘발성 메모리
→ 전원이 꺼져도 데이터 유지
```

정도의 차이 이해가 우선

## 12. HDD와 SSD

컴퓨터에서 파일을 장기간 저장하는 Storage Device

### HDD

**HDD = Hard Disk Drive**

자기 디스크를 회전시키면서 데이터를 저장하는 저장장치

특징

- 대용량 저장에 유리
- 용량 대비 가격이 저렴한 편
- 물리적으로 움직이는 부품 존재
- SSD보다 일반적으로 느림

### SSD

**SSD = Solid State Drive**

반도체 메모리를 이용하여 데이터를 저장하는 장치

특징

- HDD보다 빠른 데이터 접근
- 물리적으로 회전하는 디스크 없음
- 소음이 적음
- 현대 PC에서 널리 사용

## 13. RAM과 SSD의 차이

컴퓨터를 이해할 때 반드시 구분해야 하는 개념

| RAM | SSD |
|---|---|
| 현재 작업 공간 | 장기간 저장 공간 |
| 실행 중인 데이터 저장 | 파일 저장 |
| 매우 빠름 | RAM보다 느림 |
| 일반적으로 휘발성 | 비휘발성 |
| 프로그램 실행 시 사용 | 프로그램 파일 자체 저장 |

쉽게 비유하면

```text
SSD = 책장

RAM = 책상

CPU = 책상에서 실제 작업을 하는 사람
```

책장에서 필요한 책을 꺼내 책상 위에 올리고 작업하는 것과 비슷한 구조

## 14. Motherboard

Motherboard는 컴퓨터의 주요 부품들이 연결되는 중심 기판

한국에서는 일반적으로 **메인보드**라고 부름

다음과 같은 장치들이 Motherboard를 통해 연결

```text
CPU
RAM
GPU
SSD
USB
Network Device
```

각 장치가 독립적으로 존재하는 것이 아니라 Motherboard의 연결 구조를 통해 데이터를 주고받음

## 15. Bus

컴퓨터 내부 구성 요소 사이에서 데이터와 신호를 전달하는 통로

대표적인 개념

```text
Data Bus
Address Bus
Control Bus
```

### Data Bus

실제 데이터를 전달

### Address Bus

어떤 Memory Address나 장치에 접근할 것인지 전달

### Control Bus

읽기, 쓰기 등 제어와 관련된 신호 전달

입문 단계에서는

> Bus = CPU, Memory, Device 등이 서로 정보를 주고받기 위한 통로

라고 이해하면 충분

## 16. Input / Output

**I/O = Input / Output**

컴퓨터가 외부와 데이터를 주고받는 과정

### Input Device

컴퓨터에 정보를 입력하는 장치

예

- Keyboard
- Mouse
- Microphone
- Camera

### Output Device

컴퓨터가 처리한 결과를 사용자에게 전달하는 장치

예

- Monitor
- Speaker
- Printer

프로그램에서도 파일 읽기, 키보드 입력, 화면 출력 등을 I/O 작업이라고 표현

## 17. GPU

**GPU = Graphics Processing Unit**

대량의 계산을 병렬로 처리하는 데 특화된 장치

원래 그래픽 처리 목적으로 발전했지만 현재는 다양한 작업에 사용

예

- 3D Graphics
- Game
- AI
- 영상 처리
- 과학 계산

CPU와 비교하면 CPU는 다양한 작업을 처리하는 범용성이 높고 GPU는 많은 계산을 동시에 처리하는 병렬 연산에 강한 특성을 가짐

## 18. Software의 종류

Software는 크게 System Software와 Application Software로 생각 가능

```text
Software
│
├─ System Software
│   └─ Operating System
│
└─ Application Software
    ├─ Chrome
    ├─ VS Code
    ├─ Discord
    └─ Game
```

### System Software

컴퓨터 Hardware를 관리하고 다른 Software가 실행될 수 있는 환경을 제공

대표적으로 Operating System

### Application Software

사용자가 특정 작업을 수행하기 위해 사용하는 프로그램

예

- Web Browser
- Text Editor
- Game
- Messenger

## 19. Operating System

**OS = Operating System = 운영체제**

컴퓨터의 Hardware와 Software를 관리하는 핵심 System Software

대표적인 운영체제

- Windows
- Linux
- macOS
- Android
- iOS

운영체제의 주요 역할

```text
CPU 관리
Memory 관리
Process 관리
File 관리
Device 관리
User 관리
Permission 관리
```

예를 들어 Chrome과 VS Code를 동시에 실행하면 두 프로그램이 CPU와 RAM을 사용해야 함

각 프로그램이 Hardware를 마음대로 사용하도록 두는 것이 아니라 운영체제가 자원을 관리하고 배분

## 20. Kernel

Kernel은 Operating System의 핵심 부분

운영체제에서 가장 중요한 시스템 자원을 직접 관리

대표적으로 관리하는 대상

- CPU
- Memory
- Process
- File System
- Device

일반 프로그램이 Hardware를 직접 마음대로 조작할 경우 시스템 안정성과 보안에 문제가 발생 가능

따라서 다음과 같은 구조 사용

```text
Application
     ↓
Operating System
     ↓
Kernel
     ↓
Hardware
```

Kernel은 정보보안에서 매우 중요한 개념

System Hacking, Malware Analysis, Digital Forensics 등에서 계속 등장

## 21. User Space와 Kernel Space

운영체제는 일반 프로그램이 실행되는 공간과 Kernel이 동작하는 공간을 분리

### User Space

일반 Application이 실행되는 영역

예

```text
Chrome
VS Code
Python
Game
```

### Kernel Space

운영체제 Kernel이 실행되는 보호된 영역

전체 구조

```text
User Space

Chrome
VS Code
Python

↓ System Call

Kernel Space

Kernel

↓

Hardware
```

일반 프로그램이 Kernel Space에 자유롭게 접근할 수 있다면 하나의 프로그램 오류가 시스템 전체에 영향을 줄 수 있고 보안 문제도 발생 가능

따라서 운영체제가 영역을 분리하고 권한을 제한

## 22. System Call

Application이 Kernel에게 운영체제 기능을 요청하기 위한 방법

예를 들어 프로그램이 파일을 읽고 싶다고 가정

프로그램이 SSD를 직접 제어하는 것이 아니라 운영체제에게 요청

```text
Program
↓
"파일을 읽어줘"
↓
System Call
↓
Kernel
↓
File System / Storage
```

파일 읽기, 파일 쓰기, Process 생성, Network 사용 등 다양한 작업에서 System Call 사용

System Hacking과 Operating System 학습에서 중요하게 다루는 개념

## 23. Device Driver

Device Driver는 Operating System이 특정 Hardware를 사용할 수 있도록 연결하는 Software

예

- Graphics Driver
- Network Driver
- Printer Driver
- Audio Driver

단순화하면

```text
Application
↓
Operating System
↓
Device Driver
↓
Hardware
```

Hardware 종류마다 동작 방법이 다르기 때문에 Driver가 운영체제와 Hardware 사이의 연결 역할 수행

## 24. Program

Program은 컴퓨터가 실행할 명령어와 데이터가 저장된 것

예

```text
chrome.exe
notepad.exe
python.exe
```

Program은 아직 실행되지 않은 상태에서도 Storage에 파일 형태로 존재 가능

즉

> Program = 실행할 수 있도록 저장되어 있는 코드와 데이터

라고 이해 가능

## 25. Executable File

실행 가능한 프로그램 코드가 포함된 파일

Windows에서는 대표적으로

```text
.exe
```

확장자를 사용

예

```text
chrome.exe
notepad.exe
python.exe
```

Linux에서는 파일 이름에 `.exe`가 없어도 실행 권한과 올바른 실행 형식을 갖고 있으면 실행 가능

따라서

> 프로그램 = 무조건 `.exe` 파일

이라고 생각하면 안 됨

## 26. Process

**Process = 실행 중인 Program의 인스턴스**

저장장치에 존재하던 Program을 실행하면 Operating System이 실행에 필요한 자원을 할당하여 Process를 생성

```text
SSD

chrome.exe
Program

↓ 실행

RAM

Chrome Process
```

Process에는 일반적으로 다음과 같은 정보와 자원이 연결됨

- 실행 중인 코드
- 사용 중인 Memory
- 열린 File
- 실행 권한
- Thread
- Process ID

Program과 Process의 차이

```text
Program
→ 실행 전에도 존재할 수 있는 코드와 파일

Process
→ 실제로 실행되고 있는 프로그램
```

보안에서는 어떤 Process가 실행됐는지 확인하는 것이 매우 중요

악성코드 역시 실행되면 Process 형태로 동작하는 경우가 많음

## 27. PID

**PID = Process ID**

운영체제가 각각의 Process를 구분하기 위해 부여하는 식별 번호

예

```text
PID 1024 → chrome
PID 2048 → python
PID 3150 → vscode
```

Process 이름이 같더라도 여러 Process가 동시에 실행될 수 있기 때문에 PID를 이용하여 구분

Linux에서는 `ps` 명령 등을 이용하여 PID 확인 가능

## 28. Thread

Thread는 Process 내부에서 실제 작업을 수행하는 실행 흐름의 단위

하나의 Process가 여러 Thread를 가질 수 있음

```text
Process
│
├─ Thread 1
├─ Thread 2
└─ Thread 3
```

예를 들어 하나의 프로그램이 동시에

```text
사용자 입력 처리
파일 다운로드
화면 표시
```

등의 작업을 수행하기 위해 여러 Thread를 사용할 수 있음

기본적인 차이

```text
Process
→ 실행 중인 프로그램의 자원 단위

Thread
→ Process 내부의 실행 흐름
```

## 29. Multitasking

여러 프로그램이 동시에 실행되는 것처럼 사용할 수 있도록 하는 운영체제 기능

예

```text
Chrome 실행
VS Code 실행
Discord 실행
Music 실행
```

하나의 CPU Core가 모든 작업을 완전히 동시에 수행하는 것만을 의미하지는 않음

운영체제가 여러 Process와 Thread에 CPU 시간을 빠르게 나누어 제공하여 동시에 실행되는 것처럼 동작할 수도 있음

## 30. Scheduler

Operating System에서 어떤 Process 또는 Thread에게 CPU를 사용할 기회를 줄 것인지 결정하는 기능

예

```text
Chrome
VS Code
Discord
Python

↓ Scheduler

CPU 사용 순서와 시간 결정
```

구체적인 Scheduling Algorithm은 운영체제를 깊게 공부할 때 학습

현재는 운영체제가 CPU 자원을 여러 작업에 배분한다는 개념 이해가 우선

## 31. Context Switching

CPU가 현재 실행하던 작업을 멈추고 다른 Process 또는 Thread를 실행하기 위해 상태를 변경하는 과정

예

```text
Process A 실행
↓
A의 현재 상태 저장
↓
Process B 실행
↓
B의 상태 복원
```

나중에 다시 Process A를 실행하기 위해 기존 상태를 저장해두는 것이 중요

이러한 작업 전환 과정을 Context Switching이라고 부름

## 32. Memory

Memory라는 표현은 넓게 사용되지만 프로그램 실행 문맥에서는 일반적으로 RAM과 연결하여 생각하는 경우가 많음

실행 중인 Process는 Memory에 자신의 코드와 데이터를 저장하면서 동작

예

```text
Process
│
├─ 실행 코드
├─ 변수
├─ 함수 정보
└─ 동적으로 생성된 데이터

↓

Memory
```

System Hacking과 Reverse Engineering에서는 Memory 구조가 매우 중요

## 33. Memory Address

Memory에는 많은 데이터가 저장되기 때문에 각 데이터의 위치를 구분할 필요가 있음

이 위치를 나타내는 것이 **Memory Address**

쉽게 비유하면

```text
RAM = 매우 큰 아파트

Memory Address = 각각의 집 주소
```

Memory Address는 일반적으로 16진수로 표현하는 경우가 많음

예

```text
0x1000
0x7FF...
```

CPU는 Address를 이용하여 필요한 Memory 위치에 접근

## 34. Pointer

Pointer는 **Memory Address를 저장하는 값**

예를 들어 변수 A가 다음 위치에 있다고 가정

```text
변수 A

Address
0x1000
```

Pointer P가

```text
P = 0x1000
```

을 저장하고 있다면 P는 변수 A가 존재하는 위치를 가리키는 역할

```text
Pointer P
    │
    │ 0x1000
    ↓
Variable A
```

Pointer는 C Programming, Reverse Engineering, System Hacking에서 매우 중요한 개념

현재 단계에서는

> Pointer = 다른 데이터가 저장된 Memory Address를 가지고 있는 값

정도로 이해하면 충분

## 35. Stack

Stack은 Process가 사용하는 Memory 영역 중 하나

함수 실행과 매우 밀접한 관계 존재

대표적으로 다음 정보들이 저장될 수 있음

- 함수의 지역 변수
- 함수 호출과 관련된 정보
- 함수가 끝난 뒤 돌아갈 위치

예를 들어

```text
main()
↓
functionA() 호출
↓
functionB() 호출
```

처럼 함수가 연속해서 호출될 때 각 함수의 실행 정보가 Stack을 이용하여 관리됨

Stack은 후입선출 방식과 연결

```text
LIFO
Last In First Out
```

마지막에 들어온 것이 먼저 나가는 구조

System Hacking에서 Stack Buffer Overflow를 공부할 때 매우 중요한 개념

## 36. Heap

Heap 역시 Process가 사용하는 Memory 영역 중 하나

프로그램이 실행 중 필요한 만큼 Memory를 **동적으로 할당**할 때 사용

예를 들어 프로그램 실행 전에 필요한 데이터 크기를 정확히 알 수 없는 경우

```text
프로그램 실행

↓

1000개의 데이터를 저장할 공간 필요

↓

Heap Memory 할당
```

C에서는 대표적으로

```c
malloc()
free()
```

등을 통해 Heap Memory를 관리

System Hacking에서는 Heap 관련 취약점도 존재

현재 단계에서는

```text
Stack
→ 함수 호출 및 지역 변수와 관련

Heap
→ 실행 중 동적으로 필요한 Memory 공간과 관련
```

정도의 차이 이해가 우선

## 37. Virtual Memory

각 Process가 자신의 독립적인 Memory 공간을 가지고 있는 것처럼 사용할 수 있도록 운영체제와 CPU가 제공하는 메모리 관리 방식

예

```text
Process A
자신의 Virtual Memory

Process B
자신의 Virtual Memory
```

Process A가 Process B의 Memory를 마음대로 읽거나 수정할 수 있다면 시스템 안정성과 보안에 큰 문제가 발생

따라서 운영체제가 Process별 Memory 공간을 분리하고 보호

### Physical Memory

실제로 컴퓨터에 장착된 RAM

### Virtual Memory

각 Process가 바라보는 논리적인 Memory Address 공간

운영체제와 CPU가 Virtual Address와 Physical Memory의 연결을 관리

현재 단계에서는 내부 Page Table 구조까지 이해할 필요는 없음

## 38. Page

Virtual Memory를 일정한 크기의 작은 단위로 나누어 관리하는 개념

이러한 단위를 **Page**라고 부름

```text
Virtual Memory

├─ Page
├─ Page
├─ Page
└─ Page
```

운영체제는 Page 단위로 Memory를 관리하고 Physical Memory와 연결

세부 내용은 Operating System과 System Hacking 학습 과정에서 다시 학습 가능

## 39. File

File은 Storage에 저장된 데이터의 단위

예

```text
note.txt
photo.jpg
program.exe
report.pdf
music.mp3
```

사람에게는 서로 완전히 다른 파일처럼 보이지만 컴퓨터 입장에서는 결국 Byte의 집합

즉

```text
Text File
Image File
Executable File
PDF File

↓

모두 Byte Data
```

각 프로그램이 해당 Byte의 구조를 해석하여 문자, 사진, 프로그램 등으로 보여주는 방식

Digital Forensics에서 매우 중요한 개념

## 40. File Extension

File 이름 뒤에 붙는 확장자

예

```text
.txt
.jpg
.png
.pdf
.exe
.zip
```

확장자는 사용자와 프로그램이 파일 종류를 구분하기 쉽게 만드는 역할

하지만 확장자만 변경한다고 실제 File Data가 변경되지는 않음

예를 들어

```text
photo.jpg
```

파일 이름을

```text
photo.txt
```

로 변경해도 실제 내부 데이터가 Text File로 변하는 것은 아님

따라서 Digital Forensics에서는 확장자만 믿지 않고 실제 File Header나 File Signature 등을 확인하기도 함

## 41. Directory

Directory는 File과 다른 Directory를 관리하기 위한 구조

Windows에서는 일반적으로 Folder라는 표현을 많이 사용

예

```text
Documents
│
├─ report.pdf
├─ homework.docx
└─ security
    └─ notes.txt
```

Directory를 이용하여 File을 계층적으로 관리 가능

## 42. Path

File이나 Directory가 어디에 존재하는지 나타내는 위치

Windows 예

```text
C:\Users\dahui\Documents\test.txt
```

Linux 예

```text
/home/user/test.txt
```

### Absolute Path

파일의 전체 위치를 처음부터 나타내는 경로

```text
/home/user/test.txt
```

### Relative Path

현재 위치를 기준으로 나타내는 경로

```text
./test.txt
../test.txt
```

Linux를 사용할 때 매우 자주 등장

## 43. File System

File System은 Storage Device에 File과 Directory를 어떤 구조로 저장하고 관리할 것인지 정의하는 방식

대표적인 File System

```text
NTFS
FAT32
exFAT
ext4
APFS
```

대표적으로

```text
Windows
→ NTFS를 많이 사용

Linux
→ ext4 등을 사용

macOS
→ APFS 사용
```

File System은 다음과 같은 정보를 관리

- File 위치
- File 크기
- Directory 구조
- Permission
- Metadata
- Timestamp

Digital Forensics에서는 File System 구조를 분석하여 File과 삭제 흔적 등을 조사하는 경우가 있음

## 44. Partition

하나의 Physical Storage Device를 논리적인 여러 영역으로 나누는 것

예

```text
SSD

├─ Partition 1
├─ Partition 2
└─ Partition 3
```

각 Partition에 서로 다른 File System을 구성할 수도 있음

Windows에서 `C:`나 `D:` 같은 Drive Letter를 볼 수 있지만 Drive Letter와 Partition이 항상 완전히 같은 개념은 아님

## 45. Volume

Operating System이 하나의 저장 공간으로 인식하고 사용하는 논리적인 저장 단위

Partition과 관련되어 있지만 반드시 동일한 의미는 아님

현재 단계에서는

```text
Disk
→ Physical Storage

Partition
→ Disk를 논리적으로 나눈 영역

Volume
→ OS에서 사용 가능한 논리적 저장 공간
```

정도로 구분하면 충분

## 46. Metadata

**Metadata = Data about Data**

즉 데이터 자체가 아니라 해당 데이터에 대한 정보를 의미

예를 들어 사진 File에는 사진 이미지 데이터 이외에도 상황에 따라 다음과 같은 정보가 포함될 수 있음

- File Name
- File Size
- Created Time
- Modified Time
- Camera 정보
- 촬영 시간
- 위치 정보

Digital Forensics에서는 Metadata를 통해 File이 언제 생성되었는지, 어떤 장치에서 만들어졌는지 등의 단서를 확인할 수 있음

## 47. Timestamp

File이나 System Event와 관련된 시간 정보

File System에서는 대표적으로 다음과 같은 시간 정보를 볼 수 있음

```text
Created Time
Modified Time
Accessed Time
```

다만 실제로 어떤 Timestamp가 존재하며 언제 변경되는지는 Operating System과 File System에 따라 차이가 있음

따라서 포렌식에서는 단순히 시간 하나만 보고 판단하지 않고 여러 정보를 함께 분석

## 48. User

Operating System을 사용하는 사용자 계정

한 컴퓨터에서도 여러 User가 존재 가능

예

```text
User A
User B
Administrator
Guest
```

각 User마다 접근할 수 있는 File이나 실행할 수 있는 기능이 다르게 설정될 수 있음

## 49. Group

여러 User를 하나의 그룹으로 묶어 Permission을 관리하기 위한 개념

예

```text
developers
students
administrators
```

각 User에게 Permission을 하나씩 설정하는 대신 Group에 Permission을 설정하여 여러 User를 동시에 관리할 수 있음

Linux에서 특히 자주 사용

## 50. Permission

User나 Process가 특정 File 또는 System Resource에 어떤 행동을 할 수 있는지를 결정하는 권한

대표적으로

```text
Read
Write
Execute
```

Linux에서는 다음 문자로 표현

```text
r = Read
w = Write
x = Execute
```

예를 들어

```text
Read 가능
Write 불가능
Execute 가능
```

처럼 사용자마다 다른 Permission을 가질 수 있음

보안에서 Permission 관리가 중요한 이유는 사용자가 필요 이상의 권한을 가지면 공격자가 해당 계정을 탈취했을 때 더 많은 작업을 수행할 수 있기 때문

## 51. Owner / Group / Others

Linux File Permission에서 자주 사용하는 구분

```text
Owner
Group
Others
```

### Owner

File을 소유한 User

### Group

해당 File과 연결된 Group

### Others

Owner와 Group에 해당하지 않는 나머지 User

각 대상에게 서로 다른 Read, Write, Execute Permission을 설정 가능

## 52. Administrator와 root

Operating System에서 강력한 관리 권한을 가진 계정

Windows에서는

```text
Administrator
```

Linux에서는

```text
root
```

라는 표현을 주로 사용

관리자 권한으로는 일반 User보다 더 많은 시스템 작업 수행 가능

예

- 시스템 설정 변경
- 프로그램 설치
- 다른 User 관리
- 중요한 File 수정
- Process 관리

보안에서는 공격자가 일반 User 권한을 얻은 뒤 관리자 권한을 획득하려는 공격이 자주 등장

이를 **Privilege Escalation**이라고 부름

## 53. Privilege

User 또는 Process가 System에서 가지고 있는 권한

예

- 특정 File 읽기
- File 수정
- 프로그램 설치
- Process 종료
- System 설정 변경

### Least Privilege

**Principle of Least Privilege**

사용자나 프로그램에게 작업에 필요한 최소한의 권한만 제공하는 보안 원칙

예를 들어 단순히 문서를 읽어야 하는 프로그램에게 System 전체 관리자 권한을 줄 필요는 없음

권한이 클수록 보안 사고 발생 시 피해 범위도 커질 수 있음

## 54. Authentication과 Authorization

컴퓨터 시스템과 보안에서 매우 중요한 두 개념

### Authentication

**인증**

사용자가 누구인지 확인하는 과정

쉽게 표현하면

```text
"너 누구야?"
```

예

```text
ID + Password
Fingerprint
OTP
```

### Authorization

**인가 또는 권한 확인**

인증된 사용자가 특정 행동을 수행할 수 있는지 판단하는 과정

쉽게 표현하면

```text
"너 이 작업 해도 돼?"
```

예

```text
일반 사용자
→ 게시글 읽기 가능
→ 관리자 페이지 접근 불가

관리자
→ 사용자 관리 가능
```

두 개념을 구분하는 것이 중요

```text
Authentication
→ 누구인지 확인

Authorization
→ 무엇을 할 수 있는지 확인
```

## 55. Source Code

Programmer가 사람이 읽을 수 있는 Programming Language로 작성한 코드

Python 예

```python
print("Hello")
```

C 예

```c
#include <stdio.h>

int main() {
    printf("Hello");
    return 0;
}
```

CPU가 이러한 Source Code를 그대로 직접 이해하는 것은 아님

CPU가 실행 가능한 형태로 변환하는 과정 필요

## 56. Machine Code

CPU가 직접 실행할 수 있는 형태의 명령어

Binary 형태의 데이터로 존재

사람이 직접 읽고 작성하기에는 매우 어려움

개념적으로

```text
Source Code
↓
변환
↓
Machine Code
↓
CPU 실행
```

## 57. Assembly Language

Machine Code를 사람이 비교적 이해하기 쉬운 형태로 표현한 저수준 언어

예

```asm
mov
add
cmp
jmp
call
ret
```

Assembly와 Machine Code는 CPU Architecture와 밀접한 관련 존재

Reverse Engineering에서는 실행 파일을 분석하여 Assembly Code를 확인하는 경우가 많음

관계를 단순화하면

```text
Python / C
고수준 언어

↓

Assembly
저수준 언어

↓

Machine Code

↓

CPU
```

## 58. Compiler

Compiler는 Source Code를 다른 형태의 코드로 변환하는 프로그램

C의 경우 일반적으로 다음과 같은 흐름으로 이해 가능

```text
C Source Code

↓

Compiler 등의 Build 과정

↓

Executable / Machine Code

↓

CPU 실행
```

사람이 작성한 C Code를 CPU가 실행할 수 있는 형태로 변환하는 과정

## 59. Interpreter

Source Code를 실행하기 위한 방식 중 하나

Python은 일반적으로 Interpreter를 이용하여 실행하는 언어로 설명됨

예

```text
Python Source Code
↓
Python 실행 환경
↓
코드 실행
```

실제 현대 Programming Language의 구현에서는 Bytecode, Virtual Machine, JIT 등 여러 기술이 함께 사용될 수 있기 때문에

```text
Compiled Language
Interpreter Language
```

를 완전히 단순한 두 종류로만 나누기보다는 입문 단계에서 실행 방식의 차이를 이해하는 것이 중요

## 60. Library

자주 사용하는 기능을 미리 구현해놓은 Code의 모음

Programmer가 모든 기능을 처음부터 직접 만들 필요 없이 Library의 기능을 가져와 사용 가능

Python 예

```python
import os
import json
```

Library를 이용하면 기존에 만들어진 기능을 재사용 가능

## 61. API

**API = Application Programming Interface**

Software가 다른 Software의 기능을 사용할 수 있도록 정해놓은 사용 방법 또는 인터페이스

API는 Web에서만 사용하는 개념이 아님

예

```text
Operating System API
Library API
Web API
```

프로그램이 다른 System이나 Program의 기능을 사용할 수 있도록 약속된 방식이라고 이해 가능

## 62. Runtime

Program이 실제로 실행되는 환경 또는 실행 과정에서 필요한 구성 요소와 관련된 용어

예

```text
Java Runtime
.NET Runtime
Python Runtime
```

문맥에 따라 정확한 의미가 달라질 수 있지만 기본적으로 프로그램이 실제로 실행되는 환경이라는 개념으로 이해 가능

## 63. CLI

**CLI = Command Line Interface**

문자 기반 명령어를 이용하여 컴퓨터를 조작하는 방식

예

```bash
cd
ls
pwd
python
```

GUI와 달리 Mouse와 Button보다 Command 입력을 중심으로 사용

정보보안과 Linux에서는 CLI를 사용하는 일이 매우 많음

## 64. GUI

**GUI = Graphical User Interface**

Window, Icon, Button, Mouse 등의 그래픽 요소를 이용하여 컴퓨터를 사용하는 방식

예

- Windows Desktop
- File Explorer
- Settings
- Web Browser 화면

일반 사용자는 GUI를 많이 사용하지만 Server, Linux, 보안 도구에서는 CLI를 자주 사용

## 65. Shell

Shell은 사용자가 입력한 Command를 해석하고 Operating System의 기능을 사용할 수 있도록 하는 프로그램

대표적인 Shell

```text
Bash
Zsh
PowerShell
cmd
```

예를 들어 Shell에서

```bash
cd Documents
```

를 입력하면 Shell이 Command를 해석하여 현재 Directory를 변경

Linux를 공부할 때 Bash를 자주 사용하게 됨

Windows에서는 PowerShell을 많이 접할 수 있음

## 66. Terminal

Terminal은 Shell을 사용할 수 있도록 화면과 입력 환경을 제공하는 프로그램

즉

```text
Terminal
→ 명령어를 입력할 수 있는 창

Shell
→ 입력된 명령어를 해석하는 프로그램
```

두 용어가 일상적으로 비슷하게 사용되기도 하지만 정확히 같은 개념은 아님

## 67. Environment Variable

Operating System과 Program이 사용하는 환경 설정값

대표적인 예

```text
PATH
HOME
TEMP
```

### PATH

Command를 입력했을 때 Operating System이 실행할 프로그램을 찾을 Directory 목록과 관련

예를 들어 Terminal에서

```bash
python
```

이라고 입력했을 때 현재 Directory에 `python.exe`가 없어도 PATH에 등록된 위치에서 실행 파일을 찾을 수 있음

프로그램 설치 후

```text
PATH 설정이 필요합니다
```

같은 말을 보는 이유와 연결

## 68. Service와 Daemon

사용자가 직접 화면에서 조작하지 않더라도 Background에서 계속 실행되며 특정 기능을 제공하는 Program

Windows에서는 주로

```text
Service
```

Linux/Unix 계열에서는

```text
Daemon
```

이라는 표현을 많이 사용

예

```text
Web Server
SSH Server
Database Server
Logging Service
```

사용자가 화면을 열어두지 않아도 Background Process 형태로 계속 실행 가능

## 69. Booting

컴퓨터 전원을 켠 뒤 Operating System이 실행되어 사용할 수 있는 상태가 되는 과정

전체 과정을 매우 단순화하면

```text
Power ON

↓

BIOS / UEFI

↓

Hardware 초기화

↓

Boot Device 확인

↓

Bootloader 실행

↓

Kernel 실행

↓

Operating System 시작
```

이 전체 과정을 Booting이라고 부름

## 70. BIOS와 UEFI

컴퓨터 전원을 켰을 때 가장 먼저 실행되는 Firmware 환경

현대 PC에서는 주로 **UEFI** 사용

주요 역할

- Hardware 초기화
- 기본 Hardware 상태 확인
- Boot Device 확인
- Operating System 실행 준비

BIOS는 이전부터 사용된 방식이며 UEFI는 이를 대체하는 현대적인 Firmware Interface

## 71. Firmware

Hardware에 매우 가까운 수준에서 장치를 제어하는 Software

예

```text
SSD Firmware
Router Firmware
UEFI Firmware
Keyboard Firmware
```

일반 Application보다 Hardware 동작에 직접적인 영향을 주는 Software

Hardware와 Software 사이의 연결 역할을 하는 개념으로 이해 가능

## 72. POST

**POST = Power-On Self-Test**

컴퓨터가 켜질 때 기본 Hardware 상태 등을 검사하는 과정

예

- CPU
- Memory
- 기본 장치

등이 정상적으로 초기화될 수 있는지 확인하는 과정과 관련

## 73. Bootloader

Operating System Kernel을 Memory에 올리고 실행할 수 있도록 준비하는 Program

Boot 과정에서 Firmware 다음 단계에서 동작

Linux에서는 대표적으로

```text
GRUB
```

을 접할 수 있음

단순화하면

```text
UEFI
↓
Bootloader
↓
Kernel
↓
Operating System
```

## 74. 32bit와 64bit

CPU와 Operating System, Program이 데이터를 처리하고 Memory Address를 다루는 구조와 관련된 구분

현대 PC는 대부분 64bit 환경 사용

보안 공부에서는 다음 표현을 자주 볼 수 있음

```text
x86
x86-64
AMD64
x64
```

64bit 환경에서는 32bit 환경보다 훨씬 큰 Address 공간을 사용할 수 있음

Reverse Engineering에서는 32bit Program과 64bit Program의 Register와 Assembly 구조가 다를 수 있기 때문에 중요

## 75. Computer Architecture

Computer Architecture는 컴퓨터가 어떻게 구성되고 명령어를 어떻게 처리하는지 정의하는 구조

CPU 문맥에서는 특히 CPU가 사용하는 **Instruction Set Architecture**와 연결되어 사용

대표적인 Architecture

```text
x86
x86-64
ARM
ARM64
```

서로 다른 Architecture에서는 사용할 수 있는 Machine Instruction 등이 달라질 수 있음

예를 들어 스마트폰에서는 ARM 계열을 많이 사용하고 PC에서는 x86-64 계열을 많이 사용

Reverse Engineering에서 분석 대상 Program의 Architecture를 확인하는 이유도 여기에 있음

## 76. Endianness

여러 Byte로 구성된 데이터를 Memory에 어떤 순서로 저장할 것인지 결정하는 방식

대표적인 두 방식

```text
Little Endian
Big Endian
```

예를 들어 여러 Byte로 이루어진 숫자를 저장할 때 Byte 순서가 달라질 수 있음

x86과 x86-64 Architecture에서는 일반적으로 Little Endian 사용

Reverse Engineering, Digital Forensics, Network Data 분석 등에서 Byte 순서를 해석할 때 중요

현재는 두 방식이 존재한다는 사실과 Byte 저장 순서에 관한 개념이라는 정도로 이해하면 충분

## 77. Compression

데이터를 더 작은 크기로 표현하는 과정

대표적인 압축 형식

```text
ZIP
7z
gzip
```

### Lossless Compression

압축을 풀었을 때 원래 데이터를 완전히 복원 가능

예

- ZIP
- PNG

### Lossy Compression

일부 정보를 제거하여 데이터 크기를 크게 줄이는 방식

원본과 완전히 동일하게 복원할 수 없음

예

- JPEG
- MP3

Digital Forensics에서는 압축된 File 내부를 분석하는 상황도 자주 발생

## 78. Hash

Hash Function은 입력 데이터를 일정한 길이의 값으로 변환하는 함수

```text
Original Data

↓

Hash Function

↓

Hash Value
```

대표적인 Hash Algorithm

```text
SHA-256
SHA-3
```

Hash의 중요한 특징 중 하나는 입력 데이터가 조금만 변경되어도 일반적으로 매우 다른 Hash Value가 만들어진다는 점

예

```text
file1
↓
SHA-256
↓
Hash A

file1에서 1Byte 수정
↓
SHA-256
↓
Hash B
```

활용

- File 동일성 확인
- Data 무결성 확인
- Digital Forensics 증거 확인
- Software Download 검증

Hash는 Encryption과 다른 개념

Encryption은 Key를 사용하여 원래 데이터를 복원하는 것을 전제로 하지만 Hash는 일반적으로 원본 복원을 위한 기능이 아님

## 79. Log

컴퓨터 System이나 Program에서 발생한 Event를 기록한 데이터

예

```text
사용자 로그인
로그아웃
Program 실행
File 접근
오류 발생
System 시작
System 종료
```

System이 정상적으로 동작할 때도 Log가 남을 수 있고 공격이나 오류가 발생했을 때도 기록이 남을 수 있음

따라서 보안에서는 Log를 분석하여

```text
누가 로그인했는가?

언제 실행됐는가?

어떤 Program이 실행됐는가?

어떤 오류가 발생했는가?
```

등을 조사

침해사고 대응과 Digital Forensics에서 매우 중요한 데이터

## 80. Backup

중요한 Data가 손상되거나 삭제될 상황을 대비해 별도의 복사본을 만들어두는 것

Backup이 필요한 상황

- Storage Device 고장
- 실수로 File 삭제
- Malware 감염
- Ransomware
- System 장애

중요한 Data는 하나의 Storage에만 존재하게 하는 것보다 Backup을 통해 복구 가능성을 높이는 것이 중요

## 81. Error와 Exception

### Error

Program이나 System에서 발생하는 문제를 넓게 표현하는 용어

예

```text
File 없음
Memory 부족
잘못된 입력
Network 문제
```

### Exception

Program 실행 과정에서 발생한 예외적인 상황을 Programming Language가 처리하기 위한 개념

Python 예

```python
try:
    number = int(input())
except ValueError:
    print("숫자를 입력해야 함")
```

Exception Handling을 사용하면 예상 가능한 오류 상황을 Program에서 처리 가능

## 82. CPU Usage와 Memory Usage

Windows 작업 관리자 등에서 확인 가능한 System Resource 사용량

### CPU Usage

CPU가 현재 얼마나 작업을 처리하고 있는지를 나타내는 지표

```text
CPU 10%
CPU 70%
CPU 100%
```

### Memory Usage

현재 RAM이 얼마나 사용되고 있는지를 나타내는 지표

### Disk Activity

Storage Device에서 Data를 읽거나 쓰는 작업 상태

보안 분석에서도 특정 Process가 CPU나 Memory를 비정상적으로 많이 사용하는지 확인하는 경우 존재

# 프로그램 하나를 실행하면 어떤 일이 발생하는가

앞에서 배운 개념을 하나의 흐름으로 연결하면 컴퓨터 동작을 이해하기 쉬움

예를 들어 사용자가 `program.exe`를 실행한다고 가정

```text
1. program.exe가 SSD에 저장되어 있음

                ↓

2. 사용자가 Program 실행

                ↓

3. Operating System이 Executable File 확인

                ↓

4. 새로운 Process 생성

                ↓

5. Program 실행에 필요한 Code와 Data를 RAM에 배치

                ↓

6. Process에 Virtual Memory 공간 제공

                ↓

7. CPU가 Program의 Instruction 실행

                ↓

8. CPU가 계산 과정에서 Register 사용

                ↓

9. Function 실행 과정에서 Stack 사용

                ↓

10. 필요한 경우 Heap에 Memory 동적 할당

                ↓

11. File 또는 Hardware가 필요하면 System Call 사용

                ↓

12. Kernel이 요청을 처리

                ↓

13. Program 실행 결과 화면 출력

                ↓

14. Program 종료 시 Process와 사용 Resource 정리
```

이 흐름을 이해하면 여러 컴퓨터 개념이 각각 독립적인 용어가 아니라 하나의 시스템으로 연결되어 있다는 것을 이해할 수 있음

# 정보보안과 컴퓨터 기초의 연결

정보보안에서는 정상적인 컴퓨터의 동작을 이해한 뒤 비정상적인 동작을 찾아내는 경우가 많음

예를 들어

```text
정상

일반 User
↓
허용된 Permission
↓
File 접근
```

공격자는 다음과 같은 상황을 만들려고 할 수 있음

```text
일반 User

↓

취약점 이용

↓

Administrator / root 권한 획득
```

또는 Malware 분석에서는

```text
어떤 Process가 실행됐는가?

어떤 File을 만들었는가?

어떤 Memory를 사용했는가?

어떤 권한으로 실행됐는가?
```

등을 확인

Digital Forensics에서는

```text
어떤 File이 존재했는가?

File Metadata는 무엇인가?

Timestamp는 언제인가?

File System에 어떤 흔적이 남았는가?
```

등을 분석

Reverse Engineering에서는

```text
CPU는 어떤 Instruction을 실행하는가?

Register에는 어떤 값이 들어 있는가?

Memory에는 어떤 Data가 존재하는가?

Program의 실행 흐름은 어떻게 구성되어 있는가?
```

등을 분석

따라서 컴퓨터 기초는 보안과 별개의 공부가 아니라 앞으로 배우게 될 보안 기술을 이해하기 위한 기반

# 현재 단계에서 우선적으로 이해할 개념

처음부터 모든 내용을 암기할 필요 없음

다음 개념은 앞으로 계속 등장하므로 우선적으로 익숙해지는 것이 중요

## 1순위

```text
Hardware
Software

Bit
Byte
Binary
Hexadecimal

CPU
Register
RAM
SSD

Program
Process
Thread

Operating System
Kernel

Memory
Memory Address

File
Directory
Path
File System

User
Permission
Administrator / root

CLI
Shell
```

## 2순위

```text
Cache
Core
System Call
Driver

Stack
Heap
Pointer
Virtual Memory

Metadata
Timestamp

Group
Owner

Compiler
Interpreter
Machine Code
Assembly

Environment Variable
Service / Daemon

32bit / 64bit
Architecture
Endianness
```

## 나중에 깊게 공부할 내용

현재는 개념만 이해하고 이후 Operating System, Reverse Engineering, System Hacking 등을 공부하면서 깊게 학습

```text
CPU 내부 구조
CPU Instruction Set
Register 세부 역할
Cache 구조

Process Scheduling Algorithm
Context Switching 내부 구조

Virtual Memory
Page Table
Memory Mapping

Stack Frame
Heap 내부 구조

File System 내부 구조
NTFS / ext4 구조

Kernel 내부 구조
System Call 내부 동작
```

# 핵심 정리

컴퓨터 전체 구조를 가장 간단하게 연결하면 다음과 같음

```text
[저장]

SSD / HDD

Program
File
Data 저장


        ↓ Program 실행


[작업 공간]

RAM

Process의 Code와 Data 저장


        ↓


[실행]

CPU

Instruction 실행
Register 사용


        ↓


[관리]

Operating System

Process 관리
Memory 관리
File 관리
User 관리
Permission 관리
Device 관리


        ↓


[운영체제 핵심]

Kernel

CPU
Memory
File System
Device

등 핵심 System Resource 관리
```

정보보안을 공부하면서 가장 중요한 질문

```text
이 Program은 무엇을 실행하는가?

어떤 Process가 만들어졌는가?

어떤 User가 실행했는가?

어떤 Permission을 가지고 있는가?

어떤 File에 접근했는가?

Memory에 어떤 Data가 존재하는가?

CPU는 어떤 Instruction을 실행하는가?
```

이러한 질문에 답하기 위해 컴퓨터의 구조와 동작 방식을 이해하는 것이 중요
