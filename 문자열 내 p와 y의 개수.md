#### 문제 설명

대문자와 소문자가 섞여있는 문자열 s가 주어집니다. s에 'p'의 개수와 'y'의 개수를 비교해 같으면 True, 다르면 False를 return 하는 solution를 완성하세요. 'p', 'y' 모두 하나도 없는 경우는 항상 True를 리턴합니다. 단, 개수를 비교할 때 대문자와 소문자는 구별하지 않습니다.

예를 들어 s가 "pPoooyY"면 true를 return하고 "Pyy"라면 false를 return합니다.

#### 제한사항

- 문자열 s의 길이 : 50 이하의 자연수
- 문자열 s는 알파벳으로만 이루어져 있습니다.

#### 입출력 예

|   **s**   | **return** |
| :-------: | :--------: |
| "pPoooyY" |    true    |
|   "Pyy"   |   false    |

#### 나의 풀이 1

```js
function solution(s) {
  const upper = s.toUpperCase();
  let countP = 0;
  let countY = 0;
  for (let i = 0; i < upper.length; i++) {
    if (upper[i] === "P") {
      countP++;
    }
    if (upper[i] === "Y") {
      countY++;
    }
  }
  return countP === countY;
}
```

#### 풀이1 설명

일단 대문자와 소문자를 구분하지 않는다고 했으니 모두 대문자로 바꿨다!
for문으로 돌면서 P의 개수를 세고, Y의 개수를 모두 센 뒤 두 가지를 비교해서 답을 구했다!

#### 다른 사람의 풀이

```js
function solution(s) {
  const upper = s.toUpperCase();
  return upper.split("P").length === upper.split("Y").length;
}
```

#### 다른 사람의 풀이 설명

P와 Y의 개수가 같다면 split으로 쪼갰을 때 숫자가 같을 것이라는 신박한 풀이 방법!

#### 느낀 점

다른 사람들의 풀이를 보면 조금 더 열린 사고를 가져야 할 것 같다는 생각을 자주 하게된다.
