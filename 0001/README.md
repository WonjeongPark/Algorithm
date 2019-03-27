# 문제
https://programmers.co.kr/learn/courses/30/lessons/42576
```
수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.
마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때,
완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.
```
## 제한사항
```
마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
completion의 길이는 participant의 길이보다 1 작습니다.
참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
참가자 중에는 동명이인이 있을 수 있습니다.
```
### 입출력 예
```
participant..........................	completion.............................return
["leo", "kiki", "eden"]	                ["eden", "kiki"]                	"leo"
["marina", "josipa", "nikola", "vinko"]	["josipa", "marina", "nikola"]  	"vinko"
["mislav", "stanko", "mislav", "ana"] 	["stanko", "ana", "mislav"]	        "mislav"
```
### 입출력 예 설명
```
예제 #1
"leo"는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.

예제 #2
"vinko"는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.

예제 #3
"mislav"는 참여자 명단에는 두 명이 있지만, 완주자 명단에는 한 명밖에 없기 때문에 한명은 완주하지 못했습니다.
```

# Try!
## 내가 알고 있는 것
`배열끼리 비교, 1:1로 제거하고 남은 것을 출력하자 `
## 내가 애매하게 알고 있는 것
`두개의 length가 1차이이므로 sort()해서 정렬하고 비교! `<br>

##정답
## No
```
function solution(participant, completion) {
    var participant = [];
    var completion = [];
    
    for(var i=0;i<100000; i++){
        for(var j=0;j<99999; j++){
            if(participant[i]=completion[j]){
                var removedItem1= participant.splice(i,1);
                var removedItem2= completion.splice(j,1);
            }
        }
    }
    var answer = 'participant[0]';
    return answer;
}
```


>복잡하게 이중 for을 두개 돌려 같은 것을 제거해야한다고 생각<br>
>같은 것을 제거하는 것이 아니라 같은 것을 비교하여 다른 것을 출력해야한다<br>

```
function solution(participant, completion) {
    for(var i=0;i<participant.length; i++){
            if(participant[i] !== completion[i]){
                return participant[i];
            }
    }
}
```
>천천히 다시 코드를 읽어보다가 정렬해야한다는 사실을 깨닫고 sort를 적용


## YES
```
function solution(participant, completion) {
    participant.sort();
    completion.sort();
    
    for(var i=0;i<participant.length; i++){
            if(participant[i] !== completion[i]){
                return participant[i];
            }
    }
}
```
