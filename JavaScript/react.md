# React

## Conditional Rendering

Don't use && for conditional rendering, use ternary operator.

```javascript
{
  showModal ? <Modal /> : null;
}
```

## Props

### Spread Operator

Use the spread operator to pass props to a component.

```javascript
const props = { name: "John", age: 42 };
<MyComponent {...props} />;
```

# Hooks

## useRef

Used to access DOM nodes or React elements created in the render method and persist for the lifetime of the component (between renders).

```javascript
import React, { useRef } from "react";

function TextInputWithFocusButton() {
  const inputEl = (useRef < HTMLInputElement) | (null > null);

  const onButtonClick = () => {
    // `current` points to the mounted text input element
    inputEl.current?.focus();
  };

  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}

export default TextInputWithFocusButton;
```

## useContext

Used to pass data through the component tree without having to pass props down manually at every level. This avoids prop drilling and also makes it easier to refactor and share state between components.

```javascript
import React, { useContext } from "react";

const themes = {
  light: {
    foreground: "#000000",
    background: "#eeeeee",
  },
  dark: {
    foreground: "#ffffff",
    background: "#222222",
  },
};

const ThemeContext = React.createContext(themes.light);

function App() {
  return (
    <ThemeContext.Provider value={themes.dark}>
      <Toolbar />
    </ThemeContext.Provider>
  );
}

function Toolbar(props) {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}
 export default App;


// in a totally different file, import the context and use it
import React, { useContext } from "react";
import { ThemeContext } from "./App";
function ThemedButton() {
  const theme = useContext(ThemeContext);
  return (
    <button style={{ background: theme.background, color: theme.foreground }}>
      I am styled by theme context!
    </button>
  );

```

## useReducer

Used to manage state in a component. It is an alternative to useState, and ideal for complex state logic that involves multiple sub-values or when the next state depends on the previous one.

```javascript
import React, { useReducer } from "react";

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "decrement":
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({ type: "decrement" })}>-</button>
      <button onClick={() => dispatch({ type: "increment" })}>+</button>
    </>
  );
}

export default Counter;
```

## useMemo

Used to memoize expensive functions so that they are not re-run on every render. I've often been confused with useMemo and useRef, but useMemo is used to memoize functions, and useRef is used to access DOM nodes or React elements created in the render method and persist for the lifetime of the component (between renders), like a button click.

```javascript
import React, { useMemo } from "react";

function ExpensiveComponent({ a, b }) {
  const expensiveResult = useMemo(() => {
    return a * b;
  }, [a, b]);

  return <div>{expensiveResult}</div>;
}

export default ExpensiveComponent;
```
