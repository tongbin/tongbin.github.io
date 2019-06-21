---
layout: posts
title:  "Typescript notes"
header:
  image: "/assets/images/road-through-desert-blog-header.jpg"

---

# Abstract

Simple notes for typescript learning. Based on [typescriptlang](https://www.typescriptlang.org/docs/home.html).



# Types

1. function with props

```typescript
interface Foo {
  (a: number, b: string): string[];
  foo: string;
}

let method: Foo = Object.assign(
  (a: number, b: string) => { return a * a; },
  { foo: 10 }
);
```

this will throw followed errors

```
Error: foo:number not assignable to foo:string
Error: number not assignable to string[] (return type)
```



2. enum

```typescript
enum Color {Red = 1, Green, Blue}
let colorName: string = Color[2];

console.log(colorName); // Displays 'Green' as its value is 2 above

```



3. Null and Undefined

By default `null` and `undefined` are subtypes of all other types. That means you can assign `null` and `undefined` to something like `number`.



4. Type assertions

    ... however, when using TypeScript with JSX, only `as`-style assertions are allowed.

   ```typescript
   let someValue: any = "this is a string";

   let strLength: number = (someValue as string).length;
   ```

# Interfaces

> ...the compiler only checks that at least the ones required are present and match the types required. There are some cases where TypeScript isn’t as lenient,... we didn’t have to explicitly say that the object we pass implements this interface like we might have to in other languages. Here, **it’s only the shape that matters**.

1. readonly vs const

> The easiest way to remember whether to use readonly or const is to ask whether you’re using it on a variable or a property. Variables use const whereas properties use readonly.

2. private properties.

According to [this page](https://curiosity-driven.org/private-properties-in-javascript), we could use closure, Symbol and WeakSet to implement private properties.

# Classes

> a class declaration creates two things: a type representing instances of the class and a constructor function. Because classes create types, you can use them in the same places you would be able to use interfaces.

```typescript
class Point {
    x: number;
    y: number;
}

interface Point3d extends Point {
    z: number;
}

let point3d: Point3d = {x: 1, y: 2, z: 3};
```

# Advanced Types

## Intersection Types

> An intersection type combines multiple types into one. For example, `Person` & `Serializable` & `Loggable` is a `Person` and `Serializable` and `Loggable`. That means an object of this type will have all members of all three types.

1. Partial

```typescript
type Partial<T> = { [P in keyof T]?: T[P]; };
```

2. keyof

```typescript
interface Todo {
  id: number;
  text: string;
  due: Date;
}
type TodoKeys = keyof Todo; // "id" | "text" | "due"
// function to getProperty
function getProperty<T, K extends keyof T>(o: T, name: K): T[K] {
    return o[name]; // o[name] is of type T[K]
}
```

3. Type Guards

```typescript
function isFish(pet: Fish | Bird): pet is Fish {
    return (<Fish>pet).swim !== undefined;
}
function isString(x: any): x is string {
    return typeof x === "string";
}
if (padder instanceof SpaceRepeatingPadder) {
    padder; // type narrowed to 'SpaceRepeatingPadder'
}
```
