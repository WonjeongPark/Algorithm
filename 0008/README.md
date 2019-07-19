# 문제
https://programmers.co.kr/learn/courses/30/lessons/42586
```
프로그래머스 팀에서는 기능 개선 작업을 수행 중입니다. 각 기능은 진도가 100%일 때 서비스에 반영할 수 있습니다.

또, 각 기능의 개발속도는 모두 다르기 때문에 뒤에 있는 기능이 앞에 있는 기능보다 먼저 개발될 수 있고,

이때 뒤에 있는 기능은 앞에 있는 기능이 배포될 때 함께 배포됩니다.

먼저 배포되어야 하는 순서대로 작업의 진도가 적힌 정수 배열 progresses와

각 작업의 개발 속도가 적힌 정수 배열 speeds가 주어질 때

각 배포마다 몇 개의 기능이 배포되는지를 return 하도록 solution 함수를 완성하세요.
```
## 제한사항
```
작업의 개수(progresses, speeds배열의 길이)는 100개 이하입니다.

작업 진도는 100 미만의 자연수입니다.

작업 속도는 100 이하의 자연수입니다.

배포는 하루에 한 번만 할 수 있으며, 하루의 끝에 이루어진다고 가정합니다.

예를 들어 진도율이 95%인 작업의 개발 속도가 하루에 4%라면 배포는 2일 뒤에 이루어집니다.
```
### 입출력 예
```
progresses	speeds	        return
[93,30,55]	[1,30,5]	[2,1]
```
### 입출력 예 설명
```
첫 번째 기능은 93% 완료되어 있고 하루에 1%씩 작업이 가능하므로 7일간 작업 후 배포가 가능합니다.

두 번째 기능은 30%가 완료되어 있고 하루에 30%씩 작업이 가능하므로 3일간 작업 후 배포가 가능합니다.

하지만 이전 첫 번째 기능이 아직 완성된 상태가 아니기 때문에 첫 번째 기능이 배포되는 7일째 배포됩니다.

세 번째 기능은 55%가 완료되어 있고 하루에 5%씩 작업이 가능하므로 9일간 작업 후 배포가 가능합니다.

따라서 7일째에 2개의 기능, 9일째에 1개의 기능이 배포됩니다.
```
# Try!
## 내가 알고 있는 것
` `
## 내가 애매하게 알고 있는 것
` `<br>
` `

## 정답
## No
```
function solution(progresses, speeds) {
    var answer = [];
    var keep = [];
    for(var i=0;i<progresses.length;i++){
        var needDay = (100-progresses[i])/speeds[i];
        if((100-progresses[i])%speeds[i]!=0){
            needDay ++;
            keep.unshift(needDay);
        }
    while(keep.length>0){
        var init = keep.pop();
        var count = 1;
        while(keep.length>0 && init >= keep.peek()){
            keep.pop();
            count++;
        }
        answer.unshift(count);
    }
    }
    return answer;
}
```
## YES
```
function solution(progresses, speeds) {
    var answer = [];

    while(speeds.length > 0) {
        // 개발
        for(let i in speeds) {
            if(progresses[i] < 100) {
                progresses[i] += speeds[i];
            }
        }

        // 배포
        let deploy_count = 0;
        while(progresses[0] >= 100) {
            progresses.shift();
            speeds.shift();
            deploy_count++;
        }
        if(deploy_count > 0) {
            answer.push(deploy_count);
        }
    }

    return answer;
}
```

## 후기
복잡하게 생각할 필요가 없었다. 큐의 가장 기본을 잊고있었기 때문이다.<br><br>
progresses가 100이 넘는 순간 list와 speeds의 수를 구하는건 어렵지 않았고,<br>
앞부분도 100이 넘어야 100이 넘는 뒷부분도 출력하는 과정을 괜히 복잡하게 생각해서 고민했다.<br>
큐 배열의 첫 번째 부분이 100이 넘어 shift하면 두 번째부분이 앞으로 밀리기 때문에<br>
while(progresses[0] >=100) ~ 부분의 [0]을 변수가 아닌 0으로 두어도 되는 부분을 잘 기억해두자.<br>
