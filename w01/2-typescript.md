# TypeScript

## Type Alias 와 Interface

* 둘 다 객체를 지정해줄 수 있다.
* 확장하는 부분에서 차이를 보인다.

  ```ts
    // interface
    interface IPerson {
        name: string
        age: number
    }

    interface IStudent extends IPerson {
        school: string
    }

    // type alias
    type Person = {
        name: string
        age: number
    }

    type Student = Person & {
        school: string
    }
  ```

  * type 은 interface 의 기능을 거의 사용할 수 있지만, 선언적으로 확장은 불가능하다.

  ```ts
    interface IPerson {
        name: string
    }

    interface IPerson {
        age: number
    }

    // IPerson 는 name 과 age 멤버를 가지는 타입이 된다.

    type Person = {
        name: string
    }

    // Error, type alias 는 확장이 불가능하다.
    type Person = {
        age: number
    }
  ```

* emotion.d.ts 에서 Theme 타입을 제공해줄때 interface 를 사용해야 선언병합되어 props.theme 타입 추론이 가능하다.

* 팀 컨벤션에 따라 interface 를 쓸지. type alias 을 쓸지 정하면 된다. 현재 우리팀은 type alias 를 주로 사용한다. 이유는 타입 정보를 더 잘 표현해주기 때문.

## 타입을 집합의 관점으로 바라보기

* 타입은 값의 집합이다.
* 집합에 속하지않는 값은 할당되지 못한다. (보통 값으로 타입을 추론되게 하는 것이 좋다. as 는 피한다.)
* &(인터섹션) 는 교집합. |(유니온) 는 합집합으로 생각하기.
  * A & B 는 A 타입이 되어도, B 타입이 되어도 무방한 타입이어야한다. (교집합)

  ```ts
    interface IPerson1 {
        name: string
    }

    interface IPerson2 {
        age: number
    }

    type IPerson = IPerson1 & IPerson2; // name 과 age 멤버를 가지는 타입이 된다.

    type A = 'a';
    type B = 'b';

    type C = A & B; // never, 'a' 가 되거나 'b' 가 되는 타입은 없다.
  ```

  * A | B 는 A 에 속하거나 B 에 속하는 타입이다. (합집합)

  ```ts
    interface IPerson1 {
        name: string
    }

    interface IPerson2 {
        age: number
    }

    type IPerson = IPerson | IPerson2; // { name: string } 이거나 { age: number } 여야한다.

    type A = 'a';
    type B = 'b';

    type C = A | B; // 'a' | 'b' 가 된다. 'a' 거나 'b' 인 타입. 유니온은 하나의 집합을 선정한다.

    type IPersonKey = keyof IPerson; // never, IPerson1 이 되거나 IPerson2 가 되는 속성은 없다. (겹치는 속성이 없다.)
  ```

  * `keyof (A & B) = (keyof A) | (keyof B)`
  * `keyof (A | B) = (keyof A) & (keyof B)`

## Null 과 Undefined 를 구분하기

* Null 은 의도적으로 값을 비울때.
* Undefined 는 의도치않게 값이 없을때

Reference

* <https://yceffort.kr/2021/03/typescript-interface-vs-type>
* <https://fe-developers.kakaoent.com/2022/221124-typescript-tip/>
* <https://blog.hwahae.co.kr/all/tech/9954>
