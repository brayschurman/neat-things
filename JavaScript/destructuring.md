# Destructuring

Makes it possible to unpack values from arrays or properties from object in distinct variables. All done in a single line.

```javascript
let a, b, rest;
[a, b] = [10, 20];

console.log(a);
// 10

console.log(b);
// 20

[a, b, ...rest] = [10, 20, 30, 40, 50];

console.log(rest);
// [30, 40, 50]
```

Same goes for objects.

```javascript
const user = {
    id: 42,
    isVerified: true
};

const {
    id,
    isVerified
} = user;

console.log(id) // 42
console.log(isVerified) // true
```
