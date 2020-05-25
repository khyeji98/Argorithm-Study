# Argorithm-Study

### 정렬
**- [K번째 수](#K번째-수)**

***

## 정렬

### K번째 수

*Solution 1*
```Swift
import Foundation

func solution(_ array:[Int], _ commands:[[Int]]) -> [Int] {
    
    var answer = [Int]()
    
    for i in commands {
        var array1 = Array(array[i[0]-1...i[1]-1])
        array1.sort()
        
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
