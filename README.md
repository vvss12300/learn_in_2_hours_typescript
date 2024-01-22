# Under 30 minutes: Typescript (TS) #

- Official Website: [https://www.typescriptlang.org/](https://www.typescriptlang.org/)

- Introduction
	- Typescript is a Typed Superset of JavaScript
	- It adds Static Typing to javascript
	- After code implementation, TS is converted back to JS by tsc(TypeScript Compiler)
	- File extension for typescript should be .ts or .tsx
	- A project can have both JS and TS files as TS files will convert to JS after compilation
	- A TS config file can be added to a project to configure TS settings for the project
	- It is recommended for new projects use TS from the start but existing JS-based projects can be migrated in phase to TS

- Points we will cover:
	- Primitive Types: number, string, boolean
	- Complex Types: Arrays and Objects
	- Union Types
	- Functions and parameters

- Primitive Types
	- Add a colon(:) after variable name and assign a type
	- Types are in lowercase
	- If a different type of value is assigned to the variable like string is assigned to a number variable then Typescript compiler will give an error while compiling, however depending on your TS Config, an output JS file will be created.

```javascript
// Primitive Types
let name: string = 'John Doe';
let age: number = 25;
let isGraduate: boolean = true;
```

- Arrays
	- If you define an array in JS, it allows values of multiple types to be stored like
		- let smapleArray = ['One', 2, true];
	- In TS, we need to specify the type of array, and then only the value of that type can be stored.

```javascript
// Arrays
let allJobs: string[] = ['Facebook', 'Microsoft', 'Google'];
let salaries: number[] = [12000000, 14000000, 16000000];
```

- Objects
	- An object is a combination of multiple Primitive types with multiple levels of nesting.
	- With static typing in object with basically means to specify the structure of the object.

```javascript
// Object in JS doesn't have a fixed structure
let person = {
	name: 'John Doe',
	age: 25
}

//Here we are altering the structure of the object and JS doesn't have any issue with it
person = {
	isGraduate: false
}
```

```javascript
//Objects in TS have a well-defined structure called as object type description
// Here we are telling TS that a person object has 2 properties name of string and age of type number 
let person : {
	name: string;
	age: number;
};

// Allowed because it matches the object type description
person = {
	name: 'John Doe',
	age: 25
};

// Not allowed as isGraduate is not defined in the object type description
person = {
	isGraduate: false
};

//Array of objects
let employees : {
	name: string;
	age: number;
}[];

employees = [ { name: 'John Doe', age: 25},
			  { name: 'David Ga', age: 40} ];
```

- Union Types
	- If we need to assign more than one type to a variable then we use the feature union type
```javascript
// Here we are saying that sampleVariable can be a string or number
let sampleVariable: string | number = 'John Doe';
sampleVariable = 10;
```

- Special Type **any**
	- If a variable is defined with type **any** in the TS, it means any value can be stored in it
	- It is highly discouraged to use any if the type is known.


```javascript
function logError(errorObject : any){
	console.log(errorObject);
}
```

- Type Alias
	- Create a custom type that is common in the application
	- Use the TS **type** keyword to define a custom type
	- Best practice to use Pascal casing for types
	- A common practice is to create a folder as **types** in the project and have all common types used across application as separate files or single files in this folder

```javascript
// Create a custom type person
type Person{
	name: string,
	age: number
}

//Declare variable of type Person
let employee: Person;

//Declare array of type Person
let employess: Person[];
```


- Interfaces
	- An interface declaration is another way to name an object type
	- Type Alias and interfaces are very similar, and in many cases, you can choose between them freely. Almost all features of an interface are available in type, the key distinction is that a type cannot be extended to add new properties vs an interface is always extendable.	

```javascript
// Create an interface person
interface  Person{
	name: string,
	age: number
}

//Declare variable of type Person
let employee: Person;
```

```javascript
//Extending an interface
interface Animal {
  name: string;
}

interface Bear extends Animal {
  honey: boolean;
}

const bear = getBear();
bear.name;
bear.honey;
```


- Function types
	- Types can be defined for Function parameters and return values.
	- Optional Parameters can be defined with '?' keyword

```javascript
function getSalary(salaryPerDay: number, noOfWorkingDays: number) : number {
	return salaryPerDay * noOfWorkingDays;
}


// Another complex example
type Person{
	name: string,
	age: number
}

function convertToPerson(name: string, age: number) : Person {
	return {
		name,
		age
	};
}

// Arrow Function
const convertToPerson = (name: string, age: number): Person => ({
   name,
	age
});

//Functions Which Return Promises
async function convertToPerson(name: string, age: number) : Promise<Person> {
	return {
		name,
		age
	};
}

//Function with optional parameter
function sum(firstNumber: number, secondNumber: number,  thridOptionalNumber?: number): number {
  if (typeof thridOptionalNumber !== "undefined") {
    return firstNumber + secondNumber + thridOptionalNumber;
  }
  return firstNumber + secondNumber;
}
```

- Type Inference
	- If the variable is declared and initialized at the same time, the type doesn't need to be defined as TS will infer the best possible type based on the initialization
```javascript
// In the below expample TS will infer that name variable will be string based on the assigned value. So, we don't need to explicitly add ": string" in the declaration
let name = 'John Doe';
```

- Type Assertions
	- Sometimes you will have information about the type of a value then that TypeScript infers.
	- For example, if you’re using document.getElementById, TypeScript only knows that this will return some kind of HTMLElement, but you might know that your page will always have an HTMLCanvasElement with a given ID.
	- TypeScript only allows type assertions that convert to a more specific or less specific version of a type. 	

```javascript
// You can use a type assertion to specify a more specific type
const myCanvas = document.getElementById("main_canvas") as HTMLCanvasElement;

//or
const myCanvas = <HTMLCanvasElement>document.getElementById("main_canvas");
```

- Type null and undefined
	- null and undefined are also 2 types of TS
	- any variable as per take a value null or undefined if it's defined with these types
	- Postfix !: TypeScript also has a special syntax for removing null and undefined from a type without doing any explicit checking.

```javascript
function doSomething(x: string | null) {
  if (x === null) {
    // do nothing
  } else {
    console.log("Hello, " + x.toUpperCase());
  }
}


//Writing ! after any expression is effectively a type assertion that the value isn’t null or undefined:
function liveDangerously(x?: number | null) {
  // No error
  console.log(x!.toFixed());
}
```


- Generics
	- If an operation supports a variety of data types rather than a single data type, generics is a way.
	- It can used in functions, types, or interfaces
	- Generics use a special kind of type variable **<T>** that denotes types.

```javascript
//Here T can be any data type. Exact type is passed during function call
function getItems<T>(items : T[] ) : T[] {  
    return new Array<T>().concat(items);  
}

// Here T is getting passed as a number
let arrNumber = getItems<number>([10, 20, 30]);

// Here T is getting passed as a string
let arrString = getItems<string>(["Hello", "JavaTpoint"]);

//Here T can be either a number or a string
let arrHybrid = getItems<number | string>([10, "Hello"]);


//Generics in object
interface Box<Type> {
  contents: Type;
}

// during  initialization of object we provide the exact type to be realized
let boxofStrings: Box<string> = { contents: "hello" };
let boxofNumbers: Box<number> = { contents: "123" };
```

- Classes
	- TypeScript offers full support for the class keyword introduced in ES2015.
	- Classes contain properties and methods
	- While using typescript, define the type of each property and method
	- A Class can extend from another class
	- TypeScript can be used to control whether certain methods or properties are visible to code outside the class.
		- Public: The default visibility of class members is public. A public member can be accessed anywhere
		- Protected: Protected members are only visible to derived of the class they’re declared in.
		- Private: Only visible within the same class


```javascript
class Point {
  x = 10;
  y = 10;
 
  scale(n: number): void {
    this.x *= n;
    this.y *= n;
  }
}
```

```javascript
 //A derived class has all the properties and methods of its base class, and can also define additional members.
class Animal {
  move(steps: number) {
    console.log("Moving steps:" + steps);
  }
}
 
class Dog extends Animal {
  woof(times: number) {
    for (let i = 0; i < times; i++) {
      console.log("woof!");
    }
  }
}
 
const dogObject = new Dog();
// Base class method
dogObject.move(2);
// Derived class method
dogObject.woof(3);
```

```javascript
//Public: The default visibility of class members is public. A public member can be accessed anywhere
//Protected: Protected members are only visible to derived of the class they’re declared in.
//Private: Only visible within the same class
class Greeter {
  private helloText: string = "Hello, ";
  public greet(name: string) {
    console.log("Hello, " + name);
  }

  protected getName() {
    return "hi";
  }
}
```

- There are a lot of other utility types which you can find [here](https://www.typescriptlang.org/docs/handbook/utility-types.html)

Creating your first TypeScript App
- Create a folder and start a new node app
```console
npm init 
```
- Install TypeScript
```console
npm install typescript
```

- Install TypeScript
```console
npm install -g typescript
```

- Create a file person.ts and below content
```Javascript
interface Person {
    firstName: string;
    lastName: string;
  }
   
function greeter(person: Person) {
    return "Hello, " + person.firstName + " " + person.lastName;
}
 
let samplePerson: Person = { firstName: "John", lastName: "Doe" };
console.log(greeter(samplePerson));
```

- Compile TypeScript
```console
tsc person.ts
```

- Output Javascript file
```Javascript
function greeter(person) {
	return "Hello, " + person.firstName + " " + person.lastName;
}
var samplePerson = { firstName: "John", lastName: "Doe" };
console.log(greeter(samplePerson));
```
