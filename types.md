# Types, TypeScript, Type Checking

## Strategies for avoiding 'Warning: Forbidden non-null assertion.'

* use helper functions to check if variable is defined, if not throw an error

```javascript
export const getEnv = (v: string): string => {
    const ret = process.env[v];
    if (ret === undefined) {
        throw new Error("process.env." + v + " is undefined.");
    }
    return ret;
}
```

* or verify it exists and proceed that way
  
```javascript
function foo(instance: MyClass | undefined) {
    if (instance !== undefined) {
        instance.doWork();
    }
}
```

* for arrays where deeper references happen, assign a variable check that

```javascript
const member = newArr[index];

if (member === undefined) {
    throw new Error("Could not update member input, row index not found.");
}

if (field === "name") {
    member.name = e.target.value;
}
```
