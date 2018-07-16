---
categories: JavaScript
title: JavaScript Study EP 1
---


*이 게시글은 학습목적으로 작성되었으며 생활코딩(opentutorial.org)의 온라인 강의 내용에 대한 정리입니다.*


## 자바스크립트 기본

### 숫자와 문자

#### 숫자

자바스크립트에서는 큰따옴표나 작은따옴표가 붙지 않은 숫자는 숫자로 인식한다.

> 곱하기를 할 때는  `*`를 사용한다
>
> 나누기를 할 때는 `/`를 사용한다.

자바스크립트에서는 사칙연산 보다 좀 더 복잡한 연산도 지원한다.

```javascript
Math.pow(3, 2);           // 3의 2승
Math.round(10.6);         // 10.6을 반올림
Math.ceil(10.2);          // 10.2를 올림
Math.floor(10.6);         // 10.6를 내림
Math.sqrt(9);             // 9의 제곱근
Math.random();            // 0부터 1.0사이의 랜덤한 숫자
```

#### 문자

문자는 큰따옴표`"` 또는 작은따옴표`'` 중의 하나로 감싸야 한다. string 이라고 부른다.

숫자를 따옴표로 감싸면 문자가 된다. 

만약 문자열 안에 작은따옴표나 큰따옴표를 넣고 싶다면 이스케이프 `\`를 원하는 따옴표 앞에 입력하면 된다.

#### 여러줄의 표시

여러줄을 표시하기 위해서는 아래와같이 \n 을 넣는다.

```javascript
alert("안녕하세요. \n 생활코딩의 세계에 오신 것을 환영합니다.");
```

#### 문자연산

아래와 같이 문자와 문자를 더할 수 있다.

```javascript
"coding"+"everybody"
```

문자의 길이를 구할 때는 문자 뒤에 .length 를 넣는다.

```javascript
"javascript".length
```

### 변수

변수 (Variable)는 (문자나 숫자 같은) 값을 담는 컨테이너로 값을 유지할 필요가 있을 때 사용한다.

여기에 담겨진 값은 다른 값으로 바꿀 수 있다. 변수는 마치 자연어에서 대명사와 비슷한 역할을 한다.

#### 변수의 선언

JavaScript 에서 변수는 var로 시작한다. var은 변수를 선언하겠다는 것을 의미한다.

var을 생략할 수도 있지만 이것은 유효범위라는 것에 영향을 미친다. 그러므로 var의 의미를 명확하게 이해하기 전까지는 var를 사용하는 것을 권장한다. 변수의 이름은 $, _, 혹은 특수 문자를 제외한 모든 문자로 시작할 수 있다.

```javascript
var a = 1;        // 변수선언은 let 으로도 가능
// var a = 1;
alert(a + 1);     // 2 
```

`//` 은 주석(comment)으로 코드에 부가적인 설명을 쓰거나 사용하지 않는 코드를 비활성시키기 위해서 사용한다

`;` 은 하낭의 구문이 끝났음을 명시적으로 나타내는 기호다. 다음처럼 한줄에 여러구문을 사용하고 싶을 때 세미콜론이 유용하다.

```javascript
 a = 1; alert(a+1);
```

JavaScript에서는 세미콜론을 생략할 수 있는데, 이 경우 줄바꿈을 명령의 끝으로 간주하게 된다. 

변수의 값은 꼭 숫자만 올 수 있는 것은 아니다. 

```javascript
let first = "coding";
let a = 'coding', b = 'everybody';
```

#### 변수가 없다면

변수는 코드의 재활용성을 높여준다. 예를 들어 100에 10을 더하고, 10을 나눈 후에 다시 10을 빼고 거기에 10을 곱해야 한다고 할때 각 단계마다 그 결과를 출력해야하는 코드는 아래와 같다.

```javascript
alert(100+10);
alert((100+10)/10);
alert(((100+10)/10)-10);
alert((((100+10)/10)-10)*10);
```

