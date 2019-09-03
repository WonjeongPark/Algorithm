# 문제
https://programmers.co.kr/learn/courses/30/lessons/42627?language=javascript
```
하드디스크는 한 번에 하나의 작업만 수행할 수 있습니다.
디스크 컨트롤러를 구현하는 방법은 여러 가지가 있습니다. 가장 일반적인 방법은 요청이 들어온 순서대로 처리하는 것입니다.

예를들어
- 0ms 시점에 3ms가 소요되는 A작업 요청
- 1ms 시점에 9ms가 소요되는 B작업 요청
- 2ms 시점에 6ms가 소요되는 C작업 요청
와 같은 요청이 들어왔습니다. 이를 그림으로 표현하면 아래와 같습니다
```
![힙1](https://github.com/WonjeongPark/Algorithm/blob/master/009/%ED%9E%991.png?raw=true)
<br>
`한 번에 하나의 요청만을 수행할 수 있기 때문에 각각의 작업을 요청받은 순서대로 처리하면 다음과 같이 처리 됩니다.`
<br>
![힙2](https://github.com/WonjeongPark/Algorithm/blob/master/009/%ED%9E%992.png?raw=true)
<br>
```
- A: 3ms 시점에 작업 완료 (요청에서 종료까지 : 3ms)
- B: 1ms부터 대기하다가, 3ms 시점에 작업을 시작해서 12ms 시점에 작업 완료(요청에서 종료까지 : 11ms)
- C: 2ms부터 대기하다가, 12ms 시점에 작업을 시작해서 18ms 시점에 작업 완료(요청에서 종료까지 : 16ms)
```
```
이 때 각 작업의 요청부터 종료까지 걸린 시간의 평균은 10ms(= (3 + 11 + 16) / 3)가 됩니다.
하지만 A → C → B 순서대로 처리하면
```
![힙3](https://github.com/WonjeongPark/Algorithm/blob/master/009/%ED%9E%993.png?raw=true)
```
- A: 3ms 시점에 작업 완료(요청에서 종료까지 : 3ms)
- C: 2ms부터 대기하다가, 3ms 시점에 작업을 시작해서 9ms 시점에 작업 완료(요청에서 종료까지 : 7ms)
- B: 1ms부터 대기하다가, 9ms 시점에 작업을 시작해서 18ms 시점에 작업 완료(요청에서 종료까지 : 17ms)
```
```
이렇게 A → C → B의 순서로 처리하면 각 작업의 요청부터 종료까지 걸린 시간의 평균은 9ms(= (3 + 7 + 17) / 3)가 됩니다.

각 작업에 대해 [작업이 요청되는 시점, 작업의 소요시간]을 담은 2차원 배열 jobs가 매개변수로 주어질 때,
작업의 요청부터 종료까지 걸린 시간의 평균을 가장 줄이는 방법으로 처리하면 평균이 얼마가 되는지 return 하도록 solution 함수를 작성해주세요.
(단, 소수점 이하의 수는 버립니다)
```
## 제한사항
```
jobs의 길이는 1 이상 500 이하입니다.
jobs의 각 행은 하나의 작업에 대한 [작업이 요청되는 시점, 작업의 소요시간] 입니다.
각 작업에 대해 작업이 요청되는 시간은 0 이상 1,000 이하입니다.
각 작업에 대해 작업의 소요시간은 1 이상 1,000 이하입니다.
하드디스크가 작업을 수행하고 있지 않을 때에는 먼저 요청이 들어온 작업부터 처리합니다.
```
### 입출력 예
```
jobs	                        return
[[0, 3], [1, 9], [2, 6]]	9
```
### 입출력 예 설명
```
문제에 주어진 예와 같습니다.

0ms 시점에 3ms 걸리는 작업 요청이 들어옵니다.
1ms 시점에 9ms 걸리는 작업 요청이 들어옵니다.
2ms 시점에 6ms 걸리는 작업 요청이 들어옵니다.
```

# Try!
## 정답
## No
```
function solution(jobs) {
    var arr= []
    var arr2 = jobs;
    arr.push(arr2.shift());
    arr2.sort((a,b)=>a[1]-b[1])
    for(var i=0; i<arr2.length+1; i++){
        if(arr[i][1]>=arr2[i][0]){
            arr.push(arr2.shift());
        }arr.push(arr2.shift());
    }
    var temp = 0;
    var temp2 = 0;
    var temp3 =0;
    for (var j=0; j<arr.length; j++){
        temp += arr[j][1]
    temp2 += temp;
        temp3 += arr[j][0]
    var answer;
        answer = (temp2-temp3)/arr.length;     
    } 
    return answer;
}
```
## YES
(프로그래머스 답)
```
function solution (jobs) {
    jobs.sort((a, b) => a[0] - b[0])

    const len = jobs.length
    let past = jobs[0][0]
    const queue = []

    function enqueue () {
        if (jobs.length === 0) return
        let idx = jobs.findIndex(j => j[0] > past)
        if (idx === -1) idx = jobs.length
        queue.push(...jobs.splice(0, idx))
    }

    function dequeue () {
        queue.sort((a, b) => b[1] - a[1])
        return queue.pop()
    }

    let total = 0
    while (jobs.length || queue.length) {
        enqueue()
        const job = dequeue()
        past += job[1]
        total += past - job[0]
        if (queue.length === 0 && jobs.length > 0 && jobs[0][0] > past) past = jobs[0][0]
    }

    return ~~(total / len)
}
```

## 후기
힙! 새로운 개념이다. 완전 이진 트리구조로 최댓값, 최솟값 구하기 쉬운 구조.<br>
sort 하는 방법은 잘 생각해낸 것 같은데 예시로 나온 값에만 성공이고 채점은 엉망이었다. 
정답 예처럼 queue에 해당하는 배열을 잘 넣는 법(jobs[0][0]보다 큰 인덱스 범위 지정) 
그것을 sorting 하여 pop 하는 법을 함수로 잘 정리하여 정해진 범위에서 간단하게 함수를 실행하여 값을 구하는 것을 잘 봐 둬야 겠다.<br><br>
예를 들면 jobs[1]의 값인 [0,3]이 수행되고 나서 다음으로 수행될 수 있는 것들은 3 이전에 요청이 온 값들 중에서 수행 시간이 짧은 것이어야 한다. 
jobs[i][1]의 값들을 sorting 하면서 그것이 모든 jobs[i][0]에서 적용 될것이 아니라 3이전에 요청 온 것과 같이 범위를 한정하는 게 어려웠고 
늘 알고리즘을 풀면서 놓치고 있는 부분인 if (idx === -1) idx = jobs.length와 같은 예외 처리도 잘 생각해야겠다.
