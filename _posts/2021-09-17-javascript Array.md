---
title: "[Javascript] Array Method"
excerpt: "Javascript의 배열을 어떻게 처리하는지 확인해보자. "

categories:
  - Javascript
tags:
  - [Blog, jekyll, Github, Git]

toc: true
toc_sticky: true

date: 2021-09-18
last_modified_at: 2020-09-18
---

# 1. 배열에서 마지막 요소 추가 push( )

```javascript
const target = ["a", "b", "c", "d", "e"];
target[target.length] = "f";
target.push("f");
```

# 2. 배열에서 마지막 요소 삭제 : pop( )

```javascript
const target2 = ["a", "b", "c", "d", "e"];
target2, pop(); // e 제거 ->['a', 'b', 'c', 'd']
```

# 3. 배열에서 첫번째 요소 추가 : unshift( )

```javascript
const target3 =['b', 'c', 'd', 'e', 'f'];
target3.unshift('a'); -> ['a', 'b', 'c', 'd', 'e', 'f'];
```

# 4. 배열에서 첫번째 요소 삭제 : shift( )

```javascript
const target4 =['a', 'b', 'c', 'd', 'e'];
target4.shift('a'); -> ['b', 'c', 'd', 'e'];
```

# 5. 배열에서 중간 요소 삭제 : splice(시작 인덱스, 배열에서 제거할 요소의 수)

```javascript
const target5 = ["가", "나", "다", "라", "마"];
const splice = target5.splice(1, 1);
console.log(target5, splice);

<결과>
["가", "다", "라", "마"] ["나"]
```

```javascript
const target5 = ["가", "나", "다", "라", "마"];
const splice = target5.splice(2, 2);
console.log(target5, splice);

<결과>
["가", "나", "마"] ["다", "라"]
```

```javascript
const target5 = ["가", "나", "다", "라", "마"];
const splice = target5.splice(1);
console.log(`target5 : ${target5}, splice : ${splice}`)

<결과>
target5 : ["가"] splice : ["나", "다", "라", "마"]
```

```javascript
const target5 = ["가", "나", "다", "라", "마"];
const splice = target5.splice(1, 3, '타', '파');
console.log(`target5 : ${target5}, splice : ${splice}`)

<결과>
target5 : 가,타,파,마, splice : 나,다,라
```

```javascript
const arr = ["가", "나", "다", "라", "마"];
arr.splice(2, 0, "바");
console.log(arr);
//'바'를 '다' 위치에 추가

<결과>
["가", "나", "바", "다", "라", "마"]
```

# 6. 배열에서 요소찾기 : includes( ),

#### 요소가 있으면 true, 없으면 false로 return, 반복문과 조건문에 주로 사용

```javascript
const target = ["가", "나", "다", "라", "마"];
const result = target.includes("다");
const result2 = target.includes("카");
console.log(result);
console.log(result2);
// <결과>
true;
false;
```

# 7. 배열 인덱스 위치 확인 : indexOf, lastIndexOf

#### 앞에서 찾기(indexOf), 뒤에서 찾기(lastIndexOf), 만일 배열의 인덱스의 값이 없으면 -1로 return

```javascript
const target = ["라", "나", "다", "라", "다"];
const result = target.indexOf("다");
const result2 = target.lastIndexOf("라");
const result3 = target.indexOf("가");
console.log(result);
console.log(result2);
console.log(result3);

<결과>
2
3
-1
```

#### 0번째 자리에서 숫자를 찾을 경우

```javascript
const arr = [1, 2, 3, 4, 5];
if(arr.indexOf(1)){ // 1이 0번지여서 '1 찾았다'가 나올꺼 같지만, arr.indexOf(1)이 0이 되므로 if문 조건식에서 false(0)로 인식하여 else문을 실행함
    console.log('1 찾았다');
    else{
        console.log('1 못찾았다.')
    }
}
<결과>
1 못찾았다.
```

그렇게 때문에 아래와 같이 조건을 붙여 주어야 한다.

```javascript
const arr = [1, 2, 3, 4, 5];
if(arr.indexOf(1) > -1){ //indexOf가 0번째 자리일 경우
    console.log('1 찾았다');
    else{
        console.log('1 못찾았다.')
    }
}
<결과>
1 찾았다.
```

# 8. 배열 반복하기

#### while문

```javascript
const target = ["가", "나", "다", "라", "마"];
let i = 0;
while (i < target.length) {
    console.log(target[i]);
  i++;
}

const targetStr = '가나다라마' //문자열도 해당
while (i < targetStr.length) {
  console.log(targetStr[i]);
  i++;
}

<결과>
가
나
다
라
마
```

#### for문

```javascript
const target = ["가", "나", "다", "라", "마"];
for (let i = 0; i < target.length; i++) {
  console.log(target[i]);
}

<결과>
가
나
다
라
마
```

## 문제

#### 다음 배열에서 '라'를 모두 제거하세요. indexOf와 splice를 사용하세요.

```javascript
const arr = ["가", "라", "다", "라", "마", "라"];
while (index > -1) {
  arr.splice(index, 1);
  index = arr.indexOf("라");
}
```

#### 내가 푼것

```javascript
for (let i = 0; i < arr.length; i++) {
  arr.splice(arr.indexOf("라"), 1);
}
```