계산해야 할 값이 바뀌었다면, 위 코드를 모두 수정해야 할 것이다. 

```javascript
a = 100;
a = a + 10;
alert(a);
a = a / 10;
alert(a);
a = a - 10;
alert(a);
a = a * 10;
alert(a);
```

위의 코드에서 첫번째 줄의 100을 다른 숫자로 바꾸면 나머지 로직에 대입되느 변수의 값이 모두 바뀐다. 

수정해야 할 코드가 적다는 것은 그만큼 해야 할 일이 줄어든다는 의미고, 그 과정에서 버그가 발생할 가능성을 낮출 수 있다. 변수의 효용은 반복문, 조건문, 함수와 결합되면 더욱 중요해진다.



### 주석

null



### 줄바꿈과 여백

null



### 비교

#### 연산자

연산자란 값에 대해서 어떤 작업을 컴퓨터에게 지시하기 위한 기호인데 우리는 이미 연산자를 사용했다. `=`는 우항의 값인 1을 좌항의 변수 a에 대입하는 '대입 연산자'다. 

#### 비교연산자

프로그래밍에서 비교란 주어진 값들이 같은지, 다른지, 큰지, 작은지를 구분하는 것을 의미한다. 이 때 비교 연산자를 사용하는데 비교 연산자의 결과는 true나 false 중의 하나다  true는 비교 결과가 참이라는 의미이고 false는 거짓이라는 뜻이다. true 와 false 는 블린(boolean)이라고 불리는 데이터 형식이다.

##### ==

동등 연산자로 좌항과 우항을 비교해서 서로 값이 같다면 true 다르다면 false가 된다.

`=` 가 하나인 것은 대입 연산자로 우항의 값을 좌항의 변수에 대입할 때 사용하는 것으로 의미가 완전히 다르다

##### ===

일치 연산자로 `===` 좌항과 우항이 '정확'하게 같을 때 true 다를 때 false가 된다. 

```javascript
1 == '1' ;               // true
1 === '1' ;              // false
null == undefined        // true
null === undefined       // false
true == 1                // true
true === 1               // false
true == '1'              // true
true === '1'             // false
```

`===` 숫자 1과 문자 1을 다르게 인식한다. 반면에 `==`는 양쪽의 값이 같다고 판단한다. 즉 `===`는 서로 같은 수를 표현하고 있더라도 데이터 형이 같은 경우에만 같다고 판단하기 때문이다. `==` 보다 `===` 사용을 권한다.

NaN은 0/0과 같은 연산의 결과로 만들어지는 특수한 데이터 형인데 숫자가 아니라는 뜻이다. 

##### !=

`!` 는 부정을 의미한다. '같다'의 부정은 '같지않다'이다. 이것을 기호로 `!=` 로 표시한다.

아래의 결과는 `!=` 의 결과인데 `==`와 정 반대의 결과를 보여준다

```javascript
1 != 2                   // true
1 != 1                   // false
"one" != "two"           // true
"one" != "one"           // false
```

##### !==

`!==`는 `!=`와 `==`의 관계와 같다. 정확하게 같지않다는 의미이다.

##### >

좌항이 우항보다 크다면 참, 그렇지 않다면 거짓임을 알려주는 연산자다.

##### >=

좌항이 우항보다 크거나 같다



### 조건문

#### Boolean

비교 연산의 결과로 참(true)이나 거짓(false)를 얻을 수 있다. 여기서 참과 거짓은 숫자와 문자처럼 언어에서 제공하는 데이터 형이다. 이를 Boolean(불린)으로 부르고 불린으로 올 수 있는 값은 true와 false두가지 밖에없다.

#### 조건문

조건문이란 주어진 조건에 따라서 애플리케이션을 다르게 동작하도록 하는 것이다.

#### 조건문의 문법

##### if

