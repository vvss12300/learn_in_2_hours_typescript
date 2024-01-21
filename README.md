# Typescript (TS): To the Point #

- Official Website: [https://www.typescriptlang.org/](https://www.typescriptlang.org/)

- Introduction
	- Typescript is a Typed Superset of JavaScript
	- It adds Static Typing to javascript
	- After code implementation, TS is converted back to JS by tsc(TypeScript Compiler)
	- File extension for typescript should be .ts or .tsx
	- A project can have both JS and TS files as TS files will convert to JS after compilation
	- A TS config file can be added to a project to configure TS settings for the project
	- Its recommended for new projects to use TS from the start but existing JS based projects can be migrated in phase to TS

- Points we will cover:
	- Primitive Types: number, string, boolean
	- Complex Types: Arrays and Objects
	- Union Types
	- Functions and parameters

- Primitive Types
	- Add a colon(:) after variable name and assign a type
	- Types are in lowercase
	- If a different type of value is assigned to the variable like string is assigned to a number variable then Typescript compiler will give error while compiling, however depending on your TS Config, output JS file will be created.

```javascript
// Primitive Types
let name: string = 'John Doe';
let age: number = 25;
let isGraduate: boolean = true;
```

- Arrays
	- If you define an array in JS, it allows values of multiple types to be stored like
		- let smapleArray = ['One', 2, true];
	- In TS, we need to specify the type of array, then only value of that type can be stored.

```javascript
// Arrays
let allJobs: string[] = ['Facebook', 'Microsoft', 'Google'];
let salaries: number[] = [12000000, 14000000, 16000000];
```

- Objects
	- An object is a combination of multiple Primitive types with multiple level of nesting.
	- With static typing in object with basically mean to specify the structure of the object.

```javascript
// Object in JS doesn't have fixed structure
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
// Object in TS have a well defined structure called as object type desciption
// Here we are telling TS that person object have 2 properties name of string and age of type number 
let person : {
	name: string;
	age: number;
};

// Allowed because it matches the object type desciption
person = {
	name: 'John Doe',
	age: 25
};

// Not allowed as isGraduate is not defined in the object type desciption
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
	- If we need to assign more than one type to variable then we use the feature union type
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
	- Create a custom type that are common in the application
	- Use the TS **type** keyword to define a custom type
	- Best practice to use Pascal casing for types
	- A common practice is to create a folder as **types** in the project and have all common types used accoss application as seperate files or single file in this folder

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
	- Type Alias and interfaces are very similar, and in many cases you can choose between them freely. Almost all features of an interface are available in type, the key distinction is that a type cannot be extended to add new properties vs an interface which is always extendable.	

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
	- Types can be defined for Function parameters and return value.

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
```

- Type Inference
	- If the variable is declared and initialized at the same time, type doesn't need to be defined as TS will infer the best possible type based on the initialization
```javascript
// In the below expample TS will infer that name variable will be string based on the assigned value. So, we don't need to explicitly add ": string" in the declaration
let name = 'John Doe';
```

- Type Assertions
	- Sometimes you will have information about the type of a value then that TypeScript infer.
	- For example, if you’re using document.getElementById, TypeScript only knows that this will return some kind of HTMLElement, but you might know that your page will always have an HTMLCanvasElement with a given ID.
	- TypeScript only allows type assertions which convert to a more specific or less specific version of a type. 	

```javascript
// You can use a type assertion to specify a more specific type
const myCanvas = document.getElementById("main_canvas") as HTMLCanvasElement;

//or
const myCanvas = <HTMLCanvasElement>document.getElementById("main_canvas");
```

- Type null and undefined
	- null and undefined are also 2 types in TS
	- any variable as per take a value null or undefined if its defined with these types
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



 
