Typescript 4.0 Handbook



#Uncalled function checks in conditional expressions

in Typescript 3.7 introduced uncalled function checks to report an error when you are forgotten to call a function

```ts 
//Uncalled check

function hasPermissions(): boolean {
 return true;
}

//Opp!

if (hasPermissions) {
	// this condition will always return true since the function is always defined.
	// Did you mean to call it instead?
}
```

However, this error only applied to conditions in if statements, this feature is also now supported in ternary conditionals (i.e: the cond ? trueExpr : falseExpr syntax)

```ts 
//Uncalled check

function hasPermissions(): boolean {
  return true;
}

const asText =  hasPermissions ? 'Yes, you Can': 'No, you can\'t';
```

#Enum
Typescript can catch silly bugs where we might be comparing values incorrectly

```ts
enum Greeting {
  HELLO,
  HI,
  HEY
}

function getText(greeting: Greeting) {
    if (greeting !== Greeting.HI || greeting !== Greeting.HEY ) {
      // Error! this condition will alway return 'true' since the types `Greeting.HI` and `Greeting.HEY` have no overlap.
      return 'Xin chao!'
    }
  return 'Ê!'
}
```

## Enum at runtime

```ts
enum Test {
    X, Y, Z
}

function f(obj: {X: number}) {
    return obj.X;
}

//it works, since 'Test' has a property named "X" with is a Number.
f(Test)
```

## Const Enums
In most cases. enum are a perfectly valid solution. However, sometimes requirements are tighter. To avoid paying the cost
of extra generated code and additional indirection when accessing enum values, it's possible to use const enums. Const enum
are defined using the const on our enums.
Const enums can only use constant enum expressions and unlike regular enums they are completely removed during compilation.
Const enum members are inlined at use sites. This is possible since const enums can not have computed members.
```ts
const enum Greeting {
  HELLO,
  HI,
  HEY
}

const greeting = [Greeting.HELLO, Greeting.HEY, Greeting.HI];
```
in generated code will become 

```javascript
var greeting = [0, 1, 2]
```

# Rest Parameters
Rest parameters (denoted by ...argumentName for the last arguments) allow you  to quickly accept multiple arguments in your
function and get them as an array. This is demonstrated in the below ex:

```ts
function takeAll(first, second, ...allOthers) {
    return allOthers;
}

takeAll(1, 2) //[]
takeAll(1, 2, 3, 4, 5) //[3, 4, 5]
```

## Destructuring with rest

### Objects
```ts
const {name, age, address} = {name: 'Anh', age: 'xx', city: 'Thu Duc', country: 'Vietname'}
console.log(name, age, address) // Anh, xx, {city: 'Thu Duc', country: 'Vietname'}
```

### Array
```ts
const [first, second, allOthers] = [1, 2, 3, 4, 5, 6];
console.log(first, second, allOthers) // 1, 2, [3, 4, 5, 6]
```

### Array Destructuring with ignores
```ts
const [first, , ...allOthers] = [1, 2, 3, 4, 5, 6];
console.log(first, allOthers) // 1, [3, 4, 5, 6]
```

# Singleton Pattern
The conventional singleton pattern is really something that all code must be in a class.

```ts
class Singleton {
  private static instance: Singleton;

  private constructor() {
  }
  
  static getInstance() {
      if (!Singleton.instance) {
          Singleton.instance = new Singleton();
      }
      return Singleton.instance;
  }
  public someMethod() {
      
  }
}

let something = new Selection(); // Error, constructor of Singleton is private
let instance = Singleton.getInstance(); // do something with the instance
```

#Currying

Just use a chain of fat arrow functions

```ts
// a curried functions
const add = (a: number) => (b: number) => a + b;

//signle usage
add(10)(20)

// pratially applied
const addWith10 = add(10);
//fully apply the function
addWith10(20)
```