조건문은 if로 시작한다. if 뒤의 괄호에 조건이 오고, 조건이 될 수 있는 값은 Boolean이다. Boolean의 값이 true라면 조건이 담겨진 괄호 다음의 중괄호 구문이 실행된다.

```javascript
# 예제 1>
if(true){                              // 실행결과는 'result : true'이다. 
    alert('result : true');            // 뒤에 true가 왔기 때문이다.
}
# 예제 2>
if(false){                             // 뒤에 false가 왔기 때문에
    alert('result : true');            // 아무것도 출력하지 않을 것이다.
}
# 예제 3>
if(true){                              // 뒤에 true가 붙었으므로
    alert(1);                          // 123을 출력할 것이다
    alert(2);
}
alert(3);
# 예제 4>
if(false){
    alert(1);                          // 뒤에 false가 붙었으므로
    alert(2);                          // 3만 출력할 것이다. 
}                                      // 중괄호 구간이 실행되지않기 때문이다.
alert(3);
```

##### else

if만으로는 좀 더 복잡한 상황을 처리하는데 부족하다.

if문의 조건이 true라면 if의 중괄호 구간이 실행되고, false라면 else 이후의 중괄호 구간이 실행된다. 즉 else는 주어진 조건이 거짓일 때 실행할 구간을 정의하는 것이다. 

```javascript
if(true){                // 결과는 1이다
    alert(1);
} else {
    alert(2);
}
if(false){               // 결과는 2이다
    alert(1);
} else {
    alert(2);
}
```

##### else if

else if 를 이용하면 조건문을 좀 더 풍부하게 할 수 있다. 

else if 는 좀 더 다양한 케이스의 조건을 검사할 수 있는 기회를 제공한다. else if 의 특징은 if 나 else 와는 다르게 여러개가 올 수 있다는 점이다. else if 의 모든 조건이 false 라면 else 가 실행된다. else 는 생략 가능하다.

```javascript
if(false) {                     // 결과는 2이다
    alert(1);
} else if(true) {
    alert(2);
} else if(true) {             
    alert(3);
} else {
    alert(4);
}
```

#### 변수와 비교 연산자

앞서 배운 변수와 비교 연산자 그리고 조건문을 결합해보자. ID의 값으로 ryan을 입력해보고, 다른 값도 입력해보자 

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8"/>
</head>
<body>
    <script>
        id = prompt('아이디를 입력해주세요')
        if(id == 'ryan') {
            alert('아이디가 일치합니다.')
        } else {
            alert('아이디가 일치하지 않습니다.')
        }
    </script>
</body>
</html>
```

위의 내용에서 prompt() 구문은 사용자가 입력한 값을 가져와서 id 변수의 값으로 대입한다. 이러한 것을 API 또는 함수라고 부른다. 사용자가 입력한 값이 ryan이라면 '아이디가 일치 합니다.' 를 출력하고 그렇지 않다면 '아이디가 일치하지 않습니다.'를 출력한다.

#### 조건문의 중첩

아이디와 비밀번호 검증

if문 안에 다시 if문이 등장했다. 즉 사용자가 입력한 값과 아이디의 값이 일치하는지를 확인한 후에 일치한다면 비밀번호가 일치하는지 확인한 것이다. 이렇게 조건문은 조건문안에 중첩해서 사용될 수 있다. 조건문은 조건문안에 중첩해서 사용될 수 있다.

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset = "utf-8"/>
</head>
<body>
    <script>
        id = prompt('아이디를 입력해주세요.');
        if(id=='ryan'){
            password = prompt('비밀번호를 입력해주세요.')
            if(password === '111111'){
                alert('인증 했습니다.');
            } else {
                alert('인증에 실패했습니다.');
            }
        } else {
            alert('등록된 아이디가 없습니다.')
        }
    </script>     
</body>
</html>
```

#### 논리 연산자

