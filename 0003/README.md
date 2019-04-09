# 문제 [해시]
https://programmers.co.kr/learn/courses/30/lessons/42578?language=javascript
```
스파이들은 매일 다른 옷을 조합하여 입어 자신을 위장합니다.

예를 들어 스파이가 가진 옷이 아래와 같고 오늘 스파이가 동그란 안경, 긴 코트, 파란색 티셔츠를 입었다면
다음날은 청바지를 추가로 입거나 동그란 안경 대신 검정 선글라스를 착용하거나 해야 합니다.

종류	이름
얼굴	동그란 안경, 검정 선글라스
상의	파란색 티셔츠
하의	청바지
겉옷	긴 코트

스파이가 가진 의상들이 담긴 2차원 배열 clothes가 주어질 때
서로 다른 옷의 조합의 수를 return 하도록 solution 함수를 작성해주세요.
```
## 제한사항
```
clothes의 각 행은 [의상의 이름, 의상의 종류]로 이루어져 있습니다.
스파이가 가진 의상의 수는 1개 이상 30개 이하입니다.
같은 이름을 가진 의상은 존재하지 않습니다.
clothes의 모든 원소는 문자열로 이루어져 있습니다.
모든 문자열의 길이는 1 이상 20 이하인 자연수이고 알파벳 소문자 또는 '_' 로만 이루어져 있습니다.
스파이는 하루에 최소 한 개의 의상은 입습니다.
```
### 입출력 예
```
clothes	                                                                           return
[[yellow_hat, headgear], [blue_sunglasses, eyewear], [green_turban, headgear]]            5
[[crow_mask, face], [blue_sunglasses, face], [smoky_makeup, face]]	                  3 
```
### 입출력 예 설명
```
예제 #1
headgear에 해당하는 의상이 yellow_hat, green_turban이고 eyewear에 해당하는 의상이 blue_sunglasses이므로
아래와 같이 5개의 조합이 가능합니다.

1. yellow_hat
2. blue_sunglasses
3. green_turban
4. yellow_hat + blue_sunglasses
5. green_turban + blue_sunglasses
```
```
예제 #2
face에 해당하는 의상이 crow_mask, blue_sunglasses, smoky_makeup이므로 아래와 같이 3개의 조합이 가능합니다.

1. crow_mask
2. blue_sunglasses
3. smoky_makeup
```
# Try!
## 생각과정

**[[의상이름,의상종류],[의상이름,의상종류]...]중에서 서로 다른 조합의 수는<br>
[(같은 의상의종류의 수+1)x(같은 의상의종류의 수+1)...]-1 로 구할 수 있다.<br>
각 의상의 종류의 수에 1을 더하는 것은 그 의상을 입지 않았을 경우의 수를 추가하는 것이고<br>
마지막의 -1는 각각 의상을 입지않아 모든 것을 입지않은 경우를 빼는 것이다.<br>
의상의 종류로 구분해서 경우의 수를 구해야할 듯 싶다.**
<br>

## 정답

## YES
```
function solution(clothes) {
    var answer = 1;
    var obj = {}
    clothes.forEach(function(element){
        if(obj[element[1]]>=1){
            obj[element[1]] += 1}
        else{
            obj[element[1]] = 1}
    })
    for(var x in obj){
        answer *= (obj[x]+1)}
        return answer-1;
}
```

**element[1]은 의상의 종류를 뜻한다.(따라서 element[0]은 의상의 이름)<br>
의상의 종류를 key값으로 사용하여 존재(>=1)하면 +1을 해주고<br>
그렇지 않다면 1로 초기화해준다.<br>
그렇게 구한 값에 각각 1을 더하여 곱해준 값 answer에 -1을 해주면 답이 나온다.<br>**

## 후기
```
var person = {
  name : "Jay",
  gender : "female"
};
 
console.log( person.name, person.gender );
// 결과 : Jay female

var key1 = 'name', key2 = 'gender';
 
console.log( person[key1], person[key2] );
// 결과 : Jay female
```
위의 예처럼 Object의 key를 변수로 받을 수 있다.<br>
obj[element[1]]의 값이 >=1이 아닌 값들도 1로 정해야 곱한 값을 구할 때 영향이 없다.<br>
(answer이 1인 이유도 마찬가지이다.)<br>
