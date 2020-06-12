---
author: "Kyongsub Kong"
date: 2020-05-16
linktitle: Python 가상 개발환경 구축
menu:
  main:
    parent: tutorials
next: /tutorials/
prev: /tutorials/python-virtual-environment
title: Python 개발 가상환경 구축
weight: 10
---

Python은 한 가지에 중점 되어 있지 않고 다방면(웹, 모바일, 데스크탑)에서 사용이 가능한 프로그래밍 언어이며, 설치하기 쉽고 복잡하지 않아 개발자 뿐만 아니라 초보자들에게도 사용하기 적절한 언어입니다. 현재 2020년 5월 기준 Python 3이 가장 최신 버전입니다. 

자, 이제 리눅스 환경에서 파이썬3 개발용 가상환경을 터미널을 이용해 세팅을 해볼 겁니다. 이 글에 사용되는 OS는 Ubuntu 18.04 lts 버전이며 다른 Debian Linux 환경에도 똑같이 적용이 가능합니다.  


## 1단계 - Python 3 설치
### python
마우스를 이용해 브라우저를 통해 설치 하는 방법보다 터미널 이용해 간단한 명령어를 입력시켜 설치를 해 볼 것입니다. 

Command line (a.k.a Shell)은 이용자가 간단한 명령어를 통해 설치나 변경, 사용 등등 여러가지 일을 손쉽게 사용할 수 있게 해줍니다.

Ubuntu 18.04 lts 환경에서는 왼쪽 상단 Activities를 클릭하면 중앙 상단에 검색어 입력창이 나오는데 검색어 입력창에 "terminal"를 입력하시면 터미널을 실행 시키실 수 있습니다. 간단한 단축키(Ctrl + Alt + T)를 이용해 바로 실행 시키실 수도 있습니다.

Ubuntu 18.04 버전에서는 Python 2와 Python 3가 기본적으로 설치가 되어 있는데 최신 버전으로 업데이트를 시켜 줍니다.

```tpl
example@example:~$ sudo apt-get update
```

```tpl
example@example:~$ sudo apt-get -y upgrade
```

여기서 -y를 모든 아이템들 설치한다는 명령어 입니다.
설치가 완료 되면 Python 3의 버전을 명령어를 통해서 확인해 볼 수 있습니다.

```tpl
example@example:~$ python3 --version
```

명령어를 입력하면 아래와 같은 결과를 보여줄겁니다. 버전은 시기에 따라 조금씩 다르지만 지금 보시는 결과가 최신 버전이라고 생각하시면 됩니다.

```tpl
example@example:~$ python3 --version
Python 3.6.7
example@example:~$
```


### pip
Python 소프트웨어 패키지를 설치나 관리를 하기 위해 pip를 설치 해줍니다.

```tpl
example@example:~$ sudo apt-get install -y python3-pip
```

Python 패키지를 설치를 하시려면 pip 명령어를 사용하셔서 사용하시면 됩니다.



## 2단계 -가상환경 세팅

일단 가상환경이 왜 필요한가?
Python 프로젝트를 진행하는 과정에서 여러가지 패키지들을 설치를 하는데 동시에 몇가지의 프로젝트를 진행한다면 서로 방해가 될 수 있습니다. 또한, 버전 관리에도 훨씬 편리하기 때문에 프로젝트를 진행하는 동안 개별 가상환경을 구축해 사용하시는게 좋습니다.

디렉토리 하나를 생성하면서 이 디렉토리가 하나의 가상환경 역할을 하도록 세팅하는 것 입니다.

### venv

```tpl
example@example:~$ sudo apt-get install -y python3-venv
```

mkdir 명령어를 이용해 새로운 디렉토리를 생성해 주고 해당 디렉토리로 이동해 줍니다.

```tpl
example@example:~$ mkdir example
example@example:~$ cd example
example@example:~/example$
```

해당 디렉토리에서 가상환경을 생성해 줍니다.

```tpl
example@example:~$ python3 -m venv venv
```

이 과정에서 ls 명령어로 확인할 수 있는 필수적인 몇가지의 아이템들이 생성이 됩니다.

```tpl
example@example:~$ ls venv
Output
bin include lib lib64 pyvenv.cfg share
```

이것들은 시스템 파일과 프로젝트 파일이 공유 되지 않고 독단적으로 가상환경이 구동될 수 있도록 합니다. 프로젝트에 따라 각각 다른 패키지들이 설치가 가능하고 다른 버전들의 패키지들이 설치 될 수 있게 도와줍니다.

가상환경을 실행하기 위해 명령어를 입력해 줍니다. 가상환경이 실행되면 앞쪽에 괄호안에 가상환경 이름이 나타납니다.

```tpl
example@example:~$ source venv/bin/activate
(venv) example@example:~/example$
```


## 3단계 -테스트
### 간단한 예제 프로그램 생성 및 실행

가상환경이 잘 작동이 되는 지를 확인해 보기 위해 “Hello, World”가 프린트 되는 간단한 프로그램을 만들어 봅시다.

일단 nano 명령어를 이용해 py 파일을 생성하고 실행해 봅시다. (터미널을 통해 코드를 작성할 수 있음)

```tpl
(venv) example@example:~/example$ nano greeting.py
```

nano 명령어는 실행하는 명령어 이지만 해당 파일이 존재 하지 않을 경우 생성과 동시에 실행이 되니 이점 유의해 주시기 바랍니다.

텍스트 파일이 실행이 되면 아래 코드를 작성하고 Control + X 를 사용하고 Y를 눌러서 저장해 줍니다. 그리고 Enter 키를 누르시면 다시 디렉토리 돌아옵니다.


```tpl
print("Hello, World!")
```

그러면 우리가 작성한 프로그램을 실행해 봅시다.

```tpl
(venv) example@example:~/example$ python greeting.py
Hello, World!
```

가상환경을 종료하시려면 deactivate 명령어를 입력하시면 됩니다.

```tpl
(venv) example@example:~/example$ deactivate
```

여기까지 Ubuntu 18.04 lts 혹은 linux에서 Python 가상 개발환경 구축과 간단한 프로그램 작성 및 실행을 해보았습니다.