논리 연산자는 조건문을 좀 더 간결하고 다양한 방법으로 구사할 수 있도록 도와준다.

##### &&

`&&`는 좌항과 우항이 모두 참(true)일 때 참이된다. `&&`의 좌우항이 모두 true인 것은 첫번째 조건문 밖에 없기 때문이다. 이러한 논리 연산자를 and 연산자라고 한다. 

```javascript
if(true && true) {          // 참
    alert(1);
}
if(true && false) {         // 거짓
    alert(2);
}
if(fasle && true) {         // 거짓
    alert(3);
}
if(false && false) {        // 거짓
    alert(4);
}
```

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset = "utf-8"/>
</head>
<body>
    <script>
        id = prompt('아이디를 입력해주세요.');
        password = prompt('비밀번호를 입력해주세요.')
        if(id == 'ryan' && password === '111111'){
            alert('인증 했습니다.');
        } else {
            alert('인증에 실패했습니다.');
        }
    </script>     
</body>
</html>
```

중첩된 if 문을 하나로 줄였다. 덕분에 코드의 복잡성도 낮아졌다. `&&` 는 아래와 같은 의미를 만든다.

"id의 값이 ryan이고 password의 값이 111111 이면 참이다."

즉 && 연산자의 좌항과 우항이 모두 참일 때 전체가 참이 되는 것이다.

##### ||

`||`는 `||`의 좌우항 중에 하나라도 true라면 true가 되는 논리 연산자이다.  or 연산자라고 부른다

```javascript
if(true || true) {          // 참
    alert(1);
}
if(true || false) {         // 참
    alert(2);
}
if(fasle || true) {         // 참
    alert(3);
}
if(false || false) {        // 거짓
    alert(4);
}
```

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset = "utf-8"/>
</head>
<body>
    <script>
        id = prompt('아이디를 입력해주세요.');
        password = prompt('비밀번호를 입력해주세요.')
        if((id == 'ryan' || id == 'sedric' || id == 'francis' || id == 'mark') 
            && password === '111111'){
            alert('인증 했습니다.');
        } else {
            alert('인증에 실패했습니다.');
        }
    </script>     
</body>
</html>
```

1. (id == 'ryan' || id == 'sedric' || id == 'francis' || id =='mark') : true 가 된다.
2. password == '111111' : true가 된다.
3. true and true : true가 된다.

id비교를 할 때 괄호를 사용한 것은 사칙 연산을 할 때 괄호부터 계산하는 것과 같은 원리이다.

##### !

`!`는 부정의 의미로, Boolean의 값을 역전시킨다. true를 false로 false를 true로 만든다. not 연산자라고 부른다

```javascript
if(!true && !true) {          // 거짓
    alert(1);
}
if(!true && !false) {         // 거짓
    alert(2);
}
if(!fasle && !true) {         // 거짓
    alert(3);
}
if(!false && !false) {        // 참
    alert(4);
}
```



#### boolean의 대체제

##### 01

조건문에 사용될 수 있는 데이터 형이 꼭 불린만 되는 것은 아니다. 관습적인 이유로 0은 false, 0이 아닌 값은 true로 간주된다. 

#### 기타 false로 간주되는 데이터 형

다음은 false와 0 외에 false로 간주되는 데이터 형의 리스트다. if 문의 조건으로 !(부정) 연산자를 사용했기 때문에 각 조건문의 첫번째 블록이 실행되는 것은 주어진 값이 false이기 때문이다.

```javascript
if(!''){
    alert('빈 문자열')
}
if(!undefined){
    alert('undefined');
}
let a;
if(!a){
    alert('값이 할당되지 않은 변수');
}
if(!null){
    alert('null');
}
if(!NaN){
    alert('NaN');
}
```



### 반복문

#### 반목문의 문법

반복문의 문법은 몇가지 있다. 각각의 구문은 서로 대체 가능하기 때문에 상황과 취향에 따라서 선택해서 사용하면 된다.

