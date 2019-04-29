# 문제
https://programmers.co.kr/learn/courses/30/lessons/42579
```
스트리밍 사이트에서 장르 별로 가장 많이 재생된 노래를 두 개씩 모아 베스트 앨범을 출시하려 합니다.
노래는 고유 번호로 구분하며, 노래를 수록하는 기준은 다음과 같습니다.

속한 노래가 많이 재생된 장르를 먼저 수록합니다.
장르 내에서 많이 재생된 노래를 먼저 수록합니다.
장르 내에서 재생 횟수가 같은 노래 중에서는 고유 번호가 낮은 노래를 먼저 수록합니다.
노래의 장르를 나타내는 문자열 배열 genres와 노래별 재생 횟수를 나타내는 정수 배열 plays가 주어질 때,
베스트 앨범에 들어갈 노래의 고유 번호를 순서대로 return 하도록 solution 함수를 완성하세요.
```
## 제한사항
```
genres[i]는 고유번호가 i인 노래의 장르입니다.
plays[i]는 고유번호가 i인 노래가 재생된 횟수입니다.
genres와 plays의 길이는 같으며, 이는 1 이상 10,000 이하입니다.
장르 종류는 100개 미만입니다.
장르에 속한 곡이 하나라면, 하나의 곡만 선택합니다.
모든 장르는 재생된 횟수가 다릅니다.
```
### 입출력 예
```
genres	                                  plays	                          return
[classic, pop, classic, classic, pop]	  [500, 600, 150, 800, 2500]	  [4, 1, 3, 0]
```
### 입출력 예 설명
```
classic 장르는 1,450회 재생되었으며, classic 노래는 다음과 같습니다.

고유 번호 3: 800회 재생
고유 번호 0: 500회 재생
고유 번호 2: 150회 재생
pop 장르는 3,100회 재생되었으며, pop 노래는 다음과 같습니다.

고유 번호 4: 2,500회 재생
고유 번호 1: 600회 재생
따라서 pop 장르의 [4, 1]번 노래를 먼저, classic 장르의 [3, 0]번 노래를 그다음에 수록합니다.
```

# Try!
## 생각의 흐름
```
장르와 재생된 횟수로 array를 만들어서 같은 장르별 재생횟수의 합을 비교한다.
그 합이 제일 많은 장르부터 차례대로 장르별 재생횟수가 높은것 부터 2개씩 선발해서 
그 재생횟수가 포함되는 짝이 array의 몇 번째인지를 뜻하는 수로 array를 만든다.

-> genre와 plays의 순서가 같은 것 활용해보자.
```

## 정답
```
function solution(genres, plays) {
    var answer = [];
    let obj = {
        max:[]
    }

    for(let i in genres){
    //max array를 활용하여 장르별로 그룹지어 plays합 구하기
        if (obj[genres[i]]){
            for(let j in obj.max){
                if(obj.max[j].genres == genres[i]){
                    obj.max[j].p += plays[i]
                }
            }
            obj[genres[i]].push({
                id : i,
                p : plays[i]
            })
            } else {
    //max array
             ★ obj[genres[i]]= [];
                obj.max.push({
                    genres : genres[i],
                    p : plays[i]
                })
                obj[genres[i]].push({
                    id : i,
                    p : plays[i]
                })
            }
        }  

//크기대로 정렬해서
    Object.keys(obj).forEach((key) =>{
        obj[key].sort((a,b)=>{
            return a.p > b.p ? -1 :a.p < b.p ? 1 : 0;
        })
    })
    
 //2개 이상이면 2개, 1개면 1개만뽑아서 넣기
        for(let i in obj.max){
            let g = obj.max[i].genres
            let k = 2
            if(obj[obj.max[i].genres].length<2){
                k=1
            }
        for(let j=0; j<k; j++){
            answer.push(parseInt(obj[g][j].id))
        }
        }

    return answer;
}
```

## 후기
아직 문제를 뚝딱뚝딱 푸는 수준은 아니라, 배열을 잘 활용해서 답을 이끌어내는 과정을 계속 연습.<br>
max array를 활용하여 장르별로 그룹지어 plays합 구하는 과정의 if와 for의 단계적 과정 복습.<br>
for이 이중으로, 여러번 등장하기 때문에 복잡도를 낮추는 다른 방법 생각해보자.<br>
(물론 이 방법도 코드채점시 모두 통과했다)<br>
Object.keys(obj).forEach 구문을 잘 익혀서 나중에 key값을 활용할 때 잘 써먹어 보기.<br>
해시에 관한 문제를 난이도별로 풀어 봤으니 해시에 대해 정리해보기.<br>
