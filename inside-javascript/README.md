> INSIDE JavaScript (인사이드 자바스크립트 내용 정리)  

# 01 자바스크립트 기본 개요  

## 소개 

기존의 JavaScript는 서버로부터 받은 데이터를 HTML, CSS를 통해 렌더링 해주는 보조적인 역할만 수행함.  
웹이 발전하면서, 서버에서 담당하던 역할들이 상당 부분 웹 브라우저로 이동하였다.  

이제 JavaScript를 통해 웹 개발뿐만 아니라 서버, 어플리케이션 개발이 모두 가능해졌다.  

## 핵심 개념  

### 객체  

기본 데이터 타입 : ```boolean```, ```number```, ```string```, ```null```, ```undefined```
를 제외한 모든 것은 객체로 다뤄진다.  

### 함수  

함수도 일반적인 객체보다 조금 더 많은 기능이 있는 **객체**로 다뤄진다.  

### 프로토타입  

모든 객체는 숨겨진 링크(Link)인 프로토타입을 가진다.  
객체를 생성한 **생성자**의 프로토타입 객체를 가리킨다.  
ES에서는 [[Prototype]]이라고 표현한다.  

### 실행 컨텍스트와 클로저  

Javascript에서는 어떤 과정을 거쳐 실행 컨텍스트를 만들고 그 안에서 실행이 이루어진다.  
실행 컨텍스트는 자신만의 유효 범위(Scope)를 갖는다.  
이 과정에서 클로저를 구현할 수 있다.  

## 객체지향 프로그래밍  

프로토타입 체인과 클로저로 상속, 캡슐화, 정보 은닉 등의 객체지향 개념을 소화할 수 있다.  

## 함수형 프로그래밍  

함수와 클로저의 특성을 이용하여 함수형 프로그래밍을 구현할 수 있다.  
난해하게 구현된다.  

## 단점  

* 느슨한 타입 체크 -> 런타임 오류로 이어짐  
* 전역 객체의 존재 -> 충돌 위험성  
* 모호한 설명 (ES3) -> ES5 승인으로 인해 해결됨  

# 02 자바스크립트 개발 환경  

# 03 자바스크립트 데이터 타입과 연산자  

**기본 타입과 참조 타입**으로 나뉜다.  

## 기본 타입  

**숫자, 문자열, 불린값, null, undefined**  

그 자체가 하나의 값을 나타낸다.  

느슨한 타입 체크 언어 -> ```var```이라는 한 가지 키워드로만 변수를 선언한다.  

### 숫자  

모든 숫자를 64비트 부동 소수점 형태로 저장한다. (C언어의 double)  

