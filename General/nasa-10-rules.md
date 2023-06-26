# The Power of 10: Rules for Developing Safety-Critical Code (NASA)

[Source](https://en.wikipedia.org/wiki/The_Power_of_10:_Rules_for_Developing_Safety-Critical_Code)

## 1. Simple Control Constructs

No unnecessary gotos, breaks, continues, multiple exits from loops, multiple returns from functions, or other confusing control constructs.

```javascript
/* Don't do this */
for (let i = 0; i < 10; i++) {
  if (i == 5) {
    break; /* Avoid using breaks in the middle of loops */
  }
  console.log(i);
}

/* Do this */
for (let i = 0; i < 10; i++) {
  if (i != 5) {
    console.log(i); /* Only print if i != 5 */
  }
}
```

## 2. Limit All Loops

All loops are bound by a fixed upper limit. This limit is checked at the top of the loop and is an Integer.

```javascript
for (let i = 0; i < 10; i++) {
  console.log(i);
}
```

## 3. Don't Use The Heap

No dynamic memory allocation, aka Malloc or Free. You should exclusively use the stack for all memory allocation. In JavaScript this could be interpreted as avoiding unnecessary object creation.

Reasoning: The heap is a shared resource, and if you use it, you must be careful to avoid memory leaks and fragmentation. The stack is not shared, and is much easier to manage.

By limiting code to only using stack memory, you can set an upper bound on the amount of memory that will be used.

```javascript
/* Don't do this */
for (let i = 0; i < 10000; i++) {
  let obj = { prop: i }; /* Avoid creating new objects in a loop */
}

/* Do this */
let obj = { prop: 0 };
for (let i = 0; i < 10000; i++) {
  obj.prop = i; /* Reuse the same object */
}
```

## 4. Limit Function Size

A function should only perform one thing. They should be no longer than 60 lines. The greatly increases readability, maintainability, debugging, and testing.

```javascript
/* Don't do this */
function doEverything() {
  /* 100 lines of code */
}

/* Do this */
function doOneThing() {
  /* 30 lines of code */
}

function doAnotherThing() {
  /* 30 lines of code */
}

function doEverything() {
  doOneThing();
  doAnotherThing();
}
```

## 5. Practice Data Hiding

Practice of data hiding is about hiding internal details. It restricts access to the inner workings of a class or object, and only exposes what is necessary. This maintains data integrity.

```javascript
/* Don't do this */
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}

/* Do this */
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  getName() {
    return this.name;
  }

  getAge() {
    return this.age;
  }
}
```

## 6. Check Return Values

Always check the return values of functions, and handle errors appropriately. This is especially important for functions that return error codes.

```javascript
/* Don't do this */
function doSomething() {
  let result = doSomethingElse();
  if (result == 0) {
    /* Handle error */
  }
}

/* Do this */
function doSomething() {
  let result = doSomethingElse();
  if (result == 0) {
    /* Handle error */
  } else {
    /* Handle success */
  }
}
```

## 7. Use The Preprocessor Sparingly

The preprocessor is a tool that allows you to define macros, which are replaced by the preprocessor before compilation. This can be used to define constants, or to create inline functions. In a language like JavaScript, this would be equivalent to using a transpiler like Babel or frameworks like React.

```javascript
/* Don't do this */
#define PI 3.14159265358979323846

/* Do this */
const PI = 3.14159265358979323846;
```

## 8. Limit Pointer Use, and no Function Pointers

When you assign an object to a variable in JavaScript, you're assigning a reference to the location in memory where that object is stored. If you assign that variable to another variable, both will point to the same object, and changes made through one variable will be visible when accessing the object through the other variable. This might seem similar to dereferencing a pointer, but it's not quite the same thing.

```javascript
/* Don't do this */
let obj = { prop: 0 };
let obj2 = obj;
obj2.prop = 1;
console.log(obj.prop); /* 1 */

/* Do this */
let obj = { prop: 0 };
let obj2 = { prop: 1 };
console.log(obj.prop); /* 0 */
```

## 9. Be Pedantic

When developing, ensure all warnings are enabled, and treat them as errors. This will help you catch bugs early, and ensure your code is as clean as possible.

- [ESLint](https://eslint.org/)
- [Prettier](https://prettier.io/)
- [TypeScript](https://www.typescriptlang.org/)

## 10. Test, Test, Test

Test your code. Test it again. Test it some more. Test it until you're sure it works. Then test it again. Test it in every way you can think of. Test it in ways you can't think of. Test it until you're sure it works. Then test it again.

- [Jest](https://jestjs.io/)
- [React Testing Library](https://testing-library.com/docs/react-testing-library/intro/)