##### while

```javascript
while (조건) {
    반복해서 실행할 코드
}
```

while문은 while문 뒤에 따라오는 괄호 안의 조건이 참(true)이면 중괄호 안의 코드 구간을 반복적으로 실행한다. 조건이 거짓(false)이면 반복문이 실행되지 않는다. 여기서 true와 false는 종료조건이 되는데, 이 값을 변경하는 것을 통해서 반복문을 종료시킬 수 있다. 반복문에서 종료조건을 잘못 지정하면 무한반복이 되거나, 반복문이 실행되지 않는다. 

아래의 반복문은 i의 값을 1씩 순차적으로 증가시킴으로서 반복의 지속 여부를 결정하고 있다.

```javascript
var i = 0;
// 종료조건으로 i의 값이 10보다 작다면 true, 같거나 크다면 false
while(i < 10){
    // 반복이 실행될 때마다 coding evrybody <br /> 이 출련된다.
    document.wrtie('coding everybody <br />');
    // i의 값이 1씩 증가한다.
    i++
}
```

##### for

```javascript
for (초기화; 반복조건; 반복이 될 때마다 실행되는 코드){
    반복해서 실행될 코드
}
```

```javascript
for(let i = 0; i < 10; i++){
    document.wrtie('coding everybody'+i+'<br />');
}
```

for문은 제일 먼저 '초기화'를 한다. 위의 예제에서 초기화는 let i = 0; 이다. 즉 변수 i의 값을 0으로 설정한 것이다. 

그 다음에는 '반복조건' 인  i \< 10 이 실행된다. 현재 i의 값은 0이다. 그렇기 때문에 이 조건은 참이다. 

반복조건이 참이면 중괄호 안의 내용이 실행된다. 

i의 값이 0이기 때문에 'coding everybody \<br/>' 이라는 텍스트가 출력된다. 

'반복해서 실행될 코드'의 실행이 끝나면 '반복이 될 때마다 실행되는 코드' 가 실행된다. 

i++는 현재 i의 값에 1을 더하라는 의미다. 현재 i의 값은 0이다. 따라서 i++의 결과로 i는 1이 되었다. 

그리고 '반복조건'이 실행된다. 현재 i의 값은 1이기 때문에 i < 10은 참이다. 

다시 '반복해서 실행될 코드'가 실행된다. 그렇게 반복해서 작업이 실행된다. 

이 과정에서 i의 값은 반복할 때마다 1씩 증가한다. 

결국 i의 값이 10이 되는 순간 i \< 10을 충족시키지 못하게 되고 반복문은 종료된다.



#### 반복문이 없다면

coding everybody를 10번 반복해서 출력하고 싶다고 한다면 아래와 같이 코드를 작성하면된다

```javascript
document.write('coding everybody 1<br />');
document.write('coding everybody 2<br />');
document.write('coding everybody 3<br />');
document.write('coding everybody 4<br />');
document.write('coding everybody 5<br />');
document.write('coding everybody 6<br />');
document.write('coding everybody 7<br />');
document.write('coding everybody 8<br />');
document.write('coding everybody 9<br />');
document.write('coding everybody 10<br />');
```

더 큰 규모의 데이터를 다뤄야 한다면 반복문의 효용이 부각되기 시작한다. 

```javascript
let i = 0;
while(i < 10){
    document.write('coding everybody' + i + '<br />');
    i++;
}
```



#### 반복문 제어

##### break

반복작업을 중간에 중단시키고 싶다면 break를 사용하면 된다. 

```javascript
for(let i = 0; i < 10; i++) {
    if(i === 5) {
        break;
    }
    document.write('coding everybody'+i+'<br />');;
}
/* coding everybody 0
   coding everybody 1
   coding everybody 2
   coding everybody 3
   coding everybody 4
```

