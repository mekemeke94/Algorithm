#### 문제 설명

배열 array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, k번째에 있는 수를 구하려 합니다.

예를 들어 array가 [1, 5, 2, 6, 3, 7, 4], i = 2, j = 5, k = 3이라면

array의 2번째부터 5번째까지 자르면 [5, 2, 6, 3]입니다.
1에서 나온 배열을 정렬하면 [2, 3, 5, 6]입니다.
2에서 나온 배열의 3번째 숫자는 5입니다.
배열 array, [i, j, k]를 원소로 가진 2차원 배열 commands가 매개변수로 주어질 때, commands의 모든 원소에 대해 앞서 설명한 연산을 적용했을 때 나온 결과를 배열에 담아 return 하도록 solution 함수를 작성해주세요.

#### 제한사항

- array의 길이는 1 이상 100 이하입니다.
- array의 각 원소는 1 이상 100 이하입니다.
- commands의 길이는 1 이상 50 이하입니다.
- commands의 각 원소는 길이가 3입니다.

#### 입출력 예

|       **array**       |           **commands**            |  return   |
| :-------------------: | :-------------------------------: | :-------: |
| [1, 5, 2, 6, 3, 7, 4] | [[2, 5, 3], [4, 4, 1], [1, 7, 3]] | [5, 6, 3] |

#### 나의 풀이 1

```js
function solution(array, commands) {
  var answer = [];
  for (let i = 0; i < commands.length; i++) {
    answer.push(
      array.slice(commands[i][0] - 1, commands[i][1]).sort()[commands[i][2] - 1]
    );
  }
  return answer;
}
```

#### 풀이 설명

문제 그대로 풀었다.
주어진 array를 slice한 후 sort를 이용해 정렬하고 push를 이용해 answer에 집어넣었다.
이론상으로는 맞는 것 같은데 계속 테스트 1개가 오류가 났다..!

#### 나의 풀이 2

```js
function solution(array, commands) {
  var answer = [];
  let i = 0;
  let j = 0;
  let k = 0;
  for (let l = 0; l < commands.length; l++) {
    i = commands[l][0];
    j = commands[l][1];
    k = commands[l][2];

    let sliceArray = array.slice(i - 1, j);
    sliceArray.sort((a, b) => a - b);

    answer.push(sliceArray[k - 1]);
  }
  return answer;
}
```

#### 풀이 설명

먼저 보기 좋게 깔끔하게 정리를 하고 다시 테스트를 돌려봤다.
결과는 그대로...!

원인이 뭘까 한참을 찾았는데 바로 sort 메서드의 문제였다.

sort 메서드는 compareFunction을 받는 메서드인데,
compareFunction이란 정렬 순서를 정의하는 함수이며 생략하면 배열은 각 요소의 문자열 변환에 따라 각 문자의 유니 코드 코드 포인트 값에 따라 정렬된다.
숫자 정렬에서는 2가 1보다 크지만 compareFunction 인자가 없을 시,
숫자가 문자열로 변환되기 때문에 맨 앞 글자를 비교하여 '10'은 '2'보다 작은 값으로 취급된다고 한다.

따라서 원하는 결과인 오름차순 순서로 숫자를 비교하려면 sort( )를 비워서 쓰면 안 되고 안에 compareFunction조건을 사용해야 원하는 오름차순 결과를 얻을 수 있었다.
`sort((a, b) => a - b);`

#### 다른 사람의 풀이

```js
function solution(array, commands) {
  var answer = [];

  answer = commands.map((a) => {
    return array.slice(a[0] - 1, a[1]).sort((b, c) => b - c)[a[2] - 1];
  });
  return answer;
}
```

#### 다른 사람의 풀이 설명

궁극적인 원리는 비슷하지만 map을 사용해 더 간략하게 줄인 코드도 있었다.

#### 느낀 점

다른 사람들의 최대한 줄 수를 줄인 코드들을 보며
명시적인 코드는 과연 길지만 최대한 쉽게 풀어놓은 코드일까, 여러 메서드를 사용해 최대한 간략하고 깔끔하게 써놓은 코드일까 고민이 생겼다.
