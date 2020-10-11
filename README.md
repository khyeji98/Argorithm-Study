# Argorithm-Study

### [기본 데이터 구조의 활용](#기본-데이터-구조)
### [고급 데이터 구조의 활용](#고급-데이터-구조)

### 정렬
- [K번째수](#K번째수)
- [가장큰수](#가장큰수)

### 완전탐색
- [모의고사](#모의고사)

***

## 기본 데이터 구조

## 고급 데이터 구조
### 반복기, 시퀀스, 컬렉션

### 스택

### 큐
- 입력된 데이터가 먼저 출력되는 것을 반복하는 FIFO(First-in-First-out) 데이터 구조
- 맨 앞 요소 = head
- 맨 앞 요소가 제거됨 = pop
- 맨 뒤 요소가 추가됨 = push
    - enqueue() : 큐 맨뒤에 새로운 요소 추가(push)
    - dequeue() : 큐에서 첫번째 요소 제거하고 반환(pop)
    - peek() : 큐의 첫번째 요소를 반환하지만 제거하지는 않음
    - clear() : 큐를 재설정해 비어있는 상태로 만듬
    - count : **큐에 있는 요소의 수를 반환**
    - isEmpty()/isFull() : 큐가 비어있는지/꽉 차있는지 확인
    - capacity : 큐 용량을 가져오거나 설정하기 위한 read/write 프로퍼티(**배열 속에 담을 수 있는 요소의 수 반환**)
    - insert()/removeArIndex() : 큐의 특정 인덱스 위치에 요소 삽입/제거
- 구현 방법 : 배욜을 래핑하고 접근자 매소드를 통해 큐의 속성을 나타냄

### 순환 버퍼(=원형 큐)
- 고정된 크기의 배열 사용하고, 배열이 큐의 값들로 가득 차면 헤드 인덱스 0으로 돌아감

## 정렬

### K번째수
: 내 생각을 기반으로 다른 솔루션을 참고

*Solution 1*
```Swift
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
func solution(_ array:[Int], _ commands:[[Int]]) -> [Int] {
    
    return commands.map({key in array[(key[0]-1...key[1]-1)].sorted()[key[2]-1]})
    // 클로저가 함수에 대한 유일한 인자일 경우, ()괄호를 생략할 수 있으므로 본 코드에서 ()괄호를 생략해도 실행 가능
    // .map{key in array[key[0]-1...key[1]-1].sorted()[key[2]-1]}
}
```

*Solution 3*
```Swift
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
func solution(_ numbers:[Int]) -> String {

    var sortedNum = numbers.sorted{Int("\($0)\($1)")! > Int("\($1)\($0)")!} // 1. 가장 큰 수 찾기
    
    let answer = sortedNum.map{String($0)}.reduce(""){$0 + $1} // 2. 가장 큰 수를 String으로 조합
    
    return answer.hasPrefix("0") == true ? "0" : answer // 3. 결과가 0인지 확인
}
```
*Solution 2*
```Swift
func solution(_ numbers:[Int]) -> String {
    
    let sortedNumbers = numbers.sorted { Int("\($0)\($1)")! > Int("\($1)\($0)")! } // 옵셔널 강제추출안하면 에러!
    // sortedNumbers 는 Array<Int> 타입
    
    if sortedNumbers[0] == 0 {
        return "0"
    } // 정렬된 배열의 $0값이 0이면 모든 배열의 값이 0이라는 것이므로 0을 return
    
    return sortedNumbers.reduce("") { "\($0)" + "\($1)" } // ""은 초기값이므로 반드시 명시해야 함
}
```
*Solution 3*
```Swift
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

## 완전탐색

### 모의고사

*Error 1*
```Swift
func solution(_ answers:[Int]) -> [Int] {
    
    let firstAnswer: [Int] = [1, 2, 3, 4, 5]
    let secondAnswer: [Int] = [2, 1, 2, 3, 2, 4, 2, 5]
    let thirdAnswer: [Int] = [3, 3, 1, 1, 2, 2, 4, 4, 5, 5]
    
    var firstScore: Int = 0
    var secondScore: Int = 0
    var thirdScore: Int = 0
    
    for i in answers {
        if firstAnswer[(i % firstAnswer.count)] == answers[i] {
            firstScore += 1
        }
        if secondAnswer[(i % secondAnswer.count)] == answers[i] {
            secondScore += 1
        }
        if thirdAnswer[(i % thirdAnswer.count)] == answers[i] {
            thirdScore += 1
        }
    }
    
    if firstScore > secondScore {
        if firstScore > thirdScore {
            return [1]
        } else if thirdScore > firstScore {
            return [3]
        } else if firstScore == thirdScore {
            return [1, 3]
        } else {  return [] }
    } else if secondScore > firstScore {
        if secondScore > thirdScore {
            return [2]
        } else if secondScore == thirdScore {
            return [2, 3]
        } else { return [] }
    } else if firstScore == secondScore {
        if firstScore > thirdScore {
            return [1, 2]
        } else if firstScore < thirdScore {
            return [3]
        } else { return [] }
    }
    return []
} // signal: illegal instruction (core dumped)
```

*Solution 1*
```Swift
func solution(_ answers:[Int]) -> [Int] {
    let answer = (
        first : [1, 2, 3, 4, 5],
        second : [2, 1, 2, 3, 2, 4, 2, 5],
        third : [3, 3, 1, 1, 2, 2, 4, 4, 5, 5]
    )
    var result = [1:0, 2:0, 3:0]

    for (index, value) in answers.enumerated() {
        if answer.first[index % 5] == value {
            result[1]! += 1
        }
        if answer.second[index % 8] == value {
            result[2]! += 1
        }
        if answer.third[index % 10] == value {
            result[3]! += 1
        }
    }
    
    return result.sorted{ $0.key > $1.key }.filter{ $0.value == result.values.max() }.map{ $0.key }
}
```
