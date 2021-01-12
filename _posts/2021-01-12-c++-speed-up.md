---
layout: post
title: ios::sync_with_stdio(false), cin.tie(NULL)
subtitle: C++로 알고리즘 풀 때  실행 속도 높이기
tags: [C++]
---


### ios::sync_with_stdio

C언어의 stdio와 C++의 iosteam을 동기화하는 역할을 한다  

stdio와 iosteam의 버퍼를 모두 사용하기 때문에 딜레이가 생기는데, false로 하면 동기화가 비활성화되고 C++의 버퍼만 생성돼서 C언어의 버퍼와 같이 사용 못 한다  

그로 인해 버퍼의 수가 줄어들어서 실행속도가 향상된다는 장점이 있다  

하지만 동기화가 비활성화되어서 멀티쓰레드 환경에서는 출력 순서가 다르게 나올수있다  

또, 버퍼가 분리되어서 C언어와 C++의 printf, scanf / cin, cout을 함께 사용하면 안 된다  
  

### cin.tie(NULL)  

cin, cout은 하나의 스트림에 묶여있고 묶여있는 스트림들은 하나의 스트림이 다른 스트림에서 각 입출력 작업을 진행하기 전에 자동으로 버퍼를 비운다  

```c++
cout << "output";
cin >> input;
```
  
cin과 cout이 묶여있기 때문에, input을 입력하기 전에 "output " 구문이 먼저 출력된다  

cin.tie(null)을 추가하면 cin과 cout의 묶음이 풀리면서 "output" 구문이 출력되지도 않았는데 이름을 입력을 받는 경우가 생긴다  

이것은 cout이 기본적으로 버퍼에 추가되고 바로 비워지지 않기 때문이다 (출력 명령을 내리거나 버퍼가 가득 찼을 때만 버퍼를 비우고 출력한다)
