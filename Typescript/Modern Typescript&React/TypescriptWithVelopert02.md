# Interface, Type Alias

---

### Interface

class 또는 객체의 type을 지정할때 사용하는 문법이다.

```tsx
// 접속(접점)
interface Shape {
  getArea(): number;
}
```

interface 안에서 getArea() 라는 함수가 있어야하며, 결과물은 number type이어야 한다고 정의했다.

아래 코드를 살펴보자.

```tsx
//Shape interface 안에 있는 것을을 만족하지 않는다면 밑줄이 그어진다!
class Circle implements Shape {}

// Shape을 만족하게끔 수정
// implements(구현,도구,시행하다)
// Circle 클래스는 Shape이라는 접점에 부합하다 라고 이해하자.
class Circle implements Shape {
  getArea() {
    return 5;
  }
}
```

### Circle class

```tsx
class Circle implements Shape {
  radius: number;

  constructor(radius: number) {
    this.radius = radius;
  }

  getArea() {
    return this.radius * this.radius * Math.PI;
  }
}
```

### Retangle class

```tsx
class Rectangle implements Shape {
  width: number;
  height: number;
  constructor(width: number, height: number) {
    this.width = width;
    this.height = height;
  }
  getArea() {
    return this.width * this.height;
  }
}
```

자세히 살펴보면 두개의 class에 getArea()라는 함수가 둘다 존재 하는데 이는 각각의 class가 Shape을 implements 하고있으며, getArea()의 반환값을 interface로 명시해놓았기 떄문이다.

### instance를 만들고 각각의 넓이를 구해보자 :)

```tsx
const circle = new Circle(5);
const rectangle = new Rectangle(2, 5);
const shapes: Shape[] = [circle, rectangle];

// 각각의 넓이가 계산되서 출력!
shapes.forEach((shape) => {
  console.log(shape.getArea());
});
```

### public & private

기존의 코드를 조금더 간소화 시켜보자!

```tsx
class Circle implements Shape {
  constructor(public radius: number) {}

  getArea() {
    return this.radius * this.radius * Math.PI;
  }
}

class Rectangle implements Shape {
  constructor(private width: number, private height: number) {}
  getArea() {
    return this.width * this.height;
  }
}
```

public으로 설정한다면, 전역 스코프에서 각각의 class에 값을 볼수있지만, private라고 설정한다면, 블록 스코프 안에서만 확인이 가능하다.! 하지만 컴파일시에는 딱히 의미가없다. 즉, public과 private는 typescript 내에서만 유의미 한 속성이라고 알고있자!

### interface를 이용해 객체의 type을 지정해보자

```tsx
interface Person {
  name: string;
  age?: number;
}
```

interface 의 propertyKey 부분에 ? 를 붙이게 되면 propertyKey가 있을수도 있고, 없을수도 있다라는 것을 의미하게된다.

### propertyKey? : 'optional';

만약 특정 객체를 만들게 될때 interface의 propertyKey값에 ?가 없다면 오류를 출력한다.

```tsx
interface Person {
  name: string;
  age: number;
}

const person: Person = {
  name: 'video',
  // age : '값을 넣어야 오류가 안나요!'
};
```

interface에서 지정하지 않은 property를 넣어도 오류가 발생한다!

```tsx
interface Person {
  name: string;
  age?: number;
}

const person: Person = {
  name: '김사람',
  age: 20,
  skills: ['javascript '], // 오류!
};
```

아래와 같이 새롭게 interface와 객체를 만들어보았다!

```tsx
interface Developer {
  name: string;
  age?: number;
  skills: string[];
}

const expert: Developer = {
  name: '김개발',
  skills: ['javascript', 'react', 'typescript'],
};
```

만들고보니 interface와 중첩되는 부분이 많다. 이것을 간소화 시키는 방법을 알아보자!

### extends interface

```tsx
interface Person {
  name: string;
  age?: number;
}

const person: Person = {
  name: '김사람',
  age: 20,
  skills: ['javascript '],
};

interface Developer extends Person {
  skills: string[]; // 중복되는 값을 extends Person 을통해 해결!
}

const expert: Developer = {
  name: '김개발',
  skills: ['javascript', 'react', 'typescript'],
};
```

extends를 이용해 interface의 중복되는 값을 줄일수있다!

### type Alias

interface 대신에 type을 통해서도 위와 비슷한 작업이 가능하다!

interface 는 type으로 그리고 `=` 을 붙여주자.

extends는 type명 & 로 변경!

```tsx
type Person = {
  name: string;
  age?: number;
};

const person: Person = {
  name: '김사람',
  age: 20,
  skills: ['javascript '],
};

type Developer = Person & {
  skills: string[]; // 중복되는 값을 extends Person 을통해 해결!
};

const expert: Developer = {
  name: '김개발',
  skills: ['javascript', 'react', 'typescript'],
};
```

### interface와 type Alias가 다른점

type **Alias**는 별칭이라고 불리운다. interface에서는 못하는 것을 type Alias로는 할수있다.

아래코드를 살펴보자 :)

```tsx
// People 라는 type을 설정하고 그 타입에는 Person 배열을 type으로 한다.
type People = Person[];
const people: People = [person, expert];

// Color 라는 type을 설정하고 그타입에는 'red' | 'orange' | 'yellow' 만을 사용할수 있다.
type Color = 'red' | 'orange' | 'yellow';
const color: Color = 'orange';
```

### interface를 사용해야 하나? type Alias를 사용해야 하나?

이것은 둘중 하나만 확실하게 결정해서 사용하도록하자! 통일서있게!
