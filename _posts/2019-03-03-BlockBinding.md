---
title: "Block Binding"
categories: 
  - ECMA6 Script
last_modified_at: 2019-03-03T13:00:00+09:00
toc: true
tags:
  - ECMA6
  - 블록바인딩
  - block binding
---

## 1장. 블록바인딩

자바스크립트에서는 변수 선언 방식에 따라 변수 생성 위치가 다르다.

### 1.1 var선언과 호이스팅
호이스팅(hoisting) : var를 이용하여 변수를 선언하면 선언한 위치와 상관없이 함수의 맨 위(함수 바깥이라면 전역스코프)에 있는 것처럼 처리된다.
~~~javascript
     function getValue(condition){
        if(condition){
            var value = "blue";  // value는 condition의 참 여부와 관계없이 만들어진다.   
        } else { 
            console.log(value);
            return null;
        }
    }

    getValue(false);// 해당 변수는 초기화되지 않았기때문에 undefined값을 가진다.
~~~


이것은 자바스크립트 엔진에서 아래와 같이 작동한다.

~~~javascript
function getValue(condition){
        var value;                  // var 선언은 함수 맨 위로 호이스팅된다.
        if(condition){
            value = "blue";         // 초기화를 실행하는 코드는 그 자리에 남아있음
            return value;
        } else { 
            console.log(value);     // else절 안에서 value에 접근할 수 있음
            return null;
        }
    }
~~~

-> 일반적으로 value는 condition이 true일 때 생성된다고 예상하지만 value는 조건문과 상관없이 만들어진다.

### 1.2 블록-레벨선언
블록-레벨 선언 
 - 주어진 블록스코프 밖에서는 접근할 수 없는 바인딩을 선언하는 것이다.  
 - 함수 내부/블록내부{} 에서 만들어진다.

#### 1.2.1 let 선언
- let으로 선언된 변수의 스코프는 현재 블록으로 제한됨
- <span style="color:red">let선언은 블록의 맨 위로 호이스팅되지 않기 때문에</span>, 전체 블록으로 선언할 수 있도록 블록에 첫 부분에 두는 것이 가장 좋다. 
~~~javascript
    function getValue(condition){
        if(condition){
            // 함수 맨 위로 호이스팅되지 않고, 블록 내에서만 value 존재
            // if 바깥에서 value가 존재할 수 없다.
            let value = "blue";         
            return value;
        } else { 
            console.log(value);   // condition이 false이면 value 선언이 안된다.
            return null;
        }
    }
    getValue(false);   // 에러 발생
~~~

#### 1.2.2 재정의 금지
~~~javascript
  var count = 30;
  let count = 40; // 문법에러 발생
~~~

~~~javascript
  var count = 30;
  if(condition){
    let count = 40;
    console.log(count);   // 40 -> let count가 var count를 코드블록 내에서 대체한다.
  }
~~~

#### 1.2.3 const 선언
const를 사용하여 선언된 바인딩은 상수(const)로 간주되며, 실행하면 변경할 수 없다.
즉, 선언과 동시에 초기화해야한다.
~~~javascript
var const; // 에러 발생
~~~

let과 마찬가지로 블록레벨 선언이다.  
-> 선언된 블록 바깥에서는 더 이상 접근할 수 없으며, 호이스팅되지 않는다는 의미이다.
~~~javascript
if(condition){
  const chkConst = "const";
}
console.log(chkConst);    // 에러 발생
~~~

재정의 금지
~~~javascript
  var count = 30;
  const count = 40; // 문법에러 발생
~~~

const로 객체 선언하기
const선언은 바인딩을 변경하지 못하도록하는 것이지, 바인딩된 값의 변경을 막는 것은 아니다.
즉, const로 선언해도 객체가 가진 값은 수정할 수 있다.
~~~javascript
  const person = {
    name : "som",
  } 
  person.name = "dasom" //  에러발생x
  person = {
    name : "dasom"      // 에러발생
  }
~~~

