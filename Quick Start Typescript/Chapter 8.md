# Chapter 8. 모듈

## 8.1 모듈에 대한 이해

### 8.1.1 모듈에 대한 이해와 필요성

모듈 = **독립 가능한 기능의 단위**  
프로그램은 여러 모듈로 구성돼 있고 모듈을 결합해 하나의 프로그램을 만듦
모듈의 장점

1. 유지보수의 용이성
2. 전역 스코프 오염을 방지
3. 재사용성 향상

- 유지보수의 용이성
  애플리케이션을 개발할 때 모듈을 사용하지 않으면 같은 연산을 수행하는 중복 코드들이 생김  
  중복 코드는 유지보수를 어렵게 함  
  자주 사용하는 공통 기능을 모듈로정의해 사용하면 애플리케이션의 전체적인 수정 없이 모듈의 수정이나 교체만으로도 코드를 효과적으로 수정 가능

- 전역 스코프 오염을 방지
  전역 스코프는 전역 이름 공간을 가지므로 변수 이름이나 함수 이름을 중복해 선언할 수 없음  
  but, 변수나 함수 등을 파일 내부에 한정해 모듈로 선언하면 이름 공간이 파일 단위로 제한되며 전역 이름 공간을 침범하지 않음

- 재사용성 향상
  모듈은 프로젝트에서 자주 사용되는 공통 기능으로, 호출될 가능성이 높음  
  모듈화를 잘 해 두면 현재의 프로젝트뿐 아니라 다른 프로젝트에도 공유해 재사용 가능

##### 모듈러 프로그래밍을 위한 접근

모듈러 프로그래밍이란, 프로그램의 설계 기술로 **모듈의 분리와 모듈의 손쉬운 교체에 관심이 있음**  
모듈러 프로그래밍 방식으로 프로그램을 잘 구축하려면 상호 교환 가능한 모듈을 정의할 수 있어야 함  
모듈러 프로그래밍 개발 과정

1. 모듈을 식별함
2. 모듈을 분리해 선언함
3. 모듈을 외부로 공개함

- 모듈을 식별함
  모듈의 식별은 프로젝트 설계와 분석만으로는 어려움이 있음  
  공통 기능이 무엇인지는 실제로 구현하는 과정에서 식별될 가능성이 큼

- 모듈을 분리해 선언함
  함수 내부에서 발견되는 공통 기능은 모듈로 분리가 가능  
  모듈로 공통 기능을 분리하면 중복 코드가 줄어들고 각 함수의 역할이 더욱 분명해짐  
  또한 모듈 단위로 테스트가 쉬워지므로 에러가 발생할 확률 감소

- 모듈을 외부로 공개함
  모듈을 외부로 공개함으로써 프로젝트 내에 존재하는 특정 파일에서 호출해 사용할 수 있게 함  
  모듈을 외부로 공개할 때 모듈을 사용하기 쉽도록 모듈의 이름 등을 형식에 맞춰 선언해야 함  
  형식적으로 잘 정의된 모듈은 모듈 간의 결합을 더 쉽게 함

### 8.1.2 내부 모듈과 외부 모듈

모듈은 두 가지로 나뉨

1. 내부 모듈
2. 외부 모듈

**내부 모듈은 네임스페이스를 의미하고 외부 모듈은 export라고 선언해 외부로 공개된 모듈을 말함**

네임 스페이스는 여러 파일에 걸쳐 하나의 이름 공간을 공유, 외부 모듈은 모듈 파일마다 이름 공간이 정해짐

##### 내부 모듈

내부 모듈인 네임 스페이스는 **전역 이름 공간과 분리된 네임스페이스 단위의 이름 공간**  
따라서 같은 네임스페이스의 이름 공간이라면 파일 B가 파일 A에 선언된 모듈을 참조할 수 있는데 참조할 때는 별도의 참조문을 선언하지 않아도 됨  
파일이 다르더라도 프로젝트 내에서 같은 네임스페이스 내에서는 이름을 중복해 클래스, 함수, 변수 등 선언 X  
반대로 네임스페이스가 다르면 이름이 같아도 이름 충돌이 없음

네임스페이스는 전역 스코프에 속하지만 전역 스코프와 독립된 이름 공간

##### 외부 모듈

외부 모듈 = **export로 선언한 모듈**  
export 키워드를 이용해 외부 모듈로 선언할 수 있는 대상은 변수, 함수, 클래스 심지어 네임스페이스도 가능  
외부 모듈의 이름 공간은 파일 내부로 제한됨

export를 생략해 외부 모듈로 선언하지 않으면 **전역 스코프의 이름 공간을 공유해 이름 충돌이 발생**

