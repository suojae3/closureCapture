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
3. 즉 클로저는 클래스처럼 Reference Type(참조형식)으로 Swift의 ARC(automatic reference counting) 모델에 의해 메모리 관리가 된다.

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

var sqaureFunc = calculateFunc()

squareFunc(10) //100
squareFunc(20) //400
squareFunc(30) //900
```
1. Heap 영역은 Stack 영역보다 메모리를 더 길게 가지고 간다
2. 위의 코드에서 `calculateFunc()`는 Stack에, 클로저로 쓰이고 있는 `square()`는 Heap에 저장된다
3. `sqaure()`는 Heap영역에서 Stack영역에 있는 `calculate()`의 `sum`을 참조(refer)하고 있다.
4. 이때 `calculate()` 가 종료되면 Stack영역에서 사라짐에 따라 참조하고 있던 `sum`도 메모리에서 사라진다
5. 이를 대비해서 클로저인 `square()`는 Heap에다 미리 `sum`의 값을 저장하게 되는데 이것이 바로 **Capture**이다
6. 따라서 closure가 capture한 값은 변수명만 같을 뿐 Heap영역에 따로 저장되기 때문에 결과값이 누적이 되는 모습을 보여준다








