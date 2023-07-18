# TypeScript Cheat Sheet

TypeScript is a statically-typed language developed by Microsoft. It compiles to plain JavaScript and supports all ECMAScript features. To get started with TypeScript, install it via npm:

## 1. Setting up, compiling, development, ts-node

```bash
npm install -g typescript
```

Compile a TypeScript file with:

```bash
tsc filename.ts
```

`ts-node` allows running TypeScript files directly without compiling:

```bash
npm install ts-node --save-dev
```

Run TypeScript files directly:

```bash
ts-node filename.ts
```

## 2. Basic Types

TypeScript includes several basic types:

```typescript
let isDone: boolean = false;
let count: number = 42;
let name: string = "TypeScript";
let list: number[] = [1, 2, 3];
let tuple: [string, number] = ["hello", 42];
let anyValue: any = 5; // Avoid using 'any' when possible
let unknownValue: unknown; // Similar to 'any', but type-safe
```

## 3. Variable Declarations

TypeScript supports the same variable declarations as JavaScript:

```typescript
let x = 10; // number
const pi = 3.14; // const
```

## 4. Functions

Functions can have parameter types and return types:

```typescript
function add(a: number, b: number): number {
  return a + b;
}

// Optional and default parameters
function greet(name: string, greeting?: string): string {
  return greeting ? `${greeting}, ${name}!` : `Hello, ${name}!`;
}
```

## 5. Interfaces

Interfaces define object structures:

```typescript
interface Person {
  name: string;
  age: number;
}

function printPerson(person: Person): void {
  console.log(`Name: ${person.name}, Age: ${person.age}`);
}
```

## 6. Classes

TypeScript supports classes with constructor and inheritance:

```typescript
class Animal {
  constructor(public name: string) {}

  makeSound() {
    console.log("Some generic sound");
  }
}

class Dog extends Animal {
  makeSound() {
    console.log("Woof!");
  }
}
```

## 7. Type Inference

TypeScript can infer types based on context:

```typescript
let message = "TypeScript"; // Type inferred as string
let numbers = [1, 2, 3]; // Type inferred as number[]
```

## 8. Generics

Generics allow flexible, reusable functions and classes:

```typescript
function identity<T>(arg: T): T {
  return arg;
}

class Box<T> {
  constructor(private value: T) {}

  getValue(): T {
    return this.value;
  }
}
```

## 9. Enums

Enums allow defining named constants:

```typescript
enum Color {
  Red,
  Green,
  Blue,
}

let myColor: Color = Color.Green;
```

## 10. Advanced Types

TypeScript offers advanced types like union, intersection, and mapped types:

```typescript
type StringOrNumber = string | number;

interface Person {
  name: string;
  age: number;
}

type PersonKeys = keyof Person; // "name" | "age"
```

## 11. Type Assertion

Type assertions enable you to override TypeScript's inference:

```typescript
let message: unknown = "Hello, TypeScript!";
let strLength: number = (message as string).length;
```

## 12. Type Guards

Type guards help narrow down types within conditional blocks:

```typescript
function doSomething(value: string | number) {
  if (typeof value === "string") {
    console.log("It's a string!");
  } else {
    console.log("It's a number!");
  }
}
```

## 13. Modules

TypeScript supports ECMAScript modules:

```typescript
// math.ts
export function add(a: number, b: number): number {
  return a + b;
}

// app.ts
import { add } from "./math";
console.log(add(2, 3)); // Output: 5
```

## 14. Decorators

TypeScript supports decorators, which are used to modify classes, methods, or properties:

```typescript
function log(target: any, key: string) {
  console.log(`Logged: ${key}`);
}

class MyClass {
  @log
  myMethod() {
    // Method logic here
  }
}
```

## 15. Type Aliases

Type aliases provide a way to create custom names for types:

```typescript
type Point = { x: number; y: number };

function distance(p1: Point, p2: Point): number {
  const dx = p1.x - p2.x;
  const dy = p1.y - p2.y;
  return Math.sqrt(dx * dx + dy * dy);
}
```

## 16. String Literal Types

String literal types allow you to define a set of possible string values:

```typescript
type Direction = "up" | "down" | "left" | "right";

function move(direction: Direction): void {
  // Move logic here
}
```

## 17. Non-Null Assertion Operator

The non-null assertion operator (`!`) tells TypeScript to consider a value as non-null, even if it's not specified in the type:

```typescript
let name: string | null = getNameFromExternalSource();
let length: number = name!.length; // Asserting 'name' is not null
```

## 18. keyof and Lookup Types

The `keyof` operator and lookup types allow you to work with object keys more dynamically:

```typescript
interface Person {
  name: string;
  age: number;
}

type PersonKeys = keyof Person; // "name" | "age"

function getProperty(obj: Person, key: PersonKeys): string {
  return obj[key]; // Compiler knows this will be a string
}
```

## 19. Tuples

Tuples are arrays with fixed-length and typed elements:

```typescript
let coordinates: [number, number] = [10, 20];
let pair: [string, number] = ["answer", 42];
```

## 20. Namespaces

Namespaces help organize code and prevent naming collisions:

```typescript
namespace MyNamespace {
  export const PI = 3.14;

  export function calculateCircumference(diameter: number): number {
    return diameter * PI;
  }
}

const diameter = 10;
console.log(`Circumference: ${MyNamespace.calculateCircumference(diameter)}`);
```

## 21. Triple-Slash Directives

Triple-slash directives provide additional information to the TypeScript compiler:

```typescript
/// <reference path="path/to/another-file.ts" />

namespace AnotherNamespace {
  // Namespace content
}
```

