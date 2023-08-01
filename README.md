<br/><br/>


## 왜 closure에서 [weak self]를 선언해야할까?

<br/>

### 목차
- [클로저의 캡쳐현상](#클로저의-캡쳐)
---

### 클로저의 캡쳐

<br/>

&nbsp;&nbsp;&nbsp;&nbsp;<img src="capture list.webp" width="600" height="400"><br/><br/>

1. 클로저는 기본적으로 RAM 메모리 공간 중 Heap에 저장된다 (클로저는 기본적으로 변수에 함수를 담는 것)
2. 클로저는 메모리 주소를 가지고 있고 실행하면 바로 코드영역의 주소를 찾아간다
3. 즉 클로저는 클래스처럼 Reference Type(참조형식)으로 Swift의 ARC모델에 의해 메모리 관리가 된다.

<br/>

```swift
var sum = 0

func multipleFunc(a: Int, b: Int) -> Int { 
    sum = sum + (a * b)                    
    return sum                             
}

let closureFunc = multipleFunc //100 (주소)

closureFunc(1, 2) //2
closureFunc(2, 3) //8
closureFunc(3, 4) //20 (값이 누적되고 있다!)
```
1. 위 코드에서 `multipleFunc()`이 실행되려면 반드시 `sum`이 필요하다
2. 따라서 클로저함수는 외부변수를 **capture** 하게 된다.
3. 즉 함수가 외부에 있는 변수를 사용하면서 특정 변수에 다시 그 함수를 담을 때 외부 변수가 같이 담겨버리는 현상이다

<br/>

```swift
func calculateFunc() -> ((Int) -> (Int)) {

    var sum = 0

    func square(num: Int) -> Int {
        sum += (num * num)
        return sum
    }

    return square
}
```


