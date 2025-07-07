---
title: "What is TypeScript?"
description: "Just what is TypeScript and how is it different to JavaScript?"
lead: "Just what is TypeScript and how is it different to JavaScript?"
date: 2023-05-01T04:46:31+00:00
lastmod: 2023-12-04T11:30:00+01:00
draft: false
images: []
menu:
  docs:
    parent: "npm"
weight: 120
toc: true
---

## 10,000 ft Overview

TypeScript is a strongly typed programming language that builds on [JavaScript]({{< relref "what-is-javascript" >}}) by adding static type definitions. Developed and maintained by Microsoft, TypeScript compiles to plain JavaScript, meaning it can run anywhere JavaScript runs - in browsers, on [Node.js]({{< relref "what-are-npm-and-nodejs" >}}), and in any JavaScript engine.

The main advantage of TypeScript is that it catches errors at compile time rather than runtime, making development more predictable and debugging easier. It's particularly valuable for large-scale applications where maintaining code quality and preventing bugs becomes increasingly important.

TypeScript is widely adopted in enterprise environments and is the foundation for many popular frameworks and libraries including [Angular]({{< relref "angular/what-is-angular" >}}), which is built entirely in TypeScript. Many [React]({{< relref "react/what-is-react" >}}) developers also choose TypeScript for improved developer experience and code reliability.

{{< alert icon="💡" text="TypeScript is a superset of JavaScript, meaning all valid JavaScript code is also valid TypeScript code. You can gradually adopt TypeScript in existing JavaScript projects without rewriting everything." />}}

## Beginner Information

TypeScript adds optional static typing to JavaScript, which means you can specify what type of data a variable should hold. This helps catch errors early and makes code more self-documenting.

**Basic TypeScript Types:**
{{< highlight typescript "linenos=inline">}}
// Basic types
let name: string = "Alice";
let age: number = 30;
let isActive: boolean = true;
let hobbies: string[] = ["reading", "coding", "gaming"];

// Object types
interface User {
  id: number;
  name: string;
  email: string;
  isActive?: boolean; // Optional property
}

const user: User = {
  id: 1,
  name: "Alice",
  email: "alice@example.com"
};

// Function types
function greetUser(user: User): string {
  return `Hello, ${user.name}!`;
}

// Arrow function with types
const calculateTotal = (price: number, tax: number): number => {
  return price + (price * tax);
};

// Array types
const numbers: number[] = [1, 2, 3, 4, 5];
const users: User[] = [user];
{{< /highlight >}}

**Compilation Process:**

{{< highlight bash >}}
# Install TypeScript globally
npm install -g typescript

# Create a TypeScript file (app.ts)
# Compile to JavaScript
tsc app.ts

# This creates app.js which can run in any JavaScript environment

# Watch mode for automatic compilation
tsc app.ts --watch

# Initialize TypeScript configuration
tsc --init
{{< /highlight >}}

**TypeScript Configuration (tsconfig.json):**

{{< highlight json "linenos=inline">}}
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "lib": ["ES2020", "DOM"],
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
{{< /highlight >}}

**Benefits of TypeScript:**

- **Error Prevention**: Catch type-related errors at compile time
- **Better IDE Support**: Enhanced autocomplete, refactoring, and navigation
- **Self-Documenting Code**: Types serve as inline documentation
- **Easier Refactoring**: Safer large-scale code changes
- **Team Collaboration**: Clearer interfaces between different parts of code

**Common Use Cases:**

- Large-scale web applications
- Enterprise software development
- Library and framework development
- API development with Node.js
- React and Angular applications

## Intermediary Information

TypeScript provides advanced type system features that enable sophisticated type checking and code organization patterns.

**Advanced Type Features:**

{{< highlight typescript "linenos=inline">}}
// Union types
type Status = "pending" | "approved" | "rejected";
let currentStatus: Status = "pending";

// Intersection types
interface Person {
  name: string;
  age: number;
}

interface Employee {
  employeeId: string;
  department: string;
}

type PersonEmployee = Person & Employee;

// Generic types
interface ApiResponse<T> {
  data: T;
  success: boolean;
  message?: string;
}