## 22. Asynchronous Programming with Async/Await

TypeScript seamlessly integrates with modern asynchronous programming using `async` and `await`:

```typescript
async function fetchData(url: string): Promise<string> {
  const response = await fetch(url);
  const data = await response.text();
  return data;
}
```

## 23. Intersection Types

Intersection types allow combining multiple types into one:

```typescript
interface User {
  id: number;
  name: string;
}

interface Admin {
  isAdmin: boolean;
}

type AdminUser = User & Admin;
```

## 24. Type Predicates

Type predicates

 allow you to define custom type guards:

```typescript
function isString(value: unknown): value is string {
  return typeof value === "string";
}

function processValue(value: unknown) {
  if (isString(value)) {
    console.log(value.toUpperCase());
  } else {
    console.log("Value is not a string.");
  }
}
```

## 25. Mixins

Mixins enable composition of classes from reusable components:

```typescript
class Timestamped {
  timestamp = new Date();
}

class Person {
  constructor(public name: string) {}
}

type TimestampedPerson = Person & Timestamped;
```

## 26. Abstract Classes

Abstract classes provide a blueprint for other classes to inherit from:

```typescript
abstract class Shape {
  abstract area(): number;
}

class Circle extends Shape {
  constructor(private radius: number) {
    super();
  }

  area(): number {
    return Math.PI * this.radius ** 2;
  }
}
```

## 27. Strict Null Checks

TypeScript's strict null checks (`strictNullChecks`) help avoid null and undefined errors:

```typescript
function divide(a: number, b: number): number {
  if (b !== 0) {
    return a / b;
  } else {
    throw new Error("Cannot divide by zero.");
  }
}
```

## 28. Configuring tsconfig.json

The `tsconfig.json` file allows configuring TypeScript compilation options:

```json
{
  "compilerOptions": {
    "target": "esnext",
    "module": "commonjs",
    "strict": true,
    "outDir": "dist"
  },
  "include": ["src/**/*.ts"],
  "exclude": ["node_modules"]
}
```

## 29. Using ESLint with TypeScript

ESLint can be integrated with TypeScript to enforce code quality:

```bash
npm install eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin --save-dev
```

Create an `.eslintrc.js` file:

```javascript
module.exports = {
  parser: "@typescript-eslint/parser",
  plugins: ["@typescript-eslint"],
  extends: ["eslint:recommended", "plugin:@typescript-eslint/recommended"],
  rules: {
    // Your custom rules here
  },
};
```

## 30. Type Guards and Discriminated Unions

TypeScript's discriminated unions and type guards make handling different types in conditional blocks more intuitive:

```typescript
interface Square {
  kind: "square";
  size: number;
}

interface Circle {
  kind: "circle";
  radius: number;
}

type Shape = Square | Circle;

function area(shape: Shape): number {
  switch (shape.kind) {
    case "square":
      return shape.size ** 2;
    case "circle":
      return Math.PI * shape.radius ** 2;
    default:
      throw new Error("Unknown shape!");
  }
}
```

## 31. Type-Only Imports/Exports

TypeScript allows using type-only imports and exports to improve compilation performance:

```typescript
// types.ts
export type Point = { x: number; y: number };
export type Vector = { dx: number; dy: number };

// main.ts
import type { Point } from "./types";
const p: Point = { x: 0, y: 0 };
```

## 32. Configuring Type Inference

TypeScript provides options to customize type inference for better control:

```typescript
// In tsconfig.json
{
  "compilerOptions": {
    "strictNullChecks": true,
    "noImplicitAny": true,
    "strictPropertyInitialization": false
  }
}
```

## 33. Using Utility Types

TypeScript includes utility types to manipulate existing types:

```typescript
type PartialPoint = Partial<Point>; // { x?: number; y?: number; }
type ReadonlyPoint = Readonly<Point>; // { readonly x: number; readonly y: number; }
type Merged = Point & { z: number }; // { x: number; y: number; z: number; }
```

## 34. Using `unknown` vs. `any`

Prefer using `unknown` over `any` to ensure type safety:

```typescript
function parseJSON(jsonString: string): unknown {
  return JSON.parse(jsonString);
}

const data: unknown = parseJSON("{ \"name\": \"John\", \"age\": 30 }");
// Use type assertion or type guards to access properties safely
```

## 35. Conditional Types

Conditional types enable complex type transformations based on conditions:

```typescript
type NonEmptyArray<T> = T extends Array<infer U> ? [U, ...U[]] : never;
type Numbers = NonEmptyArray<number>; // number[]
```

## 36. Using `/// <reference lib="..." />`

Use `/// <reference lib="..." />` to include specific lib types:

```typescript
/// <reference lib="esnext" />
const arr: Array<number> = [1, 2, 3];
```

## 37. ECMAScript Modules and `import.meta`

TypeScript supports `import.meta` for accessing meta information in modules:

```typescript
console.log(import.meta.url); // URL of the current module
```

## 38. Using Triple-Slash Directives for Type Declarations

Triple-slash directives can be used to include type declarations:

```typescript
/// <reference types="some-module" />
import { SomeModule } from "some-module";
```

## 39. Compiler API and Custom Transformers

For advanced scenarios, TypeScript's Compiler API allows writing custom transformers:

```typescript
import * as ts from "typescript";

const transformer: ts.TransformerFactory<ts.SourceFile> = (context) => {
  return (node) => {
    // Transformation logic here
    return node;
  };
};

const result = ts.transpileModule(code, {
  transformers: { before: [transformer] },
});
```