종료조건에 따르면 10행이 출력돼야 하는데 5행만 출력되었다. 2행의 if(i ===5)에 의해서 i의 값이 5일 때 break 문이 실행되면서 반복분이 완전히 종료된 것이다. 반복문 안에서 break가 실행되면 반복문을 즉시 종료시킨다

##### continue

실행을 즉시 중단하면서 반복은 지속되게 하려면 continue 를 사용하면 된다.

```javascript
for(let i = 0; i < 10; i++) {
    if (i === 5) {
        continue;
    }
    document.write('coding everybody'+i+'<br />');
}
/* coding everybody 0
   coding everybody 1
   coding everybody 2
   coding everybody 3
   coding everybody 4
   coding everybody 6
   coding everybody 7
   coding everybody 8
   coding everybody 9
```

i의 값이 5가 되었을 떄 실행이 중단됐기 때문에 continue 이후 구문이 실행되지 않았지만 반복문은 중단되지 않았기 때문에 나머지 결과가 출력된다.



#### 반복문의 중첩

반복문 안에는 다시 반복문이 나타날 수 있다.

```javascript
// 0부터 9까지 변수 i에 순차적으로 값을 할당
for(let i = 0; i < 10; i++) {
    // 0부터 9까지의 변수를 j의 값에 순차적으로 할당
    for(let j = 0; j < 10; j++) {
        // i와 j의 값을 더한 후에 출력
        // String은 숫자 i와 j의 데이터 타입을 문자로 형태를 변환하는 명령이다.
        // String()을 제거하고 실행해보면 의미가 좀 더 분명하게 드러난다.
        document.write(String(i) + String(j) + '<br />');
    }
}
```

단순히 글자를 반복적으로 출력하기 위해서 반복문을 사용한다고 생각 할 수도 있다. 

하지만 반복문의 진가는 배열과 결합했을 때 나타난다.



### 함수

#### 함수

함수(function) 란 하나의 로직을 재실행 할 수 있도록 하는 것으로 코드의 재사용성을 높여준다. 



#### 함수의 형식

함수의 형식은 아래와 같다.

```javascript
function 함수명 ( [인자...[,인자]] ) {
    코드
    return 반환값
}
```



#### 함수의 정의와 호출

함수는 function 뒤에 함수의 이름이 오고, 소괄호가 따라온다. 소괄호에 인자라는 값이 차례로 들어오는데 이 값은 함수를 호출할 때 함수의 로직으로 전달될 변수다. 인자는 생략할 수 있다. 함수를 호출했을 때 실행하게 될 부분이 중괄호 안쪽에 온다.

다음 예제에서 함수의 이름은 numbering 이고, 내용은 0부터 9까지를 화면에 출력하는 것이다.

```javascript
function numbering() {
    i = 0;
    while(i < 10) {
        document.write(i);
        i += 1;
    }
}
numbering();
/* 0123456789
```

제일 하단 아래 구문에 의해서 numbering이라는 이름의 함수가 호출되고 있는 것이다. 



#### 입력과 출력

함수의 핵심은 입력과 출력이다. 입력된 값을 연산해서 출력하는 것이 함수의 기본적인 역할이다. 다음은 함수에서 입력과 출력의 역할을 하는 구문들에 대한 설명이다. 



##### return

함수 내에서 사용한 return은 return 뒤에 따라오는 값을 함수의 결과로 반환한다. 동시에 함수를 종료시킨다.

```javascript
function get_member1() {
    return 'ryan';
}
function get_member2() {
    return 'mark';
}
alert(get_member1());
alert(get_member2());
/* ryan
   mark
```

get_member1와 get_member2를 출력(alert)한 결과가 각각 ryan과 mark인 이유는 함수 내에서 문자열 ryan과 mark를 return하기 때문이다. 

return은 결과를 반환하는 것 외에 함수를 중지시키는 역할도 한다. 

```javascript
function get_member() {
    return 'ryan';
    return 'mark';
    return 'francis';
    return 'sedric';
}
alert(get_member));
```