function fetchData<T>(url: string): Promise<ApiResponse<T>> {
  return fetch(url).then(response => response.json());
}

// Usage
const userResponse: Promise<ApiResponse<User>> = fetchData<User>('/api/user');

// Conditional types
type NonNullable<T> = T extends null | undefined ? never : T;

// Mapped types
type Partial<T> = {
  [P in keyof T]?: T[P];
};

type Required<T> = {
  [P in keyof T]-?: T[P];
};
{{< /highlight >}}

**Classes and Inheritance:**

{{< highlight typescript "linenos=inline">}}
abstract class Animal {
  protected name: string;
  
  constructor(name: string) {
    this.name = name;
  }
  
  abstract makeSound(): string;
  
  move(): string {
    return `${this.name} is moving`;
  }
}

class Dog extends Animal {
  private breed: string;
  
  constructor(name: string, breed: string) {
    super(name);
    this.breed = breed;
  }
  
  makeSound(): string {
    return "Woof!";
  }
  
  getBreed(): string {
    return this.breed;
  }
}

// Interface implementation
interface Flyable {
  fly(): string;
}

class Bird extends Animal implements Flyable {
  makeSound(): string {
    return "Tweet!";
  }
  
  fly(): string {
    return `${this.name} is flying`;
  }
}
{{< /highlight >}}

**Modules and Namespaces:**

{{< highlight typescript "linenos=inline">}}
// Module exports
export interface Config {
  apiUrl: string;
  timeout: number;
}

export class ApiClient {
  constructor(private config: Config) {}
  
  async get<T>(endpoint: string): Promise<T> {
    const response = await fetch(`${this.config.apiUrl}${endpoint}`);
    return response.json();
  }
}

export default ApiClient;

// Module imports
import ApiClient, { Config } from './api-client';
import * as Utils from './utils';

// Namespace (less common in modern TypeScript)
namespace Geometry {
  export interface Point {
    x: number;
    y: number;
  }
  
  export function distance(p1: Point, p2: Point): number {
    return Math.sqrt((p2.x - p1.x) ** 2 + (p2.y - p1.y) ** 2);
  }
}
{{< /highlight >}}

**Type Guards and Assertions:**

{{< highlight typescript "linenos=inline">}}
// Type guards
function isString(value: unknown): value is string {
  return typeof value === 'string';
}

function isUser(obj: any): obj is User {
  return obj && typeof obj.id === 'number' && typeof obj.name === 'string';
}

// Usage
function processValue(value: string | number) {
  if (isString(value)) {
    // TypeScript knows value is string here
    console.log(value.toUpperCase());
  } else {
    // TypeScript knows value is number here
    console.log(value.toFixed(2));
  }
}

// Type assertions
const userInput = document.getElementById('userInput') as HTMLInputElement;
const userData = JSON.parse(response) as User;

// Non-null assertion operator
const element = document.getElementById('myElement')!; // Tells TypeScript element is not null
{{< /highlight >}}

## Advanced Information

Advanced TypeScript involves sophisticated type manipulation, tooling integration, and enterprise-scale architecture patterns.

**Advanced Type Manipulation:**

{{< highlight typescript "linenos=inline">}}
// Template literal types
type EventName<T extends string> = `on${Capitalize<T>}`;
type ClickEvent = EventName<"click">; // "onClick"

// Recursive types
type Json = string | number | boolean | null | Json[] | { [key: string]: Json };

// Utility types
interface Todo {
  id: number;
  title: string;
  completed: boolean;
  userId: number;
}

type TodoPreview = Pick<Todo, "title" | "completed">;
type TodoInfo = Omit<Todo, "completed" | "userId">;
type TodoUpdate = Partial<Todo>;

// Advanced mapped types
type Getters<T> = {
  [K in keyof T as `get${Capitalize<string & K>}`]: () => T[K];
};

type UserGetters = Getters<User>; 
// { getId(): number; getName(): string; getEmail(): string; }

// Conditional type inference
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : never;
type FunctionReturn = ReturnType<(x: string) => number>; // number

// Branded types for type safety
type UserId = number & { __brand: 'UserId' };
type ProductId = number & { __brand: 'ProductId' };

function createUserId(id: number): UserId {
  return id as UserId;
}