모든 숫자를 실수로 처리 한다. (``5/2 = 2.5```)  

소수 부분을 버린 정수만 구하고 싶다면 ```Math.floor()``` 자바스크립트 메서드를 이용한다.  

### 문자열  

큰 따옴표 또는 작은 따옴표로 정의한다.  

**한번 정의된 문자열은 읽기만 가능하지 변하지 않는다.**  

인덱스를 이용하여 배열과 같이 접근할 수 있다.  

### 불린 값  

true와 false  

### null 과 undefined  

**값이 비어있음**을 나타낸다.  

undefined 타입의 변수의 타입이자, 값 또한 undefined이다.  

null 타입의 변수는 명시적으로 값이 비어있음을 나타낸다.  

null 타입의 ```typeOf``` 결과는 ```object```이다.  
따라서 null 타입 변수인지를 확인할 때에는 일치 연산자(===)를 사용해서 변수의 값을 직접 확인해야 한다.   


## 참조 타입(객체)  

기본 타입을 제외한 모든 값은 객체다. (배열, 함수, 정규표현식 등)  

객체는 단순히 key:value와 같은 해시 혀앹의 프로퍼티들을 저장하는 컨테이너이다.  
참조 타입인 객체는 여러 개의 프로퍼티들을 포함할 수 있다.  
이 프로퍼티는 **기본 타입이 되거나, 또 다른 객체가 될 수 있다.**  

함수로 구현한 프로퍼티를 메서드라고 한다.  

### 객체 생성  

[JavaScript 객체 생성 방법 3가지](https://github.com/yeoseon/tip-archive/issues/47) 참고  

### 객체 프로퍼티의 읽기/쓰기/갱신  

대괄호([]) 또는 마침표(.) 표기법을 사용한다.  

```
foo['name'] (O)
foo.name (O)  
foo[name] (X)  
```  

객체 프로퍼티에 값을 할당할 때, 이미 존재하는 프로퍼티의 경우 값을 갱신하고, 존재하지 않을 경우 동적으로 생성한다.  

프로퍼티가 표현식이거나 예약어(```full-name```)일 경우는 반드시 대괄호 표기법을 사용해야 한다.  

### for in 문과 객체 프로퍼티  

for in 문을 객체에 사용하면 객체에 포함된 모든 프로퍼티에 대해 루프를 수행한다.  

### 객체 프로퍼티 삭제  

객체의 프로퍼티를 삭제할 뿐 객체 자체는 삭제하지 못한다.  

```
delete foo.nickname; (O)   
delete foo (X)
```

## 참조 타입의 특성  

기본 타입의 연산은 해당 값 자체로 이루어지지만, **객체는 모든 연산이 실제 값이 아닌 참조값으로 처리된다.**  

### 객체 비교   

동등 연산자(==)를 통한 객체 비교시에도 실제 프로퍼티 값이 아닌 참조값을 비교한다는 것에 주의한다.  
기본타입의 경우는 실제 프로퍼티 값이 같을 경우 true가 반환되지만, 참조타입은 객체의 참조값이 같아야 true가 반환된다.  

### 참조에 의한 함수 호출 방식  

기본 타입 : 값에 의한 호출(call by value) - 메서드를 통해 값을 보낼 경우, 복사된 값이 전달된다. 해당 메소드에서 값을 변경했을 경우 기존 메소드에 있던 실제 값은 변하지 않는다.  

참조 타입 : 참조에 의한 호출(call by reference) - 메서드를 통해 값을 보낼 경우 참조값이 전달된다. 즉, 가리키고 있는 참조 대상이 같기 때문에 해당 값을 변경하면 기존의 객체 값도 변경된다.  

## 프로토타입  

**모든 객체는 자신의 부모 역할을 하는 프로토타입([[Prototype]])이라는 숨겨진 프로퍼티를 가진다.**  

```foo```라는 객체에 ```name, age```라는 프로퍼티만을 선언하였는데, ```toString()``` 메소드를 사용할 수 있는 이유  
->  foo 객체의 부모 프로토타입에 정의되어 있기 때문  

모든 객체의 프로토타입은 **객체를 생성할 때 결정된다.**  
해당 프로토타입 객체에는 모든 객체에서 호출 가능한 자바스크립트 기본 내장 메서드가 포함되어 있다.  

객체를 생성할 때, 결정된 프로토타입 객체는 임의의 다른 객체로 변경할 수 있다.  
즉 부모 객체를 동적으로 바꿀  수 있다.  
이를 이용해서 객체 상속 등의 기능을 구현하기도 한다.  

## 배열  

크기를 지정하지 않아도 된다.  
어떤 위치에 어느 타입의 데이터를 지정해도 에러가 발생하지 않는다.  

### 배열 리터럴  

**대괄호[]**
```
var colorArr = ['orange', 'yellow'];
```

```key```없이 ```value```만 포함한다.  
인덱스를 통해 접근한다.  

### 배열의 요소 생성  

동적으로 배열 원소 추가 가능  
**아무 인덱스 위치에나 값을 동적으로 추가 가능**  

배열의 크기를 현재 배열의 인덱스 중가장 큰 값을 기준으로 정의한다.  
값이 할당되지 않은 인덱스의 요소는 ```undefined``` 값을 기본으로 가진다.  

모든 배열은 ```length``` 프로퍼티를 가지고 있다.  

### 배열의 length 프로퍼티  

**배열 내 가장 큰 인덱스 + 1**  

실제 메모리는 length 크기처럼 할당되지는 않음  

### 배열 표준 메서드와 length 프로퍼티  

배열에서 사용 가능한 다양한 표준 배열 메서드를 제공한다.(예. ```push()```)  

**이 배열 표준 메소드는 모두 ```length``` 프로퍼티를 기반으로 동작한다.**  

> **원래 길이가 7이었던 메소드의 ```length```값을 5로 임의로 바꾼다면?**  
> ```push()``` 메소드는 5번째 인덱스에 문자열을 추가하게 ㅗ딘다.  

### 배열과 객체  

**배열 역시 객체지만 일반 객체와는 차이가 있다.**  

```
// 배열  
var colorArray = ['red', 'blue'];

// 객체  
var colorObj = { 
    '0': 'red',
    '1': 'blue' 
};
```

* ```colorArray[1]```, ```colorObj[1]```로 모두 접근 가능  
    * ```colorObj['1']```로 해줘야 하지만, [] 연산자 내에 **숫자**가 사용될 경우 자동으로 문자열 형태로 바꿔주기 때문에 가능하다.  
* ```typeof``` 역시 둘다 ```object```로 일치  
* ```length``` 프로퍼티는 Object의 경우 ```undefined```  
* 배열 표준 메서드 (```push()```)의 경우, Object는 사용하지 못함  
    * 객체의 경우 **Object.prototype 객체**가 프로토타입니다.  
    * 배열의 경우 **Array.prototype 객체**가 프로토타입니다.  
    * **Array.prototype 객체**의 프로토 타입은 **Object.prototype 객체**이다. 따라서 배열은 Array와 Object의 프로토타입을 모두 사용할 수 있다.  


### 배열의 프로퍼티 동적 생성  

배열 원소 이외에서 객체처럼 동적으로 프로퍼티를 생성할 수 있다.  
**배열의 ```length``` 프로퍼티는 배열 원소의 가장 큰 인덱스가 변경되었을 경우에만 변경된다.  
프로퍼티를 아무리 추가해도 ```length```는 변경되지 않음  

### 배열의 프로퍼티 열거  

```for in``` 문을 사용하면, 해당 배열 객체 안에 들어있는 모든 프로퍼티를 차례대로 출력한다.  
따라서 불필요하게 원소 외의 프로퍼티들도 출력할 수 있으므로, ```for```문 사용을 권장하고 있다.  

### 배열 요소 삭제  

```delete```  
해당 요소의 값을 ```undefined```로 설정할 뿐, 원소 자체를 삭제하지는 않는다. 따라서 ```length``` 값은 변하지 않는다.  

```splice()``` 배열 메서드  
보통 요소들을 완전히 삭제할 경우 사용한다. 이를 사용할 경우 ```length```도 변한다.  
```
splice(start, deleteCount, item...)  
* start - 배열에서의 시작 위치(index + 1)    
* deleteCount - start에서 지정한 시작 위치로부터 삭제할 요소의 수  
* item - 삭제할 위치에 추가할 요소  
```

### Array() 생성자 함수  

배열은 일반적으로 배열 리터럴로 생성한다.  
**Array() 생성자 함수**를 통해 배열을 생성하는 것을 단순화 시킨 것이 배열 리터럴이다.  
생성자 함수를 이용할 때는 반드시 ```new```를 사용한다.  

* 호출할 때 인자가 1개이고 숫자인 경우 : 호출된 인자를 ```length```로 갖는 빈 배열 생성  
* 그 외 : 호출된 인자를 요소로 갖는 배열 생성  

### 유사 배열 객체  

```length``` 프로퍼티를 가진 일반 객체  

```apply()``` 메소드를 사용하여 표준 배열 메소드를 사용할 수 있다.  

```
var obj = {name: 'foo', length: 1};
Array.prototype.push.apply(obj, ['baz']);

console.log(obj); // (출력값) { '1', 'baz', name: 'foo', length: 2 }
```

## 기본 타입과 표준 메서드  

숫자, 문자열, 불린값에 대해 각 타입별로 호출 가능한 표준 메서드를 제공한다.  

기본 타입의 경우는 객체가 아닌데 어떻게 메소드를 호출하는가?  
-> 기본값은 메소드 처리 순간에 객체로 변환된 다음 각 타입별 표준 메서드를 수행하게 된다.  
메서드 호출이 끝나면 다시 기본값으로 복귀하게 된다.  

```
toExponential() //숫자를 지수 형태의 문자열로 변환  
charAt() // 문자열에서 인자로 받은 위치에 있는 문자 반환  
```  

## 연산자  

### + 연산자  

더하기 연산과 문자열 연결 연산  

### typeof 연산자  

피연산자의 타입을 문자열 형태로 리턴  

null, 배열 : object  
함수 : function  
undefined : undefined  

### ==(동등) 연산자와 ===(일치) 연산자  

```==``` : 피연산자의 타입이 다를 경우 같은 타입으로 변환한 후 비교  
```===```: 타입이 달라도 변환하지 않고 비교  

타입 변환에 따른 잘못된 결과를 얻을 수 있으므로 ```===```를 쓰자!  

### !! 연산자  

피연산자를 불린값으로 변환  

console.log(!!''); //false  
console.log(!!{}); //true : 객체는 값이 비어있는 빈 객체라도 true로 변환된다.  

# 04 함수와 프로토타입 체이닝  

## 함수 정의  

* 함수 선언문   
* 함수 표현식  
* Function() 생성자 함수  

### 함수 리터럴  

함수 선언문과 표현식 방법에 해당한다.  

```
function add(x, y) {
    return x + y;  
}
```

* 함수명은 선택 사항이다.(익명함수)  

### 함수 선언문 방식(function statement)  

함수 리터럴 중 **반드시 함수명이 정의되어야 하는** 방법  

### 함수 표현식 방식(function expression)  

**함수도 하나의 값처럼 취급한다.**  

함수 리터럴로 하나의 함수를 만들고, 이 생성된 함수를 변수에 할당하는 방법  

```
var add = function(x,y) {
    return x+y;
}
add(3,4);
```

* 함수 명은 선택사항이다.  
* ```add```는 **함수 변수**라고 부른다.  
* ```add```는 함수의 참조값을 가지므로, 또 다른 변수에도 그 값을 그대로 할당할 수 있다. 같은 곳을 참조하게 된다.  
* 이렇게 생성된 함수를 사용하려면 **함수 변수**를 사용해야 한ㄷ.ㅏ  

**익명 함수**
* 이름이 없는 함수 형태  
* 익명 함수의 호출은 함수 변수에 ()를 붙여서 기술하는 것으로 가능하다.  

**기명 함수의 예**  
```
var add = function sum(x,y) {
    return x+y;
}

console.log(add(3,4)); // 7
console.log(sum(3,4)); // sum is not defined  
```
* 함수 표현식에서 사용된 함수 이름이 외부코드에서 접근 불가능하다.  
* 함수 표현식에서 사용된 함수 이름은 정의된 함수 내부에서 재귀적으로 호출하거나, 디버거에서 함수를 구분할 때만 사용한다.  

> **함수 선언문과 표현식에서의 세미콜론**  
> 선언문 방식은 세미콜론을 붙이지 않지만, 표현식의 경우는 붙이는 것을 권장한다.  

### Function() 생성자 함수를 통한 함수 생성  

```
new Function(arg1, arg2, ... argN, functionBody)  

var add = new Function('x', 'y', 'return x+y');
```
거의 사용하지 않음. 

### 함수 호이스팅  

함수 생성의 3가지 방식에는 차이가 있다. 그 중하나가 함수 호이스팅이다.  

**함수 표현식만을 사용할 것을 권장하고 있다.**  
그 이유 중 하나가 함수호이스팅 때문   

**함수 선언문 형태로 정의한 함수의 유효 범위는 코드의 맨 처음부터 시작한다.**  
-> 함수를 사용하기 정네 반드시 선언해야 한다는 규칙을 무시하므로 코드의 구조를 엉성하게 만들 수 있다.  
-> 함수 호이스팅이 발생하는 원인 : **자바스트립트의 변수 생성과 초기화의 작업이 분리되서 진행되기 때문에**

**함수 표현식 형태는 호이스팅이 일어나지 않는다.**  

## 함수 객체 : 함수도 객체다  

### 함수도 객체다  

기본 기능인 코드 실행 뿐만 아니라 프로퍼티들을 가질 수 있다.  

* **함수 코드**는 함수 객체의 **[[Code]] 내부 프로퍼티**에 자동으로 저장된다.  
* 함수의 프로퍼티도 일반 객체처럼 ```.```을 이용해서 접근할 수 있다.  

### 함수는 값으로 취급된다.  

일급 객체  
* 리터럴에 의해서 생성  
* 변수나 배열의 요소, 객체의 프로퍼티 등에 할당 가능  
* 함수의 인자로 전달 가능  
* 함수의 리턴값으로 리턴 가능  
* 동적으로 프로퍼티를 생성 및 할당 가능  

이 특성을 이용하여 함수형 프로그래밍이 가능하다.  

#### 변수나 프로퍼티의 값으로 할당  

```
//변수에 함수 할당  
var foo = 100;
var bar = function() { return 100; };
console.log(bar()); // 100  

// 프로퍼티에 함수 할당  
var obj = {};
obj.baz = function() { return 200; }
console.log(obj.baz()); // 200  
```

```foo```와 달리 ```bar```는 **함수의 참조값**을 저장하고 있으므로, ```bar()```라고 했을 때, 실제 함수 호출이 가능하다.  

#### 함수의 인자로 전달  

```
var foo = function(func) {
    func();
}

foo(function() {
    console.log("메롱");
}
```

```foo()```함수를 실행할 때, 함수 리터럴 방식으로 생성한 **익명 함수**를 ```func```인자로 넘겼다.  

#### 리턴값으로 활용  

```
var foo = function() {
    return function() {
        console.log('메롱');
    };
};

var bar = foo();
bar();

// 출력 결과 : 메롱  
```

### 함수 객체의 기본 프로퍼티  

Javascript에는 일반 객체와는 다르게 함수 객체만의 표준 프로퍼티가 정의되어 있다.  
함수를 정의하고 ```console.dir()```을 통해 개발자도구에서 확인해본다.  

```arguments```, ```caller```, ```length``` 등과 같은 프로퍼티가 생성되어 있다.  

![image](https://user-images.githubusercontent.com/54384004/74785434-a825d580-52ed-11ea-865e-4ccd9348c162.png)  

* EC5 명세에서는 모든 함수가 **length** **prototype** 프로퍼티를 가져야 한다고 기술한다.  
* length, prototype 외의 name, caller, arguments, __proto__ 프로퍼티는 ECMA 펴준은 아니다. 
    * name 프로퍼티는 함수의 이름을 나타낸다. 익명함수라면 빈 문자열이 된다.  
    * caller 프로퍼티는 자신을 호출한 함수를 나타낸다. 호출하지 않았다면 null이다.  
    * arguments 프로퍼티는 함수를 호출할 때 전달된 인자값을 나타낸다. 호출되지 않으면 null이다.(뒤에 자세한 설명 참고)  
    * __proto__ 프로퍼티
        * 모든 객체는 **[[Prototype]]**이라는 내부 프로퍼티를 가진다.  
        * 자신의 부모 역할을 하는 프로토타입 객체를 가리킨다.  
        * 함수 객체의 부모역할을 하는 프로토타입 객체를 **Function.prototype 객체**라고 명명했다. 이 역시 함수 객체이다.  
        * __proto__역시 함수 객체이므로, name, callse, arguments 등과 같은 함수 객체의 프로퍼티를 가지고 있음을 확인할 수 있다.  

> **Function.prototype 객체의 프로토타입 객체는?**  
> Function.prototype 객체도 결국는 함수라고 정의하고 있다.  
> ECMA 에서는 예외적으로 Function.prototype 함수 객체의 무조는 모든 객체의 조상인 **Object.prototype 객체**라고 설명한다.  
> 참고로 Function.prototype 객체는 모든 함수들의 부모 역할을 하는 프로토타입 객체다.  
> Function.prototype 객체가 가져야 하는 프로퍼티를 다음과 같이 기술한다.  
> * constructor 프로퍼티  
> * toString() 메서드  
> * **apply(thisArg, argArray) 메소드**  
> * **call(thisArg, [, arg1 [,arg2,]]) 메소드**  
> * bind(thisArg, [, arg1[,arg2,]]) 메소드  


#### length 프로퍼티  

함수가 정상적으로 실행될 때 기대되는 인자의 개수  

#### prototype 프로퍼티  

**내부 프로퍼티인 [[Prototype]]과 혼동하지 말 것**  

> [[Prototype]]는 **객체 입장에서 자신의 부모 역할을 하는 프로포타입 객체**  
> prototype 프로퍼티는 **이 함수가 생성자로 사용될 때 이 함수를 통해 생성된 객체의 부모역할을 하는 프로토타입 객체**  

* 함수가 생성될 때 만들어진다.  
* constructor 프로퍼티 하나만 있는 객체를 가리킨다.  
    * 이 프로퍼티는 자신과 연결된 함수를 가리킨다.  

> **프로포타입 객체 네이밍**  
> 함수의 prototype 프로퍼티가 가리키는 프로토타입 객체는 
> 따로 네이밍 하지 않고 자신과 연결된 함수의 prototype 프로퍼티 값을 그대로 이용한다. (add.prototype)  

```
function myFunc() {
    return true;
}

console.dir(myFunc.prototype);
console.dir(myFunc.prototype.contructor);  
```
![image](https://user-images.githubusercontent.com/54384004/74786180-6302a300-52ef-11ea-9ad6-b198ac085e33.png)

* myFunc.prototype 객체는 constructor와 __proto__라는 두개의 프로퍼티가 있다.  
* myFunc.prototype.constructor 를 보면 프로토타입 객체와 매핑된 함수를 볼 수 있고, 이는 ```myFunc``` 함수를 가리키고 있다.  

**함수 객체와 프로토타입 객체**는 서로 밀접하게 연결되어 있다.  

이 개념은 이후 프로토타입과 프로토타입 체이닝을 이해할 기본 지식인만큼 꼭 기억하자.  
(page 90 그림 4-9 참고)  

## 함수의 다양한 형태  

### 콜백 함수  

함수 이름은 꼭 붙이지 않아도 된다. <- 익명함수  
익명함수의 대표적인 용도  

단지 함수를 등록하기만 하고, 어떤 이벤트가 발생했거나 특정 시점에 도달했을 때 시스템에서 호출되는 함수.  
또는 어떤 함수의 인자로 넘겨서 코드 내부에서 호출되는 함수 또한 콜백함수가 된다.  

```
// 대표적인 예 : 이벤트 핸들러  
window.onload = function() {
    alert('메롱');
};
```

### 즉시 실행 함수  

[TIL - 즉시실행함수](https://github.com/yeoseon/tip-archive/issues/43) 참고  

함수를 정의함과 동시에 바로 실행하는 함수  

```
(function(name) {
    console.log('이게 바로 즉시실행 함수' + name);
})('foo');
// 이게 바로 즉시실행 함수foo  
```

* 함수 리터럴을 괄호로 둘러 싼다.  
* 함수가 바로 호출될 수 있게 () 괄호 쌍을 마지막에 추가하고, 그 안에 값을 추가하면 인자로 넘겨진다.  
* 같은 함수를 다시 호출할 수 없다. -> **최초 한번의 실행만을 필요로 하는 초기화 코드 부분** 등에 사용할 수 있다.  
* jQuery 와 같은 보통의 라이브러리들도 모든 코드가 즉시실행함수로 둘러싸여져 있다.  
    * 변수 유효범위 특성 때문이다.  
        * 함수 유효범위를 지원한다.  
        * 기본적으로 변수를 선언할 경우 프로그램 전체에서 접근할 수 있는 전역 유효범위를 가진다.  
        * 그러나 함수 내부에서 ```var```를 통해 정의된 변수들은 함수 코드 내부에서만 유효하다.(```var```를 통하지 않으면 함수 내부여도 전역에서 접근 가능하다.)  
    * 이 때문에, 여러 라이브러리를 쓰더라도 각 함수만의 유효범위를 갖게되어 변수명이 충돌 되는 등의 문제를 방지하지 않을 수 있다.(전역 네임스페이스를 더럽히지 않는다.)  

> **즉시 실행 함수 패턴**  
> 라이브러리 코드가 로드되면 실행되는 초기화 작업시 많이 사용된다.  

### 내부 함수  

함수 코드 내부에서도 다시 함수 정의가 가능하다.  
내부 함수는 클로저를 생성하거나 부모함수 코드에서 외부에서의 접근을 막고 독립적인 헬퍼 함수를 구현하는 용도 등으로 사용된다.  

```
function parent() {
    var a = 100;
    var b = 200;

    function child() {
        var b = 300;

        console.log(a);
        console.log(b);
    }
    child();
}

parent();
child();

//100
//300
//child is not defined  
```

#### 내부 함수에서는 자신을 둘러싼 부모 함수의 변수에 접근이 가능하다.  
* 스코프 체이닝 때문이다.  

#### 내부 함수는 일반적으로 자신이 정의된 부모 함수 내부에서만 호출이 가능하다.  
* 함수 스코핑 때문이다.  
* 함수 외부에서도 특정 함수 스코프 안에 선언된 내부 함수를 호출하려면, 내부함수를 외부로 리턴하는 등의 방법을 사용하여 가능하기도하다.  
    ```
    function parent() {
        var a = 100;

        var child = function() {
            console.log(a);
        }

        return child;
    }
    var inner = parent();
    inner();

    //100  
    ```  

    함수의 참조값을 가지므로 가능한 일  

    실행이 끝난 parent()와 같은 부모 함수 스코프의 변수를 참조하는 inner()와 같은 함수를 클로저라고 한다.  

### 함수를 리턴하는 함수  

일급 객체이므로 리턴할 수 있다.  

## 함수 호출과 this  

### arguments 객체  

JavaScript 에서는 함수를 호출할 때 함수 형식에 맞춰 인자를 넘기지 않더라도 에러가 발생하지 않는다.  

인자 보다 적게 함수를 호출했을 경우, 넘겨지지 않은 인자는 ```undefined```되고, 더 많은 인자를 넘길 경우 나머지 인자는 무시된다.  

이러한 특성 때문에 **런타임시에 호출된 인자의 개수를 확인하고 이에 따라 동작을 다르게 해줘야하는 경우가 있다.**  
이에 사용되는 것이 바로 arguments 객체이다.  

함수를 호출할 때 넘긴 인자들이 배열 형태로 지정된 객체를 의미한다.  
이는 **유사 배열 객체**이다.  

다음과 같이 세 부분으로 구성되어 있다.  
* 넘겨진 인자(배열 형태)  
* length : 인자의 개수  
* callee : 이 함수의 참조값  

### 호출 패턴과 this 바인딩  

자바스크립트에서 함수 호출시 기존 매개변수로 전달되는 인자값에 더해 **arguments 객체**와 **this 인자**가 함수 내부로 암묵적으로 전달된다.  

this는 확실히 이해해야하는 개념.  

함수가 호출되는 방식 (호출 패턴)에 따라 this가 다른 객체를 참조한다.(this 바인딩)  

#### 객체의 메서드를 호출할 때의 this 바인딩  

객체의 **프로퍼티**가 함수일 경우, 이 함수를 메서드라고 부른다.  
이 메서드를 호출할 때, 메서드 내부 코드에서 사용되는 ```this```는 **해당 메서드를 호출한 객체로 바인딩** 한다.  

```
var myObject = {
    name: 'foo',
    sayName: function() {
        console.log(this.name);
    }
};

var otherObject = {
    name: 'bar'
}

otherObject.sayName = myObject.sayName;  

myObject.sayName(); // foo
otherObject.sayName(); // bar  
```

#### 함수를 호출할 때의 this 바인딩  

프로퍼티가 아닌 그냥 함수를 호출할 때, ```this```는 **전역 객체에 바인딩**된다.  
브라우저에서는 **window 객체**가 될 것이다.  

> **전역 객체란?**  
> 브라우저 환경에서의 전역 객체는 ```window```가 된다.  
> Node.js 처럼 서버프로그래밍을 할 수 있도록 설계된 자바스크립트 런타임 환경에서의 전역 객체는 ```global```이 된다.  

**JavaScript의 모든 전역 변수는 전역 객체의 프로퍼티들이다.**  
```
var test = 'test'; //전역 변수

//모두 같다.
console.log(this.test); 
console.log(window.test); 
```

#### 내부 함수를 호출할 경우 **  

내부함수에서의 ```this```는 주의해야 한다.  

**Javascript 에서는 내부함수호출 패턴을 정의해놓지 않아서, 내부함수의 this는 전역 객체(window)에 바인딩 된다.**  

```
var value = 100;

var myObject = {
    value: 1,
    func1: function() {
        console.log(this.value); // 함수 프로퍼티(메서드)로 호출할 때의 this는 이 메소드를 호출한 객체를 가리키므로 1이 출력된다.  

        //func2() 내부 함수  
        func2= function() {
            this.value = 2;
            console.log(this.value); // 위와 같은 맥락으로 2가 출력될 것 같지만 내부함수의 경우 this가 전역객체가 되어 100이 출력된다.  
        }
    }
};
myObject.func1();
```

이 한계를 극복하기 위해 **부모함수(func1)의 this를 내부 함수가 접근 가능한 다른 변수에 저장하는 방법(that)이 사용된다.** 보통 ```that```이라고 명명한다.  

```
var value = 100;
var myObject = {
    value: 1,
    func1: function() {
        var that = this;
        
        func2: function() {
            console.log(that.value); // 1이 출력된다.  
        }
    }
}
```

#### 생성자 함수를 호출할 때의 this 바인딩  

[객체 인스턴스 생성 방식 - 3. 생성자 함수 이용](https://github.com/yeoseon/tip-archive/issues/47) 참고  

**기존 함수에 new 연산자를 붙여서 호출하는 방법**  
**함수 이름의 첫 문자를 대문자로 명명할 것**  


자바스크립트 객체는 자신을 생성한 **생성자 함수의 prototype 프로퍼티**가 가리키는 객체를 자신의 **프로토타입 객체([[Prototype]])로 설정**한다.  
* 객체 리터럴 방식 : 객체 생성자 함수는 **Object()**  
* 생성자 함수 방식 : 객체 **생성자 함수 자체**  

그러므로 두 방식으로 생성된 객체 인스턴스의 **프로토타입 객체([[Prototype]])** 가 다른 것이다.  

그래서 생성자 함수의 this는?  
* 생성자 함수 코드가 실행되기 전 생성된 빈 객체가 바로 생성자 함수가 새로 생성하는 객체이며, 이 객체가 바로 this이다.  
* 사실 빈 객체는 아니다. 기본적으로 자바스크립트의 모든 객체는 자신의 부모인 프로토타입 객체와 연결되어 있어, 자신의 메소드처럼 사용할 수 있기 때문에.  
* 생성자 함수가 생성한 객체는 자신을 생성한 **생성자 함수의 prototype 프로퍼티가 가리키는 객체**를 **자신의 [[Prototype]]객체**로 설정한다.  

#### 생성자 함수를 new를 붙이지 않고 호출할 경우? 

일반 함수와 생성자 함수에 대한 구분이 없다. 명명규칙으로 대문자를 사용할 뿐이다.  
생성자 함수로 사용할 목적으로 개발한 함수를 new 없이 호출할 경우 오류가 발생할 수 있다. this 바인딩 방식이 다르기 때문이다.  

**일반 함수 호출은 this가 window 전역 객체에 바인딩**  
**생성자 함수 호출의 this는 새로 생성되는 빈 객체에 바인딩**  

```
var qux = Person('qux', 20, 'man');  
console.log(qux); // undefined  

console.log(window.name); //qux  
```
* 일반 함수 방식으로 호출 했기에 this로 바인딩 된 window 객체에 프로퍼티가 생성된다.  
* Person() 함수는 리턴값이 특별히 없다. **생성자 함수 호출방식에서 리턴값이 없으면 새로 생성되는 객체가 리턴되지만, 일반 함수로 호출할 때는 undefined가 리턴된다.**  
따라서 qux를 출력했을 때 undefined가 출력되었다.  

> **네이밍 규칙만으로는 이런 에러를 방지하기가 어려워서 쓰는 방식**  
> ``` 
> function A (arg) {
>   if(!this instanceof A))
>       return new A(arg);
>   this.value = arg ? arg : 0;
> }
> ```  
> 어떤 코드에서는 A라고 함수 이름을 명시적으로 쓰지 않고 ```arguments.callee```라고 명시하기도 한다.  
> 곧 호출될 함수를 가리킨다.  
> 많은 라이브러리에 이 패턴이 들어가 있다.  

#### call 과 apply 메서드를 이용한 명시적인 this 바인딩  

this를 특정 객체에 명시적으로 바인딩하고 싶을 때 **함수 객체의 기본 프로퍼티**에서 제공하는 ```apply()```와 ```call()``` 메소드를 사용한다.  

Function.prototype 객체의 메서드이므로 모든 함수는 호출가능하다.  

본질적인 기능은 함수 호출이다.  

```
function.apply(thisArg, argArray)  

//thisArg : apply()메서드를 호출한 함수의 내부에서 사용한 this에 바인딩할 객체  
//함수에 넘길 인자 배열 <- call() 메소드는 배열을 쓰지 않고 인자로 모두 나열하는 것에 차이가 있다.  
```

```
function Person(name, age, gender) {
    this.name = name;
    this.age = age; 
    this.gender = gender;
}

var foo = {};

Person.apply(foo, ['foo', 30, 'man']);
console.dir(foo);
```

![image](https://user-images.githubusercontent.com/54384004/74886903-c27ab480-53bc-11ea-8418-f0f07145cd49.png)

this를 foo 객체에 명시적으로 바인딩하여서 foo 객체에 제대로 프로퍼티가 생성되었다.  

**유사 배열 객체에서 배열 메서드를 사용할 경우에 대표적으로 사용된다.**  
* 실제 배열이 아니므로 표준 배열 메서드를 사용할 수 없지만, apply()나 call()를 이용하면 가능하다.  
```
function myFunction() {
    console.dir(arguments);  
    //arguments.shift(); //에러 발생

    var args = Array.prototype.slice.apply(arguments);
    console.dir(args);
}

myFunction(1,2,3);  
```
* **Array.prototype.slice() 메서드를 호출해라. 이때 this는 arguments 객체로 바인딩 해라.**  
* arguments 객체가 Array.prototype.slice() 메서드를 마치 자신의 메서드인 양 arguments.slice()와 같은 형태로 메서드 호출하라는 뜻

> 나의 생각  
> this 바인딩이 함수 내 꼭 변수로만 쓰이위한 this가 아니라 실제 객체 프로퍼티 등의 형태도 똑같이 형성되도록 **바인딩**한다는 것에 의미를 더 두어야 겠다. 

실제 배열 변수와 arguments 유사 배열 객체에 대해 정보를 console.logging 해보면 argumentsd의 __proto__는 Object가 나오고, 배열은 Array[0]가 나온다.  

### 함수 리턴  

함수는 항상 리턴값을 반환한다.  

#### 규칙 1) 일반 함수나 메서드는 리턴값을 지정하지 않을 경우 undefined가 리턴된다.   

#### 규칙 2) 생성자 함수에서 리턴값을 지정하지 않을 경우 생성된 객체가 리턴된다.  

다른 객체나 배열을 명시적으로 리턴하면 해당 객체와 배열이 리턴된다.  
**객체가 아닌 기본 타입(불린, 숫자 문자열)을 리턴한 경우 이를 무시하고 this로 바인딩된 객체가 리턴된다.**  

## 프로토타입 체이닝  

### 프로토타입의 두 가지 의미  

**프로토타입 기반의 객체지향 프로그래밍을 이해하자.**  

객체 리터럴 또는 생성자 함수로 생성된 객체의 **부모 객체**를 **프로토타입 객체**라고 한다. -> 상속 개념과 마찬가지로 부모의 메소드를 사용할 수 있다.  

#### 암묵적 프로토타입 링크 ([[Prototype]])  
* 자바의 모든 객체는 자신의 부모인 프로토타입 객체를 가리키는 참조 링크 형태의 숨겨진 프로퍼티가 있다.  
* **prototype 프로퍼티**와 **[[Prototype]] 객체**를 구분할 필요가 있다.  
* **모든 객체는 자신을 생성한 생성자 함수의 prototype 프로퍼티가 가지는 프로토타입 객체를 자신의 부모 객체로 설정하는 [[Prototype]] 링크로 연결한다.**  

    ```
    function Person(name) {
        this.name = name;  
    }

    var foo = new Person('foo');
    ```

    ![image](https://user-images.githubusercontent.com/54384004/74988568-83626700-5481-11ea-96fd-b7e9b3dd8ba2.png)

* 그림을 보면 Person() 생성자 함수의 prototype 프로퍼티와 foo 객체의 __proto__  링크가 같은 프로토타입 객체를 가리키고 있다는 것을 알 수 있다.  
* Person() 생성자 함수는 prototype 프로퍼티로 자신과 링크된 **프로토타입 객체**를 가리킨다.  
* foo 객체는 Person() 함수의 프로토타입 객체를 [[Prototype]] 링크로 연결한다.  
* prototype 프로퍼티나 [[Prototype]] 링크는 같은 프로토타입 객체를 가리키고 있다.  
* **prototype 프로퍼티는 함수의 입장에서 자신과 링크된 프로토타입 객체를 가리키고 있으며, [[Prototype]] 링크는 객체의 입장에서 자신의 부모 객체인 프로토타입 객체를 내부에 숨겨진 링크로 가리키고 있다.**  
* 객체를 생성하는 건 생성자 함수의 역할이지만, 생성된 객체의 실제 부모 역할을 하는 건 생성자 자신이 아닌 생성자의 prototype 프로퍼티가 가리키는 프로토타입 객체다.  

__proto__ 프로퍼티는 모든 객체에 존재하는 숨겨진 프로퍼티로 **객체 자신의 프로토타입 객체**를 가리키는 참조링크 정보다.  

### 객체 리터럴 방식으로 생성된 객체의 프로토타입 체이닝  

자신의 부모 역할을 하는 프로토타입 객체의 프로퍼티 또한 자신의 것처럼 접근할 수 있다. 이것을 가능하게 하는 것이 **프로토타입 체이닝**이다.  

``` 
var myObject = {
    name: 'foo',
    sayName: function() {
        console.log(this.name);
    }
};

myObject.sayName(); // foo
console.log(myObject.hasOwnProperty('name')); // true
myObject.sayNickName(); // undefined
```

* ```hasOwnProperty()``` : 프로퍼티나 메서드가 있는지 확인하는 자바스크립트 표준 API 함수이다.  
    * myObject에는 위의 메소드가 없는데 어떻게 에러가 발생하지 않았는가?  
    * 객체 리터럴로 생성한 객체는 **Object()**라는 내장 생성자 함수로 생성된다.  
    * 이 Object() 생성자 함수도 함수 객체이므로, prototype 프로퍼티를 가진다.  
    * **myObject 는 Object() 함수의 prototype 프로퍼티가 가지는 Object.prototype 객체를 자신의 프로토타입 객체([[Prototype]])로 연결한다.**  

> 리터럴 방식으로 생성한 함수의 prototype 프로퍼티는 Object.prototype이고,  
> 생성자 방식으로 생성한 함수의 prototype 프로퍼티는 [생성자함수].prototype 이다.  
> 이 [생성자함수].prototype도 결국 함수 객체이므로, 최종적으로는 Object.prototype을 갖게 되겠다.  

#### 프로토타입 체이닝  

자바스크립트에서 특정 객체의 프로퍼티나 메서드에 접근하려고 할 때, **해당 객체에 접근하려는 프로퍼티나 메서드가 없을 경우 [[Prototype]]링크를 따라 자신의 부모 역할을 하는 프로토타입 객체의 프로퍼티를 차례대로 검색하는 것을 말한다.**  


Object.prototype 객체는 자바스크립트 모든 객체의 조상 역할을 하는 객체이다.  

### 생성자 함수로 생성된 객체의 프로토타입 체이닝   

기본 원칙은 같다.  
> **자바스크립트에서 모든 객체는 자신을 생성한 생성자 함수의 prototype 프로퍼티가 가리키는 객체를 자신의 프로토타입 객체(부모 객체,[[Prototype]])로 취급한다.**  

```
funcion Person(name, age, hobby) {
    this.name = name;
    this.age = age;
    this.hobby = hobby;
}

var foo = new Person('foo', 30, 'tennis');  

console.log(foo.hasOwnProperty('name')); //true 
```

* foo 개체의 생성자는 Person() 함수이다. foo 객체의 프로토타입 객체는 자신을 생성한 Person 생성자 함수 객체의 prototype 프로퍼티가 가리키는 객체(Person.prototype)가 된다. = foo 객체의 프로토타입 객체는 Person.prototype 프로퍼티가 된다.  
* foo.hasOwnProperty() 메소드를 호출했지만, foo 에는 없어서 프로토타입 체이닝을 통해 Person.prototype 객체에서 찾는다. 하지만 함수에 연결된 프로토타입 객체는 디폴트인 constuctor 밖에 없으므로 해당 메서드는 없다.  

    ![image](https://user-images.githubusercontent.com/54384004/74989412-9c6c1780-5483-11ea-8aa7-33f91a4aa883.png)

* 하지만 위의 그림을 봤을 때, **Person.prototype 역시 자바스크립트의 객체이므로 Object.prototype을 프로토타입 객체로 가진다.** 
* 따라서 프로토타입 체이닝은 Object.prototype 객체로 계속 이어진다.  

### 프로토타입 체이닝의 종점  

Object.prototype은 결국 프로토타입 체이닝의 종접이 된다.  

객체 리터럴 방식이나 생성자 함수 방식에 상관없이 모든 자바스크립트 객체는 프로토타입 체이닝으로 Object.prototype 객체가 가진 프로퍼티와 메서드에 접근하고 서로 공유가 가능하다.  

### 기본 데이터 타입 확장  

JavaScript의 숫자, 문자열, 배열 등에서 사용되는 표준 메서드는 Number.prototype, String.prototype, Array.prototype 등에 정의되어 있다.  
이 내장 프로토타입 객체 또한 Object.prototype을 자신의 프로토타입으로 가지고 있어서 체이닝으로 연결된다.  

#### JavaScript는 표준 빌트인 프토토타입 객체에서 사용자가 직접 정의한 메서드를 추가하는 것을 허용한다.  

```
String.prototype.testMethod = function() {
    console.log('test');
}

var str = '메롱';  
str.testMethod(); //test
```

### 프로토타입도 자바스크립트 객체다.  

함수가 생성될 때 자신의 prototype 프로퍼티에 연결되는 프로토타입 객체는 디폴트로 construnctor 프로퍼티만을 가진 객체다.  
하지만 당연히 이 프로토타입 객체 역시 자바스크립트 객체이므로 일반 객체처럼 동적으로 프로퍼티를 추가/삭제하는 것이 가능하다. 이 역시 체이닝에 반영된다.  

```
function Person(name) {
    this.name = name;
}

var foo = new Person('foo');

//foo.sayHello(); //에러  

Person.prototype.sayHello = function() {
    console.log('Hello');
}
foo.sayHello(); // Hello 
```

### 프로토타입 메서드와 this 바인딩  

프로토타입 메서드 내부에서 this를 사용한다면??  

앞에서 배운 규칙을 그대로 적용하면 된다.  
**메서드 호출 패턴에서의 this는 그 메서드를 호출한 객체에 바인딩 된다.**  

```
function Person(name) {
    this.name = name;
}

Person.prototype.getName = function() {
    return this.name;
}

var foo = new Person('foo');

console.log(foo.getName()); //foo

Person.prototype.name = 'person';

console.log(Person.prototype.getName()); // person  
```

* getName을 호출한 객체가 foo일 경우, this는 foo에 바인딩된다.  
* Person.prototype.getName() 메서드처럼 프로토타입 체이닝이 아니라 바로 Person.prototype 객체에 접근해서 getName() 메서드를 호출하면, getName()을 호출한 객체는 Person.prototype 이므로 this도 여기에 바인딩 된다.  

### 디폴트 프로토타입은 다른 객체로 변경 가능하다.   

디폴트 프로토타입 객체는 함수가 생성될 때 같이 생성되며, 함수의 prototype 프로퍼티에 연결된다.  
이 디폴트 프로토타입 객체를 다른 일반 객체로 변경하는 것이 가능하다.  
이를 이용해 상속을 구현한다.  

**생성자 함수의 프로토타입 객체가 변경되면 변경된 시점 이후에 생성된 객체만 변경된 프로토타입 객체로 [[Prototype]] 링크를 연결한다. 변경되기 전 기존의 객체들은 기존 프로토타입 객체로의 [[Prototype]] 링크를 그대로 유지한다**  

```
function Person(name) {
    this.name = name;
}
console.log(Person.prototype.constructor);   // Person(name)

var foo = new Person('foo');
consol.log(foo.country);    // undefined

Person.prototype = {
    country: 'korea',
};

console.log(Person.prototype.constructor);      // Object()

var bar = new Person('bar');
console.log(foo.country);   // undefined
console.log(bar.country);   // korea
console.log(foo.constructor);   // Person(name)
console.log(bar.constructor);   // Object()
```
* Person() 함수를 생성할 때 Person.prototype 객체는 자신과 연결된 Person() 생성자 함수를 가리키는 constructor 프로퍼티만을 가진다.  
* foo 객체는 Person.prototype 객체를 자신의 [[Prototype]]으로 연결했다.  
* 객체 리터럴 방식을 통해 country 프로퍼티를 가진 객체로 프로토타입 객체를 변경했다.  
* Person.prototype.constructor는 바꾼 객체(얘도 결국은 객체)에 contructor 프로퍼티가 없으므로 체이닝을 통해 Object.prototype.constructor를 가져올 것이다.
* bar 객체를 이제 생성하면, 디폴트 프로토타입 객체가 아닌 변경된 프로토타입 객체를 가리키고 있다.  

### 객체의 프로퍼티 읽기나 메서드를 실행할 때만 프로토타입 체이닝이 동작한다.  

객체의 특정 프로퍼티를 **읽으려고 할 때,** 프로퍼티가 해당 객체에 없는 경우 프로토타입 체이닝이 발생한다.  
객체에 있는 특정 프로퍼티에 값을 **쓰려고 한다면** 프로토타입 체이닝일 일어나지 않고, 동적으로 객체에 프로퍼티를 추가한다.  

# 05 실행 컨텍스트와 클로저  

## 실행 컨텍스트 개념  

콜 스택과 같이 생각해보자.  
**실행 가능한 코드를 형상화 하고 구분하는 추상적인 개념**  
**실행 가능한 자바스크립트 코드 블록이 실행되는 환경**  

실행 컨텍스트 안에 실행에 필요한 여러가지 정보를 담고 있다.  
위에서 말하는 코드 블록은 대부분의 경우 함수가 된다.  

ES에서 규정하는 실행 컨텍스트가 형성되는 경우  
1. 전역 코드  
2. eval()로 실행되는 코드  
3. 함수 안의 코드를 실행할 경우  

함수로 실행 컨텍스트를 만든다 -> 코드 블록 안에 변수, 객체, 실행 가능한 코드가 들어있다. -> **코드가 실행되면 실행 컨텍스트가 생성** -> 실행 컨텍스트는 **스택 안에 하나씩 차곡차곡 쌓이고** -> **제일 위에 위치하는 실행 컨텍스트가 현재 실행되고 있는 컨텍스트**이다.  

> **현재 실행되는 컨텍스트에서 이 컨텍스트와 관련 없는 실행 코드가 실행되면 새로운 컨텍스트가 생성되어 스택에 들어가고 제어권이 그 컨텍스트로 이동한다.**  


**전역 실행 컨텍스트**  
가장 먼저 실행되는 실행 컨텍스트이다.  

## 실행 컨텍스트 생성 과정  

* 활성객체와 변수 객체  
* 스코프 체인  

```
function execute(param1, param2) {
    var a = 1, b = 2;
    function func() {
        return a+b;
    }
    return param1 + param2 + func();
}

execute(3,4);  
```

다음 예제를 보고 실행 컨텍스트가 어떻게 생성되는지 차례대로 살펴본다.  

자바스크립트에서 함수를 실행하여 실행 컨텍스트가 생성되었다.  

### 활성객체 생성  

실행 컨텍스트가 생성되면 해당 컨텍스트에서 실행에 필요한 여러가지 정보를 담을 객체를 생성하는데, 이를 활성객체라고 한다.  

사용하게 될 매개변수, 사용자 정의 변수 및 객체 등을 저장하고 새로 만들어진 컨텍스트로 접근 가능하게 되어있다.    
이는 엔진 내부에서 접근할 수 있다는 말.  

### arguments 객체 생성  

활성 객체는 arguments 프로퍼티로 이 arguments 객체를 참조한다.  
(인자 정보를 저장하는 프로퍼티)  

### 스코프 정보 생성  

**유효 범위**를 나타내는 스코프 정보를 생성한다.  
연결리스트와 유사한 형식으로 만들어진다.  
현재 컨텍스트에서 **특정 변수에 접근해야 할 경우, 이 리스트를 활용한다.**  
**현재 컨텍스트의 변수 뿐만 아니라 상위 컨텍스트의 변수로 접근 가능하다.**  
여기서 찾지 못하면 정의되지 않은 변수로 판단하고 에러를 검출한다.  

이 정보를 스코프 체인이라고 하고, **[[scope]]** 프로퍼티로 참조된다.  

**현재 생성된 활성 객체가 스코프 체인 제일 앞에 추가되며, execute() 함수의 인자나 지역 변수 등에 접근할 수 있다.**  

### 변수 생성  

현재 실행 컨텍스트 내부에서 사용되는 **지역 변수의 생성**  
이 변수를 저장하는 **변수 객체가 바로 활성 객체**  

변수 객체 안에서 호출된 함수인자는 각각의 프로퍼티가 만들어지고, 그 값이 할당된다.  
값이 넘겨지지 않으면 undefined가 할당된다. (인자대로 함수를 수행할 필요 없다는 특징 참고)  

이 과정에서는 **단지 메모리에 생성**만 할뿐 초기화는 변수나 함수에 해당하는 표현식이 실행될 때 수행된다.  
그래서 먼저 undefined가 할당된다.  
표현식 실행은 변수 객체 생성이 다 이루어진 후 시작된다.  

### this 바인딩  

마지막 단계에서는 this 키워드를 사용하는 값이 할당된다.   
this가 참조하는 객체가 없으면 전역 객체를 참조한다.  

### 코드 실행  

이제 표현식의 실행이 이루어지며, 변수의 초기화 및 연산, 또 다른 함수 실행 등이 이루어진다.  

#### 전역 실행 컨텍스트  
* 일반적인 실행 컨텍스트와 달리 arguments 객체가 없다.  
* 전역 객체 하나만을 포함하는 스코프 체인이 있다.  
* ES에서 규정한 실행 컨텍스트가 형성되는 3가지중 1번째인 전역코드에서 생성되는 컨텍스트가 바로 이 전역실행 컨텍스트이다.  
* 변수를 초기화하고 이것의 내부 함수는 일반적인 탑 레벨의 함수로 선언  
* 전역 실행 컨텍스트에서의 변수 객체가 곧 전역 객체  
* **전역적으로 선언된 함수와 변수가 전역 객체의 프로퍼티가 되는 것**  

> **브라우저에서는 최상위 코드가 곧 전역 코드지만 node.js에서는 다르다.**  
> node.js에서는 최상위에 변수를 선언해도 그 모듈의 지역변수가 된다.  
> ```var```를 사용하지 않을 경우에만 전역 객체인 global에 들어간다. (이건 사용안하는게 좋다.)  

## 스코프 체인  

현재 사용되는 변수가 어디에서 선언된 변수인지 정확히 알 수 있다.  

자바스크립트는 ```for(){}```, ```if{}```와 같은 구문에 대해서는 유효범위가 없다.  
**오직 함수**만이 유효 범위의 한 단위가 된다.  

이 유효범위를 나타네는 스코프가 [[scope]] 프로퍼티로 연결리스트 형식으로 관리되는데, 이것을 **스코프 체인**이라고 한다.  

**각 함수는 [[scope]] 프로퍼티로 자신이 생성된 실행 컨텍스트의 스코프 체인을 참조한다.**  

함수가 실행되는 순간 실행 컨텍스트가 만들어지고, 이 실행컨텍스트는 실행된 함수의 [[scope]] 프로퍼티를 기반으로 새로운 스코프 체인을 만든다.  

**책의 그림들을 참고할 것(p.148~)**  

### 전역 실행 컨텍스트의 스코프 체인  

```
var var1 = 1;
var var2 = 2;
console.log(var1);
console.log(var2);  
```

* 함수 선언 X -> 함수 호출 X  
* 전역 실행 컨텍스트 생성, 변수 객체 생성  
* 전역 실행 컨텍스트 단 하나만 실행되고 있어 참조할 상위 컨텍스트 없음.  
* 이 변수 객체는 최상위에 위치하는 변수객체.  
* 스코프체인은 **자기 자신**만을 가진다.  

### 함수를 호출할 경우 생성되는 컨텍스트의 스코프 체인  

```
var var1 = 1;
var var2 = 2;
function func() {
    var var1 = 10;
    var var2 = 20;  
    console.log(var1); //10 
    console.log(var2); //20
}
func();
console.log(var1); //1
console.log(var2); //2
```

* 전역 실행 컨텍스트 생성
* func() 함수객체 생성  
    * func()의 [[scope]]는??  
        * **그 함수 객체의 [[scope]]는 현재 실행되는 컨텍스트의 변수 객체에 있는 [[scope]] 객체를 그대로 가진다.**  
        * func 함수 객체의 [[scope]]는 전역 변수 객체가 된다.  
* func() 함수를 **실행**
    * 새로운 컨텍스트 생성 (func 컨텍스트)  
    * func 컨텍스트의 스코프 체인은 실행된 함수의 [[scope]] 프로퍼티를 **그대로 복사**한다.  
    * **그 다음, 현재 생성된 변수 객체를 복사한 스코프 체인 맨 앞에 추가한다.**  
    * func 실행 컨텍스트의 스코프 체인은 [func 변수 객체 - 전역 객체]가 된다.  

#### 정리  
* 각 함수 객체는 [[scope]] 프로퍼티로 현재 컨텍스트의 스코프 체인을 참조한다.  
* 한 함수가 실행되면, 새로운 실행 컨텍스트가 만들어진다. 현재 실행되는 함수 객체의 [[scope]] 프로퍼티를 복사하고, 새롭게 생성된 변수 객체를 해당 체인의 제일 앞에 추가한다.  
* **스코프 체인 = 현재 실행 컨텍스트의 변수 객체 + 상위 컨텍스트의 스코프 체인**  

다음 예제의 결과를 예상해보자.  
```
var value = "value1";

function printFunc() {
    var value = "value2";

    function printValue() {
        return value;
    }
    
    console.log(printValue());
}

printFunc();
```
* 각 함수 객체가 처음 생성될 당시 실행 컨텍스트가 무엇인지를 생각해야 한다.  
* 처음 생성될 때 [[scope]]는 전역 객체의 [[scope]]를 참조한다.  
* 각 함수가 실행될 때 생성되는 실행 컨텍스트의 스코프 체인은 전역 객체와 그 앞에 새롭게 만들어진 변수 객체가 추가된다.  

### 식별자 인식  

이렇게 만들어진 스코프 체인을 통해 식별자 인식이 이루어진다.  

첫번째 변수 객체부터 식별자 인식을 시작하여, 대응되는 이름을 가진 프로퍼티가 있는지 확인한다.  
첫번째 변수 객체는 곧 이 객체에 있는 공식 인자, 내부 함수, 지역 변수에 대응 되는 지를 확인하는 것이다.  
첫번째 객체에 없으면 다음 객체로 이동하여 찾을 때까지 계속 검색한다.  
**this는 식별자가 아닌 키워드로 분류되어 스코프 체인의 참조 없이 접근할 수 있다.**  

> **스코프 체인을 임의로 수정할 수 있는 ```with```**  
> ```eval```과 함께, 성능을 생각한다면 절대 사용하지 말아야할 키워드.  
> 표현식을 실행하는데, 표현식이 객체이면 객체는 현재 실행 컨텍스트의 스코프 체인에 추가된다.  


> **함수 호이스팅을 이해하자.**  
> ```
> foo();
> bar();
> 
> var foo = function() {
>    console.log("foo and x = " + x);
> };
> function bar() {
>    console.log("bar and x = " + x);
> }
> var x = 1;  
> ```  
> 함수 생성과정에서 변수 foo, 함수 객체 bar, 변수 x를 차례대로 생성한다.  
> foo 와 x 에는 undefined가 할당된다.  
> 실행이 시작되면 foo, bar를 연속해서 호출한다.  
> foo 에 함수 객체의 참조가 할당되고, 변수 x에 1이 할당된다.  
> foo에서 TypeError가 발생한다.  
> foo가 선언되어 있기는 하지만 함수가 아니기 때문이다.  
> bar()에서는 "bar and x = undefined"가 출력된다.  
> x에 1이 할당되기 전에 실행했기 때문이다.  

## 클로저

### 클로저의 개념  

``` 
function otherFunc() {
    var x = 10;
    var innerFunc = function() {
        console.log(x);
    }
    return innerFunc;
}

var inner = outerFunc();
inner(); //10
```
* innerFunc() 의 [[scope]]은 outerFunc 변수 객체와 전역 객체를 가진다.  
* outerFunc()이 끝난 후 실행되는데, outerFunc의 실행 컨텍스트가 사라진 후에 innerFunc의 실행 컨텍스트가 생성되는 것인데, 스코프 체인은 여전히 outerFunc의 변수 객체를 참조한다?  
* outerFunc 실행 컨텍스트는 사라졌지만, outerFunc 변수 객체는 여전히 남아있고, innerFunc의 스코프 체인으로 참조되고 있다. 이게 바로 **클로저**  

자바스크립트 함수는 일급 객체로 취급된다.  
최종 반환되는 함수가 외부 함수의 지역 변수에 접근하고 있다는 것이 주요하다.  
이 지역변수에 접근하려면 함수가 종료되어 외부 함수의 컨텍스트가 반환되더라도 **변수 객체는 반환되는 내부 함수의 스코프 체인에 그대로 남아있어야 접근할 수 있다.**  

**이미 생명 주기가 끝난 외부 함수의 변수를 참조하는 함수를 클로저라고 한다.**  
**클로저로 참조되는 외부 변수를 자유변수라고 한다.**  

위의 예시가 클로저의 전형적인 패턴이다.  
* 외부 함수에서 새로운 함수가 반환된다.  
* 이 반환된 함수가 클로저이다.  
* 클로저는 자유변수를 묶고 있다.  
* 반환된 클로저는 새로운 함수로 사용된다.  
* 이 패턴을 통해 함수형 프로그래밍이 가능하다.  

```
function outerFunc(arg1, arg2) {
    var local = 8;
    function innerFunc(innerArg) {
        console.log((arg1 + arg2)/(innerArg + local));
    }

    return innerFunc;
}

var exam1 = outerFunc(2, 4);
exam1(2);
```
* outerFunc() 함수를 호출하고 반환되는 함수 객체인 innerFunc()가 exam1 으로 참조된다. 이것은 exam1(n)의 형태로 실행될 수 있다.  
* outerFunc()가 실행되면서 생성되는 변수객체가 스코프체인에 들어가게 된다.  
* 이 스코프 체인은 innerFunc()의 스코프 체인으로 참조된다.  
* outerFunc()의 함수가 종료되었지만, 여전히 내부 함수(innerFunc())의 [[scope]]로 참조되므로 가비지 컬랙션 대상이 되지 ㅇ낳는다.  
* 따라서 이후에 exam1(n)을 호출하여도 innerFunc()에서 참조하고자 하는 변수 local에 접근할 수 있다.  
이 outerFunc 변수 객체의 프로퍼티 값은 읽기 및 쓰기 까지 가능하다.  

> **클로저의 성능**  
> innerfunc()에서 접근하는 변수 대부분이 스코프 체인의 첫번째 객체가 아닌 그 이후의 객체에 존재한다.  
> 이는 성능 문제를 유발시킬 수 있다.  
> 대부분의 클로저에서는 스코프 체인에서 뒤쪽에 있는 객체에 자주 접근한다.  
> 클로저를 영리하게 사용하려면 경험이 많이 필요하다.  

### 클로저의 활용  

#### 특정 함수에 사용자가 정의한 객체의 메서드 연결하기  

```
function HelloFunc(func) {
    this.greeting = "hello";
}

HelloFunc.prototype.call = function(func) {
    func ? func(this.greeting) : this.func(this.greeting);
}

var userFunc = function(greeting) {
    console.log(greeting);
}

var objHello = new HelloFunc();
objHello.func = userFunc;
objHello.call();  // hello
```
* HelloFunc은 greeting 변수가 있고 func 프로퍼티로 참조되는 함수를 call() 함수로 호출한다.  
* 사용자는 func 프로퍼티에 자신이 정의한 함수를 참조시켜 호출할 수 있다.  
* HelloFunc.prototype.call()을 보면 자신의 지역 변수인 greeting 만을 인자로 사용자가 정의한 함수에 넘긴다.  
* 사용자는 userFunc() 함수를 정의해서 objHello.func()에 참조시킨뒤, HelloFunc()의 지역변수인 greeting을 화면에 출력시킨다.  
* HelloFunc()은 greeting 만을 인자로 넣어 사용자가 인자로 넘긴 함수를 실행시킨다. 그래서 사용자가 정의한 함수로 한 개의 인자를 받는 함수를 정의할 수 밖에 없다.  
* 인자를 더 넣어서 HelloFunc()을 이용하여 호출하는 예제는 아래를 본다.  

> 어렵다. 내가 이해한 내용  
> func 함수가 바로 클로저.  
> greeting이 자유변수  
> 왜 그런진 모르지만 HelloFunc의 func **프로퍼티**가 있다.  
> 이 프로퍼티로 참조되는 함수를 HelloFunc.prototype.call을 통해 호출할 수 있다.  
> 사용자는 func 프로퍼티에 자신이 정의한 함수를 참조시켜 호출할 수 있다.  
> 여기서 HelloFunc의 자유변수인 greeting에도 접근이 가능한 것.  

```
function saySomething(obj, methodName, name) {
    return (function(greeting) {
        return obj[methodName](greeting, name);
    });
}

function newObj(obj, name) {
    obj.func = saySomething(this, "who", name);
    return obj;
}

newObj.prototype.who = function(greeting, name) {
    console.log(greeting + " " + (name || "everyone"));
}
```

* newObj()는 HelloFunc() 객체를 좀 더 자유롭게 활용하려고 정의한 함수  
* 첫번째 인자인 obj는 HelloFunc()의 객체가 되고, 두번째 인자는 사용자가 출력을 원하는 사람 이름이 된다.  
* newObj() 함수의 객체를 다음과 같이 만든다.  
```
var obj1 = new newObj(objHello, "zzoon");
```
* 첫번째 인자 obj의 func 프로퍼티에 saySomething() 함수에서 반환되는 함수를 참조하고, 반환한다.  
* 결국 obj1은 인자로 넘겼던 objHello 객체에서 func 프로퍼티에 참조된 함수만 바뀐 객체가 된다.  
```
obj1.call(); //따라서 이렇게호출이 가능하다.(newObj.prototype.who 호출)// hello zzoon
```

* saySomething() 함수 안에서 어떤 작업이 수행되는가? 
```
function saySomething(obj, methodName, name) {
    return (function(greeting) {
        return obj[methodName](greeting, name);
    });
}
```
* 첫번째 인자: newObj 객체 - obj1
* 두번째 인자 : 사용자가 정의한 메서드 이름 : who
* 세번째 인자 : 사용자가 원하는 사람 이름 값 : zzoon  
* 반환 : 사용자가 정의한 newObj.prototype.who() 함수를 반환하는 helloFunc()의 func 함수  

이렇게 반환되는 함수가 HelloFunc이 참조하는 function(greeting){} 형식의 함수가 되는데, 이것이 HelloFunc 객체의 func으로 참조된다.  
obj1.call()로 실행되는 것은 실질적으로 newObj.prototype.who()가 된다.  

**자신의 객체 메서드인 who 함수를 HelloFunc에 연결시킬 수 있다.**  
**여기서 클로저는 saySomething() 에서 반환되는 function(greeting){}이 되고, 이 클로저는 자유 변수 obj, methodName, name을 참조한다.**  

앞 예제는 정해진 형식의 함수를 콜백해주는 라이브러리가 있을 겨우, 그 정해진 형식과는 다른 형식의 사용자 정의 함수를 호출할 때 유용하게 사용한다.  

conclick, onmouseover과 같은 프로퍼티에 해당 이벤트 핸들러를 사용자가 정의해놓을 수가 있는데, 이 형식은 function(event){} 이다.  
여기에서 event 외의 원하는 인자를 더 추가한 이벤트 핸들러를 사용하고 싶을 때 앞 예제와 같은 방식으로 클로저를 활용할 수 있다.  

### 함수의 캡슐화  




