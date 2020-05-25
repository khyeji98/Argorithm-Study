# Argorithm-Study

### 정렬
**- [K번째 수](#K번째-수)**

***

## 정렬

### K번째 수

*Solution 1*

```
import Foundation

func solution(_ array:[Int], _ commands:[[Int]]) -> [Int] {
    
    var answer = [Int]()
    
    for i in commands {
        var array1 = Array(array[i[0]-1...i[1]-1])
        array1.sort()
        
        answer.append(array1[i[2]-1])
    }
    return answer
}
```

*Solution 2*

```
import Foundation

func solution(_ array:[Int], _ commands:[[Int]]) -> [Int] {
    
    return commands.map{let i = $0[0]-1; let j = $0[1]-1; let k = $0[2]-1
                        return array[i...j].sorted()[k]}

} // 세미콜론(;) : 한 라인에 여러 명령을 사용하고 싶을 때 사용
```

*Study - 배열 선언 및 초기화*

```
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

*Study - 배열 map, filter, reduce*

```

```
