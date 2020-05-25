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

```

**배열 선언 및 초기화**

