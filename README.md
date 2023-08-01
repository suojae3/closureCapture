<br/><br/>


## 왜 closure에서 weak self를 선언해야할까?

<br/>

### 목차
- [클로저의 캡쳐현상](#클로저의-캡쳐)
---

### 클로저의 캡쳐
&nbsp;&nbsp;&nbsp;&nbsp;<img src="capture list.webp"><br/><br/>


1. 클로저는 기본적으로 RAM 메모리 공간 중 Heap에 저장된다
2. 클로저는 메모리 주소를 가지고 있고 실행하면 바로 코드영역의 주소를 찾아간다
3. 즉 클로저는 클래스처럼 Reference Type(참조형식)으로 Swift의 ARC모델에 의해 메모리 관리가 된다.

