# 자바스크립트 쓰면 안되는 이유
1. [1,2,3,4,5] + False 를 입력하면
'1,2,3,4,5False'가 나온다. 오류가 있어도 어떻게든 출력하려 애쓴다.

2. 함수를 실행할 때 올바른 argument(입력값)를 사용하도록 강제하지 않는다.

3. 객체 안에 존재하지 않는 함수를 호출할 수 도 있다. ->런타임에러

# 타입스크립트?
- strongly typed programming language(강타입 언어)

1. TypeScript는 JavaScript에 추가적인 구문을 추가하여 editor와의 단단한 통합을 지원합니다. editor에서 초기에 오류를 잡을 수 있습니다.

2. TypeScript 코드는 JavaScript가 실행되는 모든 곳(브라우저, Node.js 또는 Deno 및 앱 등)에서 JavaScript로 변환될 수 있습니다.

3. TypeScript는 JavaScript를 이해하고 타입 추론(type inference)을 사용하여 추가 코드 없이도 훌륭한 도구를 제공합니다.

# 타입스크립트는 타입을 추론한다.

```
let a = "hello"
a = "bye"
a = 1			// let a: string

let b : boolean=false		// 변수 타입 지정하는 법

let c = [1, 2, 3]
c.push("1")		// 에러

// 밑에 코드처럼 작성할 필요는 없음
let a : number[] = [1, 2];
let b : string[] ["1","2"];
let c : boolean[] = [true];
```

# Object
- TypeScript에서 JavaScript의 Object처럼 사용하고 싶은 경우에는 {}를 사용합니다.
- JS와는 달리 지정한 타입 외에는 사용할 수 없다는 것을 주의해서 사용해야 합니다.
```
const player : {
	name: string,
	age?: number	//age가 없으면 undefined
} = {
	name: "GangYub"
}

if(player.age && player.age < 10){

}
```

# Alias

- Type Aliases을 사용하여 객체 타입뿐만 아니라 모든 타입에 이름을 지정할 수 있습니다.
```
type Player = {     // 첫문자는 대문자!
	name: string,
	age?: number
}
const lew : Player = {
	name: "Lew"
}
const gang : Player = {
	name: "GangYub",
	age: "12"
}

function playerMaker(name: string) : Player {	//Player로 return 타입지정
	return {
		name
	}
}

const lew = playerMaker("Lew")
lew.age = 12

const playerMake = (name: string) : Player => ({name})	// name이 있는 Player 객체를 return
```

# readonly

- JavaScript에서는 mutability(변경 가능성)이 기본값이지만 타입스크립트에서는 readonly를 통해 읽기 전용으로 만들 수 있습니다.

```
type Player = {
	readonly name: string,
	age?: number
}
const playerMaker = (name:string) : Player => ({name})
const lew = playerMaker("Lew")
lew.age = 12
lew.name = "gang"	// 에러
```

# array

- 배열 타입은 자바스크립트 Array 값의 타입을 나타내는데 쓰인다. 원소 타입 뒤에 대괄호([])를 붙입니다.

```
const pibonacci: number[] = [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55];
const myFavoriteBeers: string[] = ['Imperial Stout', 'India Pale Ale', 'Weizenbock'];
```

```
const pibonacci: Array<number> = [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55];
const myFavoriteBeers: Array<string> = ['Imperial Stout', 'India Pale Ale', 'Weizenbock'];
```
# Tuple

- 튜플 타입 변수는 정확히 명시된 개수 만큼의 원소만을 가질 수 있습니다.
- 만약 타입 정의보다 더 많은, 혹은 더 적은 원소를 갖는 배열을 할당한다면 에러가 발생합니다.

```
const player: [string, number, boolean] = ["lew", 1, true]
```

# any

- any는 Typescript로 부터 빠져나오고 싶을 때 쓰는 타입
- any를 사용하면 Typescript의 보호를 받지 못하고 Javascript로 인식되기 때문에 자주 안쓰는 것을 권장

# unknown

- API로부터 응답을 받는데 그 응답의 타입을 모를 때 씁니다.
```
let a: unknown;

if(typeof a === 'number'){
    let b = a + 1;
}
```

# void

- void는 값을 반환하지 않는 함수의 반환 값을 나타냅니다.
- 함수에 return 문이 없거나 해당 return 문에서 명시적 값을 반환하지 않을 때 항상 유추되는 타입입니다.
```
function hello(){
    console.log('x');
}
```

# never

- 함수가 절대 return 하지 않을 때 발생
- 절대 발생할 수 없는 타입
```
function hello(name: string|number){
    if(typeof name === "string"){
        // name 타입은 string
    } else if(type of name === "number"){
        // name 타입은 number
    } else {
        // name 타입은 never
    }
}
```