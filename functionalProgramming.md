# Functional Programming

## Pure Functions

These must satisfy two requirements.

1. **Not depend on state**, ie return the same output for the same input, everytime
2. **Cannot cause any side effects**, ie I/O, modifying mutable objects, reassignments

Functional programming encourages **pure** functions. In the example below, we use the spread operator to make a copy of `arr` , instead of directly manipulating it. This way we avoid any side effects.

```javascript
const arr = [2, 4, 6];

function addElement(arr, ele) {
    return [...arr, ele];
}

console.log("modified data", addElement(arr, 8)); // Expected Output: [2, 4, 6, 8]
console.log("original data", arr); // Expected Output: [2, 4, 6]
```

## Immutability

Make sure objects *are not* **reassignable**

Make sure objects *are* **immutable**

Most mutator methods can be replaced by other methods, examples:

```javascript
const a = Object.freeze([4, 5, 6]);

// Instead of: a.push(7, 8, 9);
const b = a.concat(7, 8, 9);

// Instead of: a.pop();
const c = a.slice(0, -1);

// Instead of: a.unshift(1, 2, 3);
const d = [1, 2, 3].concat(a);

// Instead of: a.shift();
const e = a.slice(1);

// Instead of: a.sort(myCompareFunction);
const f = R.sort(myCompareFunction, a); // R = Ramda

// Instead of: a.reverse();
const g = R.reverse(a); // R = Ramda 
```
