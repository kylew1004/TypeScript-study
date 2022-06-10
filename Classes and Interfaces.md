# Class

1. public: 모든 클래스에서 접근 가능
2. private: 해당 클래스 내에서만 접근 가능 (자식 클래스에서도 접근 불가)
3. protected: 해당 클래스와 자식 클래스에서 접근 가능
4. 추상(abstract) 클래스
    - 추상 클래스는 오직 다른 클래스가 상속받을 수 있는 클래스이다.
    - 하지만 직접 새로운 인스턴스를 만들 수는 없다.

```
abstract class User{
    constructor(
        private firstname:string,
        private lastname:string,
        public nickname:string
    )
    {
        abstract getNickname():void
    }
}

// 추상 메서드는 추상 클래스를 상속받는 클래스들이 반드시 구현(implement)해야하는 메서드이다.

class Player extends User{  
    getNickname(){
        console.log(this.nickname)
    }
}
```
## ✨ 클래스를 만들때 클래스를 타입처럼 사용할 수 있다. ✨

```
type Words = {
    [key:string]: string
}

class Dict{
    private words: Words
    constructor(){
    this.words = {}
}
    add(word : Word){
        if (this.words[word.term] === undefined){
            this.words[word.term] = word.def;
        }
}
    def(term:string){
        return this.words[term]
    }
    delete(word : Word){
        if(this.words [word.term] !== undefined ){
            delete this.words[word.term];
    }
}
    update(term: string, newDef:string){
        if(this.words[term] !== undefined ){
            this.words[term] = newDef
        }
    }
}

class Word{
    constructor(
        public term:string,
        public def:string
    )
}
```

## static
- static 키워드를 클래스 프로퍼티에도 사용할 수 있다. 
- 정적 메소드와 마찬가지로 정적 클래스 프로퍼티는 인스턴스가 아닌 클래스 이름으로 호출하며 클래스의 인스턴스를 생성하지 않아도 호출할 수 있다.

```
class Foo {
  // 생성된 인스턴스의 갯수
  static instanceCounter = 0;
  constructor() {
    // 생성자가 호출될 때마다 카운터를 1씩 증가시킨다.
    Foo.instanceCounter++;
  }
}

var foo1 = new Foo();
var foo2 = new Foo();

console.log(Foo.instanceCounter);  // 2
console.log(foo2.instanceCounter); // error TS2339: Property 'instanceCounter' does not exist on type 'Foo'.
```

# Interfaces & type

- type 과 interface는 오브젝트의 모양을 결정한다는 점은 같습니다.
- type이 interface보다 할 수 있는 것들이 더 많습니다. (ex: interface Hello = string (안됨))
- interface는 오직 오브젝트의 모양만을 설명하기 위한 키워드
- interface를 상속받으면 property들을 private 나 protected 로 사용불가, only public
```
type Team = "red" | "blue" | "green"
type Health = 1 | 5 | 10

interface Player = {
    nickname: string,
    team: Team,
    health: Health
}

const gangyub : Player = {
    nickname: "gangyub",
    team: "yellow",
    health: 10
}
```

``` 
type User = {
    name: string
}
type Player = User & {

}

const gangyub : Player = {
    name : "gangyub"
}
```
```
interface User {
    name: string
}
interface Player extends User {

}
const gangyub : Player = {
    name : "gangyub"
}
```

## implements

- implements을 사용하여 클래스가 특정 인터페이스를 충족하는지 확인할 수 있습니다.
- 클래스를 올바르게 구현하지 못하면 오류가 발생합니다.
- implements 절은 클래스가 인터페이스 유형으로 처리될 수 있는지 확인하는 것입니다. 클래스의 유형이나 메서드는 전혀 변경하지 않습니다.
- 추상클래스를 쓰면 자바스크립트에서는 일반적인 클래스가 만들어지고 파일의 크기가 더 커지고 추가클래스가 만들어집니다. 만약 클래스가 특정모양을 따르기 위한 용도로 쓴다면 같은 역할을 하는 interface를 쓰는 것이 더 좋습니다.
    - class Player extend User 보다 class Player implements User 로 써야 합니다. interface는 JS에서 보이지 않습니다.

```
interface Pingable {
    ping(): void;
}

// Sonar클래스는 Pingable인터페이스를 implement했기 때문에 Pingable가 가진 ping메서드를 구현해줘야 합니다.
class Sonar implements Pingable {
    ping() {
        console.log("ping!");
    }
}
```
