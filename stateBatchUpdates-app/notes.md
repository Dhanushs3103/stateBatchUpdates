# State and Batch updates explation

#### Delayed State update explaination : 
 -In the below code, why it is displaying the older value in the console is because in react `setCount` is asynchronous.
  After updating the state, React will eventually re-render the component to reflect the new state. But this re-render doesn’t happen right away.
  It’s scheduled and managed by React's reconciliation process, which is why it seems asynchronous. 
  So if you try to log the value of count right after calling setCount, you'll still see the old value, not the updated one. 
  This is because the update to count hasn't been applied yet—it's scheduled to happen later. This process is known as batching. 

 ```
 import React from 'react'

function App() {
  const [count, setCount] = React.useState(0);

  const handleClick = () => {
    setCount(count + 1);
    setCount(count + 1);
    setCount(count + 1);
		console.log(count);
  };

  return (
    <div>
      <p>Button is clicked {count} times</p>
      <button onClick={handleClick}>Click Me</button>
    </div>
  );
}

export default App
```

---

#### Multiple State Updates :

-In the below code, why count value is not updated to 3 as expected because
- Each `setCount(count + 1)` call doesn't immediately update the `count`. They all see the same initial value of `count`.
- Due to React's batching, all these updates are processed together.
- As a result, `count` increases only by 1, not 3, even though `setCount` is called three times.

```
import React from 'react'


function App() {
  const [count, setCount] = React.useState(0);

  const handleClick = () => {
    setCount(count + 1);
    setCount(count + 1);
    setCount(count + 1);
		console.log(count);
  };

  return (
    <div>
      <p>Button is clicked {count} times</p>
      <button onClick={handleClick}>Click Me</button>
    </div>
  );
}

export default App
```

---