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
` `
## 내가 애매하게 알고 있는 것
` `<br>
` `

## 정답
## No
```
function solution(answers) {
var arr1 = new Array;
    
for(var n=0; n <answers.length;n++){
    if(n=1){arr1[n]=1}
    else if(n%5==0){
      arr1[n]=5}
    else {arr1[n]=(n+1)%5;}
};
    
var arr2 = new Array;
for(var m=0;m<answers.length;m++){
  if(m%2==1){arr2[m]=2}
    else if(m%8==0){
      arr2[m]=5
  }else if (m%6==0){
      arr2[m]=4
  }else if (m%4==0){
      arr2[m]=3
  }else if (m%2==0){
      arr2[m]=1
  }
};
    
var arr3 = new Array;
for(var l=0;l<answers.length;l++){
if(l%9==0||l%9==1){
    arr3[l]=5
}else if(l%7==0||l%7==1){
    arr3[l]=4
}else if (l%5==0||l%5==1){
    arr3[l]=2
}else if (l%3==0||l%3==1){
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
[정답]
```
