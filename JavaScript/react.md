# React, JSX

Don't use && for conditional rendering, use ternary operator.

```javascript
{
  showModal ? <Modal /> : null;
}
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