function getUser(id: UserId): User {
  // This prevents accidentally passing a ProductId
  return users.find(user => user.id === id);
}
{{< /highlight >}}

**Decorators and Metadata:**

{{< highlight typescript "linenos=inline">}}
// Enable decorators in tsconfig.json: "experimentalDecorators": true

// Class decorator
function Entity(table: string) {
  return function <T extends new (...args: any[]) => {}>(constructor: T) {
    return class extends constructor {
      tableName = table;
    };
  };
}

// Property decorator
function Column(options?: { name?: string; type?: string }) {
  return function (target: any, propertyKey: string) {
    const columns = Reflect.getMetadata('columns', target) || [];
    columns.push({ propertyKey, ...options });
    Reflect.defineMetadata('columns', columns, target);
  };
}

// Method decorator
function Validate(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
  const originalMethod = descriptor.value;
  
  descriptor.value = function (...args: any[]) {
    // Validation logic
    console.log('Validating input...');
    return originalMethod.apply(this, args);
  };
}

@Entity('users')
class UserEntity {
  @Column({ type: 'integer', name: 'user_id' })
  id: number;
  
  @Column({ type: 'varchar' })
  name: string;
  
  @Validate
  save() {
    console.log('Saving user...');
  }
}
{{< /highlight >}}

**Enterprise Patterns and Architecture:**

{{< highlight typescript "linenos=inline">}}
// Dependency injection pattern
interface Logger {
  log(message: string): void;
}

interface Database {
  save<T>(entity: T): Promise<T>;
  find<T>(id: string): Promise<T | null>;
}

class UserService {
  constructor(
    private logger: Logger,
    private database: Database
  ) {}
  
  async createUser(userData: Partial<User>): Promise<User> {
    this.logger.log('Creating new user');
    const user = new User(userData);
    return await this.database.save(user);
  }
}

// Factory pattern with generics
interface Factory<T> {
  create(...args: any[]): T;
}

class UserFactory implements Factory<User> {
  create(name: string, email: string): User {
    return {
      id: Math.random(),
      name,
      email,
      isActive: true
    };
  }
}

// Repository pattern
interface Repository<T, K> {
  findById(id: K): Promise<T | null>;
  save(entity: T): Promise<T>;
  delete(id: K): Promise<void>;
  findAll(): Promise<T[]>;
}

class UserRepository implements Repository<User, number> {
  async findById(id: number): Promise<User | null> {
    // Implementation
    return null;
  }
  
  async save(user: User): Promise<User> {
    // Implementation
    return user;
  }
  
  async delete(id: number): Promise<void> {
    // Implementation
  }
  
  async findAll(): Promise<User[]> {
    // Implementation
    return [];
  }
}
{{< /highlight >}}

**Performance and Build Optimization:**

{{< highlight json "linenos=inline">}}
{
  "compilerOptions": {
    "incremental": true,
    "tsBuildInfoFile": "./build-cache/buildinfo",
    "composite": true,
    "declaration": true,
    "declarationMap": true,
    "sourceMap": true,
    "removeComments": true,
    "importHelpers": true,
    "downlevelIteration": true,
    "isolatedModules": true,
    "noEmitOnError": true,
    "strict": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true,
    "noUncheckedIndexedAccess": true,
    "exactOptionalPropertyTypes": true
  },
  "references": [
    { "path": "./packages/core" },
    { "path": "./packages/utils" }
  ]
}
{{< /highlight >}}

**Integration with Build Tools:**

- **Webpack**: ts-loader, awesome-typescript-loader
- **Rollup**: @rollup/plugin-typescript
- **Vite**: Built-in TypeScript support
- **esbuild**: Ultra-fast TypeScript compilation
- **SWC**: Rust-based super-fast TypeScript compiler

TypeScript has become essential for enterprise JavaScript development, offering the safety of static typing while maintaining JavaScript's flexibility. Its adoption continues to grow as teams recognize the benefits of catching errors early and improving code maintainability.

## External Links

- [TypeScript Documentation](https://www.typescriptlang.org/docs/) @ TypeScript
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html) @ TypeScript
- [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/) @ Basarat Ali Syed