#### 1.2.4 임시 접근 불가구역(TDZ, Temporal Dead Zone)
코드를 해석할 떄 자바스크립트 엔진은 다음 블록을 조사하고, 그 블록에서 변수 선언을 발견하면  
var의 경우 함수 <span style="color:red">최상단이나 전역스코프로 호이스팅한다.</span>  
let/const의 경우 <span style="color:red">TDZ내에 배치한다.</span>  
<br>
<span style="color:red">TDZ안의 변수에 접근하려면 런타임 에러가 발생</span>한다.  
변수 선언이 실행된 후에만 TDZ에서 제거되며 안전하게 사용할 수 있다. 
~~~javascript
  if(condition){ 
    console.log(typeof value);   // 에러 발생
    let count = 40;
  }
~~~

### 1.3 반복문 안에서의 블록 바인딩
블록 레벨 변수 스코프로 동작하는데 가장 적절한 영역은 `반복문`이다.
~~~javascript
for(var i=0; i<10; i++){
  let a = 0;
  a += i;
}
// for문이 끝난 뒤에도 i에 접근할 수 있다.
console.log(i)    // 10

for(let i=0; i<10; i++){
  let a = 0;
  a += i;
}
// for문이 끝난 뒤에는 i에 접근할 수 없다.
// i는 for문 내에서만 존재
console.log(i)    // 에러 발생
~~~

#### 1.3.1 반복문 내의 함수
var일 때 )
~~~javascript
var funcs = [];

for(var i=0; i<10; i++){
  funcs.push(function(){
    console.log(i);
  })
}
funcs.forEach(function(func) {
    func();    // 10이 10번 출력
});
~~~
~~~javascript
// 자바스크립트 엔진
var i;
for(i=0; i<10; i++){
  funcs.push(function(){
    console.log(i);
  })
}
~~~
funcs배열은 console.log(i)를 출력하는 함수를 가지고 있다.  
최종적으로 i는 10이 되어 마무리된다.  
여기서 i는 10이고 다들 같은 i를 공유하고 있기 때문에 10이 10번 출력된다.

#### 1.3.2 반복문에서의 let 선언
~~~javascript
var funcs = [];

for(let i=0; i<10; i++){
  funcs.push(function(){
    console.log(i);
  })
}
funcs.forEach(function(func) {
    func();    // 0, 1, 2, ..., 9 순서로 출력
});
~~~
funcs배열은 console.log(i)를 출력하는 함수를 가지고 있다.  
여기서 i는 for블록 내에서만 존재한다.  
즉, 반복할 때마다 매번 새 변수 i를 만들고, 그 i는 for블록 내에서만 존재한다.  
funcs의 원소(함수)는 각 i를 가지고 있다.

#### 1.3.3 반복문에서의 const 선언
const역시 반복할 때마다 새 변수 i를 만들지만 <span style="color:red">const는 상수로 취급되어 한번 초기화되면 값을 바꾸면 안된다.</span>
~~~javascript
for(const i=0; i<10; i++){
  // 한번 실행 후 에러 발생
}
~~~
아래의 경우는 초기화 부분에서 바인딩 된 값을 변경하지 않고, 매번 새로운 바인딩을 만들기 때문에 const를 반복문에 사용할 수 있다.
~~~javascript
var object = {
  a : true,
  b : true,
  c : true
};

for(const key in object){
  // 에러 발생 x
}
~~~
-> object 안의 <span style="color:red">key값에 변경이 일어나지 않기 때문에</span> 사용 가능(매번 새로운 바인딩 생성)


### 1.4 전역 블록 바인딩
전역 스코프에서 let, const는 var와 다르게 동작한다.  
1) var  
var를 전역스코프에서 사용하면 전역 객체(브라우저에서는 Window)는 프로퍼티로 새로운 전역변수를 생성한다.<br>
![전역 블록 바인딩_var]({{site.url}}/assets/images/modernJavaScript/blockBinding/windowVarTest.png)  
-> window객체에 이미 varTest가 정의되어 있더라도 varTest를 덮어쓸 수 있다는 것을 의미한다.

2) let, const
let, const를 사용하면, 새로운 바인딩이 전역스코프에 생성되지만 전역 객체(브라우저에서는 Window)의 프로퍼티로 추가되지는 않는다.  
![전역 블록 바인딩_let]({{site.url}}/assets/images/modernJavaScript/blockBinding/windowLetTest.png)  

### 1.5 모범사례
const를 기본으로 사용하고 변수값을 변경해야만 할 때 let을 사용한다.  
예상치못한 값변경은 버그의 원인이 될 수 있기 때문이다.


## 회사에 적용할 만한 것  
`var 사용보다는 let과 const를 사용해보자!`