mark, francis, sedric은 출력하지 않았다. 그것은 return 'ryan' 실행 후에 함수 가 종료되었기 때문이다. 



##### 인자

인자(argument)는 함수로 유입되는 입력 값을 의미하는데, 어떤 값을 인자로 전달하느냐에 따라서 함수가 반환하는 값이나 메소드의 동작방법을 다르게 할 수 있다. 

```javascript
function get_argument(arg) {
    return arg;
}
alert(get_argument(1));
alert(get_argument(2));
```

5행의 get_argument(1)은 1행에서 3행 사이에 정의된 함수를 실행하는 구문이다. 5행의 1은 get_argument로 1이라는 값을 전달하겠다는 의미다. 이 때 1행에 정의된 (arg)구문에 의해서 변수 arg의 값을 숫자 1이 함수 안으로 전달된다. 이 변수 arg는 함수 get_argument 안에서만 유효하다. 



##### 복수의 인자

여러개의 입력값을 받고싶다면 다음과 같이 입력하면 된다

```javascript
function get_arguments(arg1, arg2) {
    return arg1 + arg2
}
alert(get_arguments(10, 20));
alert(get_arguments(20, 30));
```

함수를 호출 할 때 전달한 인자 10과 20은 함수의 선언부 (1행)의 arg1, arg2에 차례로 할당된다. 이렇게 전달된 값은 함수 내부로 전달되서 더해진 후에 반환된다.



#### 함수를 정의하는 다른 방법

자바스크립트는 함수를 정의하는 또 다른 방법을 제공한다. 

```javascript
let numbering = function () {
    i = 0;
    while(i < 10) {
        document.write(i);
        i += 1;
    }
}
numbering();
```



### 배열

#### 배열

배열(array)이란 연관된 데이터를 모아서 통으로 관리하기 위해서 사용하는 데이터 타입이다. 변수가 하나의 데이터를 저장하기 위한 것이라면 배열은 여러 개의 데이터를 하나의 변수에 저장하기 위한 것이라고 할 수 있다. 변수 name에는 문자 ryan이 할당되었다. 이제부터 name을 호출하면 문자 ryan을 사용할 수 있다.

```javascript
let name = 'ryan'
alert(name);
```



#### 배열의 생성

여러 개의 데이터를 하나의 변수에 담아서 관리할 수 있는 방법이 배열이다. 변수 member에 회원정보를 담아보자 대괄호`[]`는 배열을 만드는 기호다. 대괄호 안에 데이터를 콤마`,`로 구분해서 나열하면 배열이 된다.

```javascript
let member = ['ryan', 'mark', 'francis', 'sedric']
```

하나의 변수에 4개의 데이터를 담았다. 각각의 데이터를 원소(Element)라고 부른다.

이 데이터를 꺼내오는 방법은 다음과 같다

```javascript
let member = ['ryan', 'mark', 'francis', 'sedric']
alert(member[0]);
alert(member[1]);
alert(member[2]);
alert(member[3]);
/* ryan
   mark
   francis
   sedric
```

즉 배열에 담겨있는 값을 가져올 때는 대괄호 안에 숫자를 넣는다. 이 숫자를 색인(index)라고 부르고 0부터 시작한다. 즉 첫번째 원소(ryan)를 가져오려면 대괄호 안에 0을 넣어주어야 한다는 것이다. 이 값을 이ㅛ용해서 배열에 저장된 값을 가져올 수 있다.



#### 배열의 사용

배열의 진가는 반복문과 결합했을 때 나타난다. 반복문으로 리스트에 담긴 정보를 하나씩 꺼내서 처리할 수 있기 때문이다.