타입스크립트는 모듈 선언과 모듈 호출에 있어서 표준인 ES2015 모듈을 지원  
모듈의 선언과 호출을 표준에 맞춰 사용하면 컴파일러가 표준 형식을 인식할 수 있게 돼 다른 모듈 형식으로 변환할 수 있음  
타입스크립트는 module 옵션을 통해 다른 모듈 형식으로 변환할 수 있도록 지원

모듈 변환을 위한 명령어: tsc --module <모듈 형식> <변환할 파일명>

module 옵션에서 사용할 수 있는 모듈 형식

- commonjs
- amd
- system
- umd
- es2015 또는 es6

## 8.2 네임스페이스

### 8.2.1 네임스페이스에 대한 이해

네임스페이스는 하나의 독립된 이름 공간을 만들고 여러 파일에 걸쳐 하나의 이름 공간을 공유할 수 있음  
네임스페이스는 namespace 키워드를 이용해 선언

네임스페이스와 똑같은 역할을 하는 키워드: module  
namespace와 module은 키워드는 다르지만, **역할과 기능상에는 차이가 없음**

##### namespace와 module의 선언과 컴파일 결과 확인

namespace와 module은 동작과 기능상의 차이가 없고 심지어 컴파일 결과도 차이가 없음

namespace와 module은 정확히 똑같은 코드로 변환됨  
내부 모듈은 자바스크립트(ES6)로 컴파일될 때 즉시 실행 함수로 변환됨

### 8.2.2 한 파일에 여러 네임스페이스 선언하기

네임스페이스는 보통 여러 파일에 걸쳐 하나의 이름 공간을 공유하는데 특정 파일에만 네임스페이스를 선언하거나 특정 파일에 여러 네임스페이스를 함께 선언해도 문제가 되지 않음

자바스크립트는 코드가 순차적으로 실행되는 특성이 있음  
이러한 특성을 생각해 보며 상위에 있는 네임스페이스에서 하위에 선언된 네임스페이스로 접근할 수 없어야 함  
하지만 실제로는 자바스크립트의 순차적인 실행 특성과 관계없이 자유롭게 호출할 수 있음  
이 이유는 ES6로 컴파일된 코드가 var로 선언되었기 때문에 호이스팅이 일어나는 것

### 8.2.3 네임스페이스 하나를 여러 파일을 선언하기

프로젝트 규모가 커지면 파일 단위로 모듈을 분할해야 함  
이때 네임스페이스를 이용하면 여러 파일에 걸쳐 하나의 네임스페이스의 이름 공간을 공유할 수 있음

타입스크립트는 네임스페이스를 이용해 논리적 그룹화를 제공  
논리적 그룹화는 네임스페이스의 이름만 같다면 컴파일 시에 하나의 논리적 영역으로 묶어 컴파일할 수 있게 함  
따라서 같은 프로젝트에 속해 있으면서 같은 네임스페이스면 명시적으로 참조 경로를 추가하지 않아도 tsc 명령어만으로 타입스크립트 컴파일러가 알아서 네임스페이스 간의 참조 관계를 고려해 컴파일함

##### 참조 경로를 추가하는 상황

tsc 명령어는 프로젝트에 속한 모든 \*.ts 파일을 대상으로 프로젝트 단위 컴파일을 수행하므로 네임스페이스를 명시적으로 참조하지 않아도 됨  
but, 프로젝트 단위 컴파일을 수행하지 않고 특정 파일만을 컴파일할 때는 같은 네임스페이스라도 외부에 선언된 네임스페이스를 인식할 수 없음

참조 경로는 트리플 슬래시를 사용해 선언함

```typescript
/// <reference path="---.ts "/>
```

참조 경로를 추가하면 컴파일러가 해당 파일이 참조하는 외부 파일이 무엇인지를 인식할 수 있게 됨

### 8.2.4 네임스페이스 모듈

**네임스페이스는 export를 이용해 모듈로 선언할 수 있음**  
모듈로 선언된 네임스페이스는 import 문을 이용해 JS로 컴파일된 뒤에도 명시적으로 모듈 호출을 할 수 있음

### 8.2.5 네임스페이스의 이름 확장

네임스페이스 이름은 알파벳의 소문자와 대문자를 사용해 다음처럼 선언함

```typescript
namespace Animal { ... }
```

네임스페이스 이름은 예외로 **점을 허용**함  
점을 이용하면 네임스페이스 간의 이름 계층을 만드는 효과가 있음

```typescript
namespace Animal.Land { ... }
```

Animal 네임스페이스와 Animal.Land 네임스페이스는 서로 다른 이름 공간임

