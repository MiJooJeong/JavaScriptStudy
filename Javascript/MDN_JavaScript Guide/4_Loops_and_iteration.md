# 4. 루프와 반복

## `for`문

```text
for ([초기문]; [조건문]; [증감문])
  문장
```

**실행순서**
1. 초기문이 존재한다면 초기문이 실행. 이 표현은 보통 1이나 반복문 카운터로 초기 설정이 된다. 그러나 복잡한 구문으로 표현되거나 변수로 선언되기도 한다.
2. 조건문은 조건을 검사하여, 참인경우 반복문이 실행되고 거짓인 경우 그 for 문은 종결된다. 생략되는 경우 참으로 추정한다.
3. 문장이 실행된다. 많은 문장을 실행할 경우, {}를 써서 문장들을 묶어준다
4. 증감문이 존재한다면 실행하고 2번째 단계로 돌아간다.

예시:

다중 선택을 허용하는 요소(`<select>`)에서 선택된 옵션들을 세는 for 문

```html
<form name="selectForm">
  <p>
    <label for="musicTypes">Choose some music types, then click the button below:</label>
    <select id="musicTypes" name="musicTypes" multiple="multiple">
      <option selected="selected">R&B</option>
      <option>Jazz</option>
      <option>Blues</option>
      <option>New Age</option>
      <option>Classical</option>
      <option>Opera</option>
    </select>
  </p>
  <p><input id="btn" type="button" value="How many are selected?" /></p>
</form>

<script>
function howMany(selectObject) {
  var numberSelected = 0;
  for (var i = 0; i < selectObject.options.length; i++) {
    if (selectObject.options[i].selected) {
      numberSelected++;
    }
  }
  return numberSelected;
}

var btn = document.getElementById("btn");
btn.addEventListener("click", function(){
  alert('Number of options selected: ' + howMany(document.selectForm.musicTypes))
});
</script>
```

## `do...while` 문

```text
do
  문장
while (조건문);
```

**실행순서**

1. 문장이 실행된다. 많은 문장을 실행하기 위해서는 {}가 필요하다.
2. 조건문을 확인한다. 조건문이 참이라면 1번으로 돌아간다. 거짓인 경우 실행을 멈추고 바로 아래 있는 문장을 실행시킨다

예시

i가 5보다 작지 않을 때까지 반복됨

```javascript
var i = 0;
do {
  i += 1;
  console.log(i);
} while (i < 5);
```

## `while` 문

```text
while(조건문)
  문장
```

조건문을 확인한다. 조건문이 참이면 문장을 실행하고, 거짓이면 반복문 바로 다음 문장을 실행시킨다. 많은 문장을 실행하기 위해서는 {}를 써서 문장들을 묶어준다.

예시

```javascript
n = 0;
x = 0;
while (n < 3) {
  n++;
  x += n;
}
```

무한 루프에 빠질 수 있다.

```javascript
while (true) {
  console.log("Hello, world");
}
```

## 레이블문

반복문을 지정하고, break문과 continue문을 같이 사용하여 실행중에 반복문을 계속 실행할지 멈출지를 지정할 수 있다.

```text
lable:
  문장
```

예시

```javascript
var str = "";

loop1:
for (var i = 0; i < 5; i++) {
  if (i === 1) {
    continue loop1;
  }
  str = str + i;
}

console.log(str);  // expected output: "0234"
```

```javascript
var i, j;

loop1:
for (i = 0; i < 3; i++) {      //The first for statement is labeled "loop1"
   loop2:
   for (j = 0; j < 3; j++) {   //The second for statement is labeled "loop2"
      if (i === 1 && j === 1) {
         break loop1;
      }
      console.log('i = ' + i + ', j = ' + j);
   }
}

// Output is:
//   "i = 0, j = 0"
//   "i = 0, j = 1"
//   "i = 0, j = 2"
//   "i = 1, j = 0"
```

## break 문

반복문, switch문, 레이블문 과 결합한 문장을 빠져나올때 사용

```text
break;
break (레이블);
```

예시

반복문에서의 `break`
```javascript
for (i = 0; i < a.length; i++) {
  if (a[i] == theValue) {
    break;
  }
}
```

레이블문에서의 `break`
```javascript
var x = 0;
var z = 0
labelCancelLoops: while (true) {
  console.log("Outer loops: " + x);
  x += 1;
  z = 1;
  while (true) {
    console.log("Inner loops: " + z);
    z += 1;
    if (z === 10 && x === 10) {
      break labelCancelLoops;
    } else if (z === 10) {
      break;
    }
  }
}
```

## `continue`문

반복문, 레이블문을 다시 시작하기 위해 사용

- 반복문에서 사용할 경우: 현재 반복을 종료하고 다음 반복으로 실행을 계속한다. `while`루프에서는 조건으로, `continue` 루프에서는 증가 표현으로 이동한다.
- 레이블문과 함께 사용하는 경우, 레이블로 식별되는 반복문에 적용된다.

예시
```javascript
i = 0;
n = 0;
while (i < 5) {
  i++;
  if (i == 3) {
    continue;
  }
  n += i;
}
```

```javascript
checkiandj:
  while (i < 4) {
    console.log(i);
    i += 1;
    checkj:
      while (j > 4) {
        console.log(j);
        j -= 1;
        if ((j % 2) == 0) {
          continue checkj;
        }
        console.log(j + " is odd.");
      }
      console.log("i = " + i);
      console.log("j = " + j);
  }
```

## `for...in`문

객체의 열거 속성을 통해 지정된 변수를 반복한다. 배열 요소를 반복하는 방법으로 사용할 수 있으나, 배열 객체의 수정있는 경우 다르게 동작할 수 있으므로 배열은 `for`문을 사용하는 것이 좋다.

```text
for (variable in object) {
    statement
}
```

예시

```javascript
function dump_props(obj, obj_name) {
  var result = "";
  for (var i in obj) {
    result += obj_name + "." + i + " = " + obj[i] + "<br>";
  }
  result += "<hr>";
  return result;
}
```

## `for...of` 문

ES6에서 새로 적용된 문법으로, 반복 가능한 객체를 통해 반복하는 루프를 만든다.

```text
for (variable of object) {
  statement
}
```

for...in 과 for...of 문의 차이

```javascript
let arr = [3, 5, 7];
arr.foo = "hello";

for (let i in arr) {
   console.log(i); // logs "0", "1", "2", "foo"
}

for (let i of arr) {
   console.log(i); // logs "3", "5", "7"
}
```