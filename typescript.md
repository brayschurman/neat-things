# Types, TypeScript, Type Checking

## Strategies for avoiding 'Warning: Forbidden non-null assertion.'

- use helper functions to check if variable is defined, if not throw an error

```javascript
export const getEnv = (v: string): string => {
  const ret = process.env[v];
  if (ret === undefined) {
    throw new Error("process.env." + v + " is undefined.");
  }
  return ret;
};
```

- or verify it exists and proceed that way

```javascript
function foo(instance: MyClass | undefined) {
  if (instance !== undefined) {
    instance.doWork();
  }
}
```

- for arrays where deeper references happen, assign a variable check that

```javascript
const member = newArr[index];

if (member === undefined) {
  throw new Error("Could not update member input, row index not found.");
}

if (field === "name") {
  member.name = e.target.value;
}
```

## Function Parameters

```typescript
type TechnologyCardProps = {
  name: string;
  description: string;
  documentation: string;
};

const TechnologyCard: React.FC<TechnologyCardProps> = ({
  name,
  description,
  documentation,
}) => {
  return (
    <section className="flex flex-col justify-center rounded border-2 border-gray-500 p-6 shadow-xl duration-500 motion-safe:hover:scale-105">
      <h2 className="text-lg text-gray-700">{name}</h2>
      <p className="text-sm text-gray-600">{description}</p>
      <Link
        className="m-auto mt-3 w-fit text-sm text-violet-500 underline decoration-dotted underline-offset-2"
        href={documentation}
        target="_blank"
        rel="noreferrer"
      >
        Documentation
      </Link>
    </section>
  );
};
```
