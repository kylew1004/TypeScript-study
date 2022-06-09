# Call Signature (호출 시그니처)

- 함수의 타입을 지정할 때 사용하는 문법
- 함수의 매개변수와 반환 값의 타입을 모두 type으로 미리 선언하는 것
- React에서 함수로 props를 보낼 때, 어떻게 작동할지 미리 설계 가능

```
type Add = (a:number, b:number) => number;

const add:Add = (a, b) => a, b;
```

# Overloading (오버로딩)

- 동일한 이름에 매개 변수와 매개 변수 타입 또는 리턴 타입이 다른 여러 버전의 함수를 만드는 것을 말합니다.
- "다양한 방식으로 호출할 수 있는 함수"를 지정할 수 있습니다.

```
type Add={
(a:number,b:number):number;
(a:number,b:number,c:number):number;
}

const add:Add=(a,b,c?:number)=>{
    if(c) return a+b+c
return a+b;
}
```

# Generic and Polymorphism (다형성) 

- 다형성이란, 여러 타입을 받아들임으로써 여러 형태를 가지는 것을 의미합니다.
- Generic을 활용해서 임의로 타입을 입력받습니다. <>를 입력하면 Generic이라는 뜻입니다.

```
type SuperPrint = {
    <GenericName>(arr:GenericName[]): void
}
const superPrint : SuperPrint = (arr) => {
    arr.forEach(i => console.log(i));
}

superPrint([1,2,3,4])
superPrint([true,false,true])
superPrint(["a","b","c"])
superPrint([1,2,true,false])
```
```
type SuperPrint = <T>(a: T[]) => T

const superPrint: SuperPrint = (a) => a[0]

superPrint([1,2,3,4])
superPrint([true,false,true])
superPrint(["a","b","c"])
superPrint([1,2,true,false])
```