```javascript
function get_members() {
    return ['ryan', 'mark', 'francis', 'sedric'];
}
members = get_members();
// members.length는 배열에 담긴 값의 숫자를 알려준다.
for(i = 0; i < members.length; i++) {
    // members[i],toUpperCase ()는 members[i]에 담긴 문자를 대문자로 변환해준다
    document.write(members[i].toUpperCase());
    document.write('<br />');
}
```

반복문을 이용해서 배열  members의 내용을 하나씩 꺼낸 후에 이름의 첫 글자를 대문자로 변경한 후에 출력하고 있다. 배열이란 연관된 정보를 하나의 그룹으로 관리하기 위해서 사용하고 그 정보를 처리할 때는 반복문을 이용한다.



#### 배열의 제어

배열은 복수의 데이터를 효율적으로 관리, 전달하기 위한 목적으로 고안된 데이터 타입이다. 따라서 추가 / 수정 / 삭제와 같은 일을 편리하게 할 수 있도록 돕는 다양한 기능을 가지고 있다. 

##### 배열의 크기

아래와 같은 방법으로 배열의 크기를 알아낼 수 있다. 

```javascript
let arr = [1, 2, 3, 4, 5];
alert(arr.length);
```

##### 배열의 조작

###### 추가

다음은 배열의 끝에 원소를 추가하는 방법이다 push는 인자로 전달된 값을 배열 (li) 에 추가하는 명령이다. 

```javascript
let li = ['a', 'b', 'c', 'd', 'e'];
li.push('f');
alert(li);
/* 'a', 'b', 'c', 'd', 'e', 'f'
```

다음은 복수의 원소를 배열에 추가하는 방법이다. concat은 인자로 전달된 값을 추가하는 명령이다.

```javascript
let li = ['a', 'b', 'c', 'd', 'e'];
li = li.concat(['f', 'g']);
alert(li);
```

다음은 배열의 시작점에 원소를 추가하는 방법이다. unshift는 인자로 전달한 값을 배열의 첫번째 원소로 추가하고 배열의 기존 값들의 색인을 1씩 증가시킨다.

```javascript
let li = ['a', 'b', 'c', 'd', 'e'];
li.unshift('z');
alert(li);
/* 'z', a', 'b', 'c', 'd', 'e'
```

만약 두번째 인덱스 뒤에 대문자 B를 넣고 싶다면 아래와 같이 한다. splice는 첫번째 인자에 해당하는 원소부터 두번째 인자에 해당하는 원소의 숫자만큼의 값을 배열로부터 제거한 후에 리턴한다. 그리고 세번째 인자로부터 전달된 인자들을 첫번째 인자의 원소 뒤에 추가한다.

```javascript
let li = ['a', 'b', 'c', 'd', 'e'];
li.splice(2, 0, 'B');
alert(li);
/* 'a', 'b', 'B', 'c', 'd', 'e'
```

###### 제거

다음은 첫번째 원소를 제거하는 방법이다. shift를 사용하면 된다.

```javascript
let li = ['a', 'b', 'c', 'd', 'e'];
li.shift();
alert(li);
/* 'b', 'c', 'd', 'e'
```

다음은 배열 끝점의 원소를 배열 li에서 제거한다. 이때는 pop을 사용한다.

```javascript
let li = ['a', 'b', 'c', 'd', 'e'];
li.pop();
alert(li);
/* 'a', 'b', 'c', 'd'
```

###### 정렬

다음은 정렬하는 방법이다. 

```javascript
let li = ['c', 'e', 'a', 'b', 'd'];
li.sort();
alert(li);
/* 'a', 'b', 'c', 'd', 'e'
```

역순으로 정렬하고 싶을때는 아래와 같다. (알파벳 정렬이아닌, 배열순서의 역순배열,, 알파벳역순으로 정렬원할시 sort후 reverse해야함. 알파벳 역순정렬은 한방에 할수있는 방법은 없나...?)

```javascript
let li = ['c', 'e', 'a', 'b', 'd'];
li.reverse();
alert(li);
/* "d", "b", "a", "e", "c"
```