이름 공간은 다르지만 논리적인 이름 순서상 상위 이름은 앞에 선언돼야 하고 하위 이름은 상대적으로뒤에 선언돼야 함

```typescript
namespace Animal { ... }
namespace Animal.Pet { ... }
```

한 파일 내에 여러 네임스페이스가 선언돼 있을 때 네임스페이스의 선언 위치에 상관없이 서로 참조할 수 있기 때문에 순서를 바꿔 선언해도 문제 X

### 8.2.6 브라우저에서 네임스페이스의 모듈 호출

여러 타입스크립트 파일을 컴파일할 때 런타임 시에 타입스크립트 파일을 인식하려면 가장 단순한 방법으로 out 옵션으로 타입스크립트 파일을 컴파일하면 됨  
그런데 브라우저에서는 파일을 하나로 합치지 않고 타입스크립트 파일을 개별적으로 컴파일하고 import 문을 사용하지 않더라도 브라우저가 호출된 것처럼 인식함

## 8.3 모듈의 이해와 사용

타입스크리트는 ES2015 모듈의 선언과 호출과 관련한 스타일을 지원하는데 선언 방법이 다양함

### 8.3.1 모듈 선언과 모듈 임포트

타입스크립트 1.5부터 ES2015 모듈 시스템을 지원  
ES2015 모듈 시스템은 export나 import 제한자를 통해 모듈을 선언하고 호출할 수 있음  
모듈은 export로 선언해야 외부로 노출됨

```typescript
export interface Information { ... }
export function add(a: number, b: number) { ... }
```

위와 같이 **export 키워드와 모듈 이름을 함께 선언해 모듈을 노출**하는 방식을 명명된 내보내기라 함
외부로 노출된 모듈은 import 키워드를 이용해 가져올 수 있음

### 8.3.2 모듈을 개별적으로 노출하고 사용하기

함수나 인터페이스와 같은 단위별로 노출하려면 개별 노출 형식을 사용

### 8.3.3 여러 모듈을 함께 export하기

모듈로 선언할 수 있는 대상은 기본적으로 함수를 생각할 수 있지만, **변수나 배열 등도 모듈로 선언할 수 있음**  
모듈을 개별적으로 선언해도 되지만 모듈을 선언할 때마다 export 키워드를 붙이는 것은 불편함  
이러한 점을 개선하기 위해 **여러 모듈과 함께 export 해주면 편리함**

여러 변수를 외부로 export 하는 방법

```typescript
export { ver, author, extensions, display };
```

만약 모듈로 선언할 대상이 인터페이스를 사용하는 함수일 때는 함수가 인터페이스와 의존 관계가 있으므로 함수와 인터페이스를 함께 export 해야 함

export할 때 모듈의 이름을 변경하려면 as 키워드를 이용함

```typescript
export { IProfile, saveName as save };
```

### 8.3.4 모듈을 재노출해 사용하기

##### 가져온 모든 모듈을 재노출

만약 재노출할 모듈이 많아 구체적인 이름을 열거하기가 불편할 때는 **"export \* from ..." 문법을 이용**  
이 문법에서 \*은 모든 모듈을 의미합니다.

모듈 파일을 재노출할 때 모든 외부 모듈을 의미하는 \*에 대한 별칭이 없으므로 **임포트할 때는 as 키워드를 이용해 별칭을 추가해야 함**

##### 네임스페이스로 감싸서 재노출하기

네임스페이스는 **독립된 이름 공간**이며 export를 이용해 모듈로 선언할 수 있음

export로 선언하면 다른 파일에서 임포트할 수 있는 모듈이 됨  
네임스페이스는 이름 공간을 정의해 하위 여러 모듈을 포함할 수 있는 특성을 지님  
이 때문에 네임스페이스를 기존에 흩어졌던 모듈을 다시 용도에 맞게 감싸서 재노출할 용도로 사용할 수 있음

네임스페이스는 외부에 노출할 모듈을 모아 라이브러리 형태로 정의할 수 있음

### 8.3.5 디폴트 모듈의 이해와 사용법

##### export-equals 문과 import-equals 문

타입스크립트 1.5가 발표되기 전에는 모듈을 선언할 때 export-equals 문으로 할당했고, 모듈을 호출할 때는 import-equals 문으로 임포트했음

```typescript
export = validator;

import Validator = require("validator");
```

##### 디폴트 모듈 선언

타입스크립트 1.5에서는 import-equals 문과 export-equals 문 대신 다른 형태로 모듈을 선언하거나 임포트할 수 있음

