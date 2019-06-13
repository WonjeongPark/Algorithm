# 문제
https://programmers.co.kr/learn/courses/30/lessons/42585?language=javascript
```
여러 개의 쇠막대기를 레이저로 절단하려고 합니다.
효율적인 작업을 위해서 쇠막대기를 아래에서 위로 겹쳐 놓고, 레이저를 위에서 수직으로 발사하여 쇠막대기들을 자릅니다.
쇠막대기와 레이저의 배치는 다음 조건을 만족합니다.

- 쇠막대기는 자신보다 긴 쇠막대기 위에만 놓일 수 있습니다.
- 쇠막대기를 다른 쇠막대기 위에 놓는 경우 완전히 포함되도록 놓되, 끝점은 겹치지 않도록 놓습니다.
- 각 쇠막대기를 자르는 레이저는 적어도 하나 존재합니다.
- 레이저는 어떤 쇠막대기의 양 끝점과도 겹치지 않습니다.

아래 그림은 위 조건을 만족하는 예를 보여줍니다.
수평으로 그려진 굵은 실선은 쇠막대기이고, 점은 레이저의 위치, 수직으로 그려진 점선 화살표는 레이저의 발사 방향입니다.
```
![쇠막대기 알고리즘 이미지](https://grepp-programmers.s3.amazonaws.com/files/ybm/dbd166625b/d3ae656b-bb7b-421c-9f74-fa9ea800b860.png)
```
이러한 레이저와 쇠막대기의 배치는 다음과 같이 괄호를 이용하여 왼쪽부터 순서대로 표현할 수 있습니다.

(a) 레이저는 여는 괄호와 닫는 괄호의 인접한 쌍 '()'으로 표현합니다. 또한 모든 '()'는 반드시 레이저를 표현합니다.
(b) 쇠막대기의 왼쪽 끝은 여는 괄호 '('로, 오른쪽 끝은 닫힌 괄호 ')'로 표현됩니다.

위 예의 괄호 표현은 그림 위에 주어져 있습니다.
쇠막대기는 레이저에 의해 몇 개의 조각으로 잘리는데,
위 예에서 가장 위에 있는 두 개의 쇠막대기는 각각 3개와 2개의 조각으로 잘리고,
이와 같은 방식으로 주어진 쇠막대기들은 총 17개의 조각으로 잘립니다.

쇠막대기와 레이저의 배치를 표현한 문자열 arrangement가 매개변수로 주어질 때,
잘린 쇠막대기 조각의 총 개수를 return 하도록 solution 함수를 작성해주세요.
```
## 제한사항
```
arrangement의 길이는 최대 100,000입니다.
arrangement의 여는 괄호와 닫는 괄호는 항상 쌍을 이룹니다.
```
### 입출력 예
```
arrangement	        return
()(((()())(())()))(())	17
```
# Try!
## 내가 알고 있는 것
`막대기는 (에서 시작해서 )로 끝난다.`<br>
`(는 바로 뒤에 )가 나올 경우 한쌍으로 레이저를 뜻한다.`<br>
`(가 나오다가 ()레이저가 나오면 (의 개수만큼 잘린 쇠막대기의 수가 증가하고,`<br>
`레이저에 해당하지 않는 부분의 )는 잘려나갈 쇠막대기의 수를 1씩 감소시킨다.`<br>

## 정답
## No
```
function solution(arrangement) {
    let result = 0
    let st = []
    for(let i=0; i<arrangement.length; i++){
        if(arrangement[i] === '('){
            st.push(arrangement[i])
        } else {
            st.pop()
            if(arrangement[i-1] === '('){
                result += st.length;
            } 
        }
        
    }
    return result
}
```
## YES
```
function solution(arrangement) {
    let result = 0
    let st = []
    for(let i=0; i<arrangement.length; i++){
        if(arrangement[i] === '('){
            st.push(arrangement[i])
        } else {
            st.pop()
            if(arrangement[i-1] === '('){
                result += st.length;
            } else result += 1
        }
        
    }
    return result
}
```

## 후기
처음엔 어떻게 풀어야할지도 감이 안잡혔지만 인터넷에서 약간의 힌트를 얻어서 풀었다.<br>
( 바로 뒤에 나오는 )가 아닌 )여도 쇠막대기의 끝을 뜻하므로 +1 해줘야한다!<br>
처음엔 이해하고 어떻게 풀어야하는지 생각하는 시간이 조금 걸렸지만<br>
복잡한 문제에 비해 생각보다 난이도가 낮은 것 같다.<br>
<br>
