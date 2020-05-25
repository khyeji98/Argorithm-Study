# Argorithm-Study

### 정렬
**- [K번째수](#K번째수)**
**- [가장큰수](#가장큰수)**

***

## 정렬

### K번째수
: 내 생각을 기반으로 다른 솔루션을 찹고

*Solution 1*
```Swift
import Foundation

func solution(_ array:[Int], _ commands:[[Int]]) -> [Int] {
    
    var answer = [Int]()
    
    for i in commands {
        var array1 = Array(array[i[0]-1...i[1]-1])
        array1.sorted()
        
        answer.append(array1[i[2]-1]) // append는 배열에 원소를 추가하는 method
    }
    return answer
}
```

*Solution 2*
```Swift
import Foundation

func solution(_ array:[Int], _ commands:[[Int]]) -> [Int] {
    
    return commands.map({key in array[(key[0]-1...key[1]-1)].sorted()[key[2]-1]})
    // 클로저가 함수에 대한 유일한 인자일 경우, ()괄호를 생략할 수 있으므로 본 코드에서 ()괄호를 생략해도 실행 가능
    // .map{key in array[key[0]-1...key[1]-1].sorted()[key[2]-1]}
}
```

*Solution 3*
```Swift
import Foundation

func solution(_ array:[Int], _ commands:[[Int]]) -> [Int] {
    
    return commands.map{let i = $0[0]-1; let j = $0[1]-1; let k = $0[2]-1 // 세미콜론(;) : 한 라인에 여러 명령을 사용하고 싶을 때 사용
                        return array[i...j].sorted()[k]} // 함수가 단일 명령문이 아니므로 return 생략 불가능

} 
```

*Study - 배열 선언 및 초기화*
```Swift
// 비어있는 배열 선언

var exmaple: Array<Int> = Array()
var example: Array<Int> = []
var example = Array<Int>()
var example: [Int] = []
var example = [Int]()

// 배열 선언과 동시에 값넣기

var example = [values]
var exmaple = Array(values)
```

*Study - map*

`.map`은 컨테이너의 각각의 값을 매개변수를 받아 함수에 적용시켜 새로운 컨테이너를 생성하는 것.   
> for-in 구문을 함축시켜 놓은 것과 같다.   
> 실행 시간이 단축된다.

### 가장큰수
: 처음엔 자릿수마다의 조건문을 만들어야하나 생각하다가 다른 솔루션을 보고 이해하는 방식으로 공부함

*Solution 1*
```Swift
import Foundation

func solution(_ numbers:[Int]) -> String {
    
    let sortedNumbers = numbers.sorted { Int("\($0)\($1)")! > Int("\($1)\($0)")! } // 옵셔널 강제추출안하면 에러!
    // sortedNumbers 는 Array<Int> 타입
    
    if sortedNumbers[0] == 0 {
        return "0"
    } // 정렬된 배열의 $0값이 0이면 모든 배열의 값이 0이라는 것이므로 0을 return
    
    return sortedNumbers.reduce("") { "\($0)" + "\($1)" } // ""은 초기값이므로 반드시 명시해야 함
}
```

*Solution 2*
```Swift
import Foundation

func solution(_ numbers:[Int]) -> String {
    
    let sortedNumbers = numbers.sorted { Int("\($0)\($1)")! > Int("\($1)\($0)")! } 
    
    let answer = sortedNumbers.map { String($0) }.reduce("") { $0 + $1 }
    
    return sortedNumbers.first == 0 ? "0" : answer // Solution 1의 if문과 같은 비슷한 맥락
}
```
> **앞뒤값을 비교할 수도 있지만 앞뒤값 조합 두가지의 차가 0보다 큰지를 이용해 정렬할 수도 있음**

*Study - reduce*

`.reduce`는 전달받는 연산법으로 각 배열의 모든 값을 combine
> sort와 map처럼 for-in loop문을 함축시킨 것.   
> 초기값을 꼭 설정해줘야 함.

*Study - sort VS sorted*

`.sort`는 원본 배열도 변경되지만, `.sorted`는 정렬된 사본 배열을 반환해주는 것이라는데 본 문제에서 `.sort`를 사용했을 때 왜 에러나는지 아직 모름.
