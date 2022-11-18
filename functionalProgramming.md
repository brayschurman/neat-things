# Functional Programming

## Pure Functions

These must satisfy two requirements.

1. **Not depend on state**, ie return the same thing for the same arguments, everytime
2. **Cannot cause any side effects**, ie I/O, modifying mutable objects, reassignments

Functional programming encourages **pure** functions. In the example below, we use the spread operator to first copy `arr` . This way we avoid any side effects

```javascript
const arr = [2, 4, 6];

function addElement(arr, ele) {
    return [...arr, ele];
}

console.log("modified data", addElement(arr, 8)); // Expected Output: [2, 4, 6, 8]
console.log("original data", arr); // Expected Output: [2, 4, 6]
```
