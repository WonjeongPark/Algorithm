# 문제
https://programmers.co.kr/learn/courses/30/lessons/42840?language=javascript
```
수포자는 수학을 포기한 사람의 준말입니다.
수포자 삼인방은 모의고사에 수학 문제를 전부 찍으려 합니다.
수포자는 1번 문제부터 마지막 문제까지 다음과 같이 찍습니다.

1번 수포자가 찍는 방식: 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...
2번 수포자가 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ...
3번 수포자가 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...

1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때,
가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return 하도록 solution 함수를 작성해주세요.
```
## 제한사항
```
시험은 최대 10,000 문제로 구성되어있습니다.
문제의 정답은 1, 2, 3, 4, 5중 하나입니다.
가장 높은 점수를 받은 사람이 여럿일 경우, return하는 값을 오름차순 정렬해주세요.
```
### 입출력 예
```
answers	      return
[1,2,3,4,5]	[1]
[1,3,2,4,2]	[1,2,3]
```
### 입출력 예 설명
```
수포자 1은 모든 문제를 맞혔습니다.
수포자 2는 모든 문제를 틀렸습니다.
수포자 3은 모든 문제를 틀렸습니다.
따라서 가장 문제를 많이 맞힌 사람은 수포자 1입니다.
```
```
모든 사람이 2문제씩을 맞췄습니다.
```
# Try!
## 내가 알고 있는 것
` 각각의 수포자들의 배열 패턴 알아낸 후 answers와 비교하여 맞힌 문제 수를 알아내자 `
## 내가 애매하게 알고 있는 것
` 맞힌 문제 개수가 아닌 많이 맞힌 사람을 배열에 담아야 하므로
마지막 부분을 수정해야한다`<br>
` 배열은 0부터 시작이니 n, n+1을 헷갈리지 말고 차근차근 풀어야한다`
`supo3의 배열 패턴을 다시 생각해보기`

## 정답
## No
```
function solution(answers) {
var arr1 = new Array;
    arr1[0]=1;
for(var n=1; n <answers.length;n++){
    if((n+1)%5==0){
      arr1[n]=5}
    else {arr1[n]=(n+1)%5;}
};
    
var arr2 = new Array;
for(var m=0;m<answers.length;m++){
  if((m+1)%2==1){arr2[m]=2}
    else if((m+1)%8==0){
      arr2[m]=5
  }else if ((m+1)%6==0){
      arr2[m]=4
  }else if ((m+1)%4==0){
      arr2[m]=3
  }else if ((m+1)%2==0){
      arr2[m]=1
  }
};
    
var arr3 = new Array;
for(var l=0;l<answers.length;l++){
if((l+1)%9==0||(l+1)%9==1){
    arr3[l]=5
}else if((l+1)%7==0||(l+1)%7==1){
    arr3[l]=4
}else if ((l+1)%5==0||(l+1)%5==1){
    arr3[l]=2
}else if ((l+1)%3==0||(l+1)%3==1){
    arr3[l]=1
}else{arr3[l]==3}
}
var supo1 = 0;
var supo2 = 0;
var supo3 = 0;

for(var i=0; i<answers.length;i++){
    if(arr1[i] == answers[i]){
        supo1++;
    };
    if(arr2[i] == answers[i]){
        supo2++;
    };
    if(arr3[i] == answers[i]){
        supo3++;
    }
    var myArray = [supo1, supo2, supo3]
    
    }var answer = Math.max.apply(null, myArray);
    return answer[];
}
```
## YES
```
function solution(answers) {
var arr1 = new Array;
    arr1[0]=1;
for(var n=1; n <answers.length;n++){
    if((n+1)%5==0){
      arr1[n]=5}
    else {arr1[n]=(n+1)%5;}
};
    
var arr2 = new Array;
for(var m=0;m<answers.length;m++){
  if((m+1)%2==1){arr2[m]=2}
    else if((m+1)%8==0){
      arr2[m]=5
  }else if ((m+1)%6==0){
      arr2[m]=4
  }else if ((m+1)%4==0){
      arr2[m]=3
  }else if ((m+1)%2==0){
      arr2[m]=1
  }
};
    
var arr3 = new Array;
for(var l=0;l<answers.length;l++){
if((l+1)%10==1||(l+1)%10==2){
    arr3[l]=3
}else if((l+1)%10==3||(l+1)%10==4){
    arr3[l]=1
}else if ((l+1)%10==5||(l+1)%10==6){
    arr3[l]=2
}else if ((l+1)%10==7||(l+1)%10==8){
    arr3[l]=4
}else{arr3[l]==5}}
    
    var supo1 = 0;
    var supo2 = 0;
    var supo3 = 0;
    
for(var i=0; i<answers.length;i++){

    if(arr1[i] == answers[i]){
        supo1++;
    }}
for(var i=0; i<answers.length;i++){
    if(arr2[i] == answers[i]){
        supo2++;
    }}
for(var i=0; i<answers.length;i++){
    if(arr3[i] == answers[i]){
        supo3++;
    }}

    var answer = []
    
    if(supo1>=supo2 && supo1>=supo3){
        answer.push(1) 
    }
    if(supo2>=supo3 && supo2>=supo1){
        answer.push(2)
    }
    if(supo3>=supo1 && supo3>=supo2){
        answer.push(3)
    }    
    return answer;
} 
```

### 후기

`난이도가 쉬운 문제라서 이미 다른사람들이 푼 정답이나 힌트를 보지않고 푼 문제`<br>
`이 쾌감을 기억해서 알고리즘 푸는 동안 더 집중하자`<br>
`더 짫고 간단한 풀이가 없는지 생각해보기`<br>
`기본적인 것들은 기억하기`<br><br>
