# React, JSX

Don't use && for conditional rendering, use ternary operator. This prevents "strange bugs" I guess.

```javascript
{showModal ? <Modal/> : null}
```