```typescript
export default {
  title: "hello world",
  length: 11,
};
```

**default로 선언된 모듈을 파일마다 하나씩만 선언돼야 함**

import-equals 문은 require()를 쓰는 대신 ES6의 import 형식으로 가져올 수 있음

```typescript
import Validator from "./validator";
```

##### 디폴트 모듈과 명명된 모듈을 함께 가져오기

디폴트 모듈은 default 키워드를 사용해서 선언함  
디폴트 모듈의 특성은 파일에 최대 1개까지만 선언 가능함

```typescript
export { p as default, h as hello };

import default, { hello } from '...';
```

디폴트 모듈과 일반 모듈을 함께 임포트할 때는 **디폴트 모듈은 이름만 선언하고 일반 모듈은 {} 내부에 모듈 이름을 선언**해야 함

##### 디폴트 모듈로 타입과 모듈을 함께 노출

**디폴트 모듈로 export할 함수명과 인터페이스 타입명을 일치시켜 선언**

```typescript
interface HelloMessage {
  first: string;
  second: string;
}
function HelloMessage(name: string): HelloMessage {
  let message: HelloMessage = { first: "hello", second: name };
  return message;
}
export default HelloMessage;
```

위와 같이 export된 디폴트 모듈을 임포트하면 같은 이름을 이용해 함수 또는 인터페이스 타입으로 사용 가능

타입스크립트 컴파일러는 선언된 위치에 따라 함수로 사용되는 지 타입으로 사용되는 지 구분해 타입 검사를 수행함

## 8.4 모듈 시스템

### 8.4.1 모듈 로더와 모듈 형식

모듈 로더는 **모듈 파일에 선언된 모듈을 실행할 수 있음**  
브라우저에서 동작하는 모듈 로더는 느린 로딩의 방식으로 모듈 파일을 가져와 모듈을 실행

타입스크립트에서는 모듈을 정의하거나 호출할 때 ES2015 모듈을 이용  
타입스크립트는 자바스크립트로 컴파일돼 실행됨  
이때 ES2015 모듈이 표준이지만 더 많은 브라우저에서 지원하게 하고자 ES5 표준으로 컴파일하고 ES2015 모듈은 모듈로더를 통해 호출 가능

모듈 형식은 모듈 정의에 관한 표준 명세에 해당  
모듈 로더가 특정 모듈 형식을 지원하려면 모듈 로더가 지원하는 모듈 형식에 맞춰 컴파일해야 함

### 8.4.2 모듈 형식에 맞춰 컴파일하기

##### 모듈 형식에 따른 컴파일 방법

타입스크립트는 ES2015 모듈을 이용해 하위 표준으로 컴파일이 가능

프로젝트 기반이 아니라 특정 모듈 파일만을 컴파일하려면 명령어를 다음과 같은 형식으로 입력  
tsc --module <모듈 형식> <변환할 모듈 파일 이름>

--module 옵션에 사용할 수 있는 모듈 형식의 설정값

- none
- commonjs
- amd
- system
- umd
- es6 또는 es2015

설정값 중에 none은 ES2015 모듈 형식과 CommonJS 모듈 형식을 사용하지 않을 때 설정

만약 --module 옵션 사용 시 모듈 형식을 지정하지 않으면 target 값에 따라 다르게 기본값이 정해짐

##### --module 옵션에 대한 부가적인 설명

명령어로 모듈을 컴파일할 때 --out 옵션을 사용하면 입력 파일을 받아 단일 파일로 생성 가능  
tsc --out <출력할 js파일명> <변환할 ts 파일명> --module <모듈 형식>

--out 옵션과 --module 옵션을 사용할 때 허용하는 설정값은 amd, system 두 가지뿐  
--out 옵션은 단일 파일로 컴파일해 결과를 생성해 내는 옵션이므로 단일 파일에 적합하지 않은 나머지 모듈 형식은 허용 X

여러 파일에 걸쳐 모듈이 나뉘어 있는 대상을 컴파일할 때 사용하는 명령어
tsc <파일1이름>.ts <파일2이름>.ts -module amd | system

만약 소스 맵이 필요하다면 -sourcemap 옵션 추가  
tsc <파일이름>.ts <파일이름>.ts -sourcemap--out <파일이름>.js

### 8.4.3 특정 모듈 형식을 실행하기 위한 준비

##### 모듈 로더를 구동하기 위해 HTTP 서버 준비

##### 모듈 로더에서 사용할 a.ts 파일과 b.ts 파일 준비

## 8.5 각종 모듈 형식에 대한 소개

### 8.5.1 ES2015 모듈 형식

