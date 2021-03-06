+++
date = "2016-10-11T16:36:39+08:30"
draft = true 
title = "동시성(Concurrency) 프로그래밍"
authors = ["Sangbae Yun"]
categories = ["How-to"]
tags = ["beginning"]
series=["Go 시작하기"]
toc = false
+++

## 동시성에 대해서
Go 언어의 장점을 이야기 할 때 빠지지 않는 특징이 "동시성을 잘 지원한다"이다. 동시성 프로그래밍 ? 병렬 프로그래밍과 다른건가 ? 헷갈린다. 먼서 동시성과 병렬성에 대해서 살펴보자.

동시성은 **여러 코드가 동시에 실행 할 수 있게 설계되어 있는지**에 대한 것이다. 논리적인 실행 환경인 셈이다. 병렬성은 **물리적인 컴퓨터가 어떻게 코드를 동시에 실행 하게 할 것인지**에 대한 것이다. 물리적인 실행 환경이다. 아래 그림을 보자.

## 고루틴(goroutines) 
커다란 프로그램들은 종종 여러 개의 작은 서브 프로그램들로 이루어지곤 한다. 예를 들어 웹 서버 프로그램의 경우 웹브라우저의 요청을 읽고 처리하기 위해서, **요청 별로** 여러 개의 핸들러를 운용하곤 한다. 핸들러는 각각의 요청을 처리하기 위한 조그마한 프로그램(코드)들이다. 

이들 조그마한 프로그램들은 동시에 여러개가 실행될 수 있어야 한다. 예컨데, 웹 서버를 개발한다면 많은 유저의 요청을 처리 할 수 있도록 즉, 핸들러가 동시에 두 개 이상이 실행될 수 있도록 해야 한다. 이때 사용하는 프로그래밍 기법이 앞서 다루었던 **동시성**이다. Go언어에서는 고루틴(goroutines)와 채널(channels)를 이용해서 동시성 프로그램을 개발 할 수 있다. 

**go**키워드를 이용하면 코드 내에서 다른 코드(함수)를 실행 할 수 있다. 
```go
```
## 고루틴과 쓰레드
C나 Java의 쓰레드와 매우 비슷하다는 느낌이 들 것이다. 고루틴과 스레드와의 차이점을 3가지 카테고리에서 살펴볼 것이다.

### 메모리 소비
쓰레드 하나를 만들기 위해서는 대략 1MB의 정도의 메모리가 필요하다. 고루틴은 2kB 정도의 스택공간으로 시작 할 수 있다.

거의 1/500 정도로 가볍기 때문에 요청 하나 당 하나의 고루틴을 만들어도 문제 없이 작동한다. 10000 개의 고루틴이 실행되도, 200M 정도의 메모리만 소비할 뿐이다. 허나 쓰레드는 만드는 데만 10G의 공간이 필요하며, 개발자는 **OutOfMemoryError**를 신경서야 한다. 

### 생성 및 삭제 비용 
쓰레드는 운영체제에서 관리하는 자원이므로, 생성과 삭제를 하려면 운영체제에 요청을 해야 한다.

## 참고
  * [An Introduction to Programming in Go](https://www.golang-book.com/books/intro/10)
  * [How Goroutines Work](http://blog.nindalf.com/how-goroutines-work/)
