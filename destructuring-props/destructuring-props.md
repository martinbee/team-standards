## If you are repeating this.props or props etc try using destructuring to clean up your markup.

```
import React from "react"

const App = (props) => {
  const {
    model,
    title
  } = props
  return (
    <div>
      <h1>{title}</h1>
      <input
        type="text"
        value={model.name}
        placeholder="Your Name"/>
    </div>
  )
}

export default App
```