타입스크립트는 ES2015 모듈 형식을 기본으로 채택해 모듈을 선언하고 모듈을 호출함

SystemJS에서는 ES2015 모듈 형식을 지원하기 위해 traceur 컴파일러를 플러그인으로 이용

traceur는 브라우저에서 ES2015 모듈 형식(import/export)을 구동하기 위해 필요한 일종의 폴리필

### 8.5.2 CommonJS 모듈 형식

CommonJS는 Node.js에서 지원하는 모듈 형식이고 대부분의 모듈 로더에서 지원함  
CommonJS 모듈 형식은 타입스크립트에서 지원하는 ES2015 모듈 형식과 import와 export에 있어서 다음처럼 약간의 차이가 있음

|export/import|CommonJS 모듈 형식|es2015 모듈 형식|
|특정 모듈을 export|exports.message = "hello";|export var message = "hello";|
|모듈 전체를 export|module.exports = "hello";|export = "hello";|
|특정 모듈을 import|var add = require('calc').add;|import { add } from 'calc';|
|모듈 전체를 import|var foo = require('add');|import add as foo;|

export로 노출한 모듈을 require 함수를 이용해 호출 가능

export로 모듈을 노출해 주고 require 함수로 모듈을 호출해 주는 CommonJS 형식은 Node.js에서 기본적으로 지원되는 형식이므로 Node.js 개발 시 이용 가능  
but, \*.ts 파일로 옮겨오면 에러 발생  
require, exports 등을 인식할 수 있는 타입 정의 파일이 설치돼 있지 않기 때문

### 8.5.3 AMD 모듈 형식

AMD는 비동기 모듈 호출 방식으로 웹 사이트의 성능을 개선하기 위한 목적으로 출시  
웹 사이트에서 AMD 모듈을 호출하면 모듈 파일을 비동기로 가져와서 호출함  
비동기라는 말은 웹 사이트 구동 시에 모듈 파일을 모두 호출하지 않고 성능을 향상시킬 목적으로 모듈 파일을 사용할 시점에 가져와 사용한다는 의미

브라우저에서는 RequireJS, curl.js, PINF 등과 같은 모듈 로더를 통해 AMD 모듈을 코딩할 수 있고 서버에서는 RequireJS, PINF와 같은 모듈 로더를 통해 AMD 모듈을 호출할 수 있음  
AMD 모듈을 정의할 때 define() 함수를 이용

```javascript
define(id?, dependencies?, factory);
```

define 함수의 첫 번째 매개변수인 id는 모듈 아이디를 의미  
필수 값 x, 생략 가능, 생략하면 디폴트 id값을 이용  
두 번째 매개변수인 dependencies는 모듈 id의 배열을 의미하며 의존하고 있는 모듈의 id 목록을 배열로 전달해줌  
세 번째 매개변수인 factory는 익명 함수로 모듈의 구현 코드가 위치

작성한 타입스크립트 모듈 파일을 AMD 방식으로 컴파일하려면 tsc 명령어에 다음과 같은 옵션을 추가해야 함
--module amd

AMD 모듈은 node 명령어로 실행할 수 없고 AMD를 지원하는 SystemJS 모듈 로더를 이용해 구동할 수 있음

### 8.5.4 UMD 모듈 형식

UMD 모듈 형식은 클라이언트, 서버에서 보편적으로 작동하며, RequireJS 등의 모듈 로더에서 지원함  
UMD는 CommonJS 형식과 AMD 형식을 모두 고려하기에 범용으로 호환성을 갖춘 모듈을 정의할 수 있음  
단점: 모듈 코드양이 많아짐  
UMD 모듈 패턴은 익명 함수의 매개변수인 factory로 모듈을 정의한 익명 함수를 전달하는 형태로 정의

UMD 방식은 CommonJS + AMD + 기타 모듈을 합해 환경에 따라 다른 방식으로 모듈을 호출하므로 특정 모듈 형식을 지원하는 환경인지에 대한 검사가 포함됨

Node.js는 CommonJS 형식을 지원  
그리고 UMD 모듈 형식 내부에는 CommonJS 형식을 감지해 모듈 형식을 지정하므로 UMD 형식의 모듈은 node 명령어를 통해 결과 출력이 가능

### 8.5.5 SystemJS 모듈 형식

SystemJS 모듈 형식은 ES 모듈을 호출할 때 브라우저나 Node.js에서 비동기 형태로 ES 모듈을 호출하는 모듈 로더  
SystemJS 모듈 형식은 지원하는 모듈 로더가 SystemJS에 한정되기 때문에 호환성이 떨어짐

system 형식은 node 명령어로 실행할 수 없음
