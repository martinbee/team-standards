## If you are repeating this.props or props etc try using destructuring to clean up your markup.

Bad Example:
```
import React from "react"

const App = (props) => {
  return (
    <div>
      <h1>{props.title}</h1>
      <input
        type="text"
        value={props.model.name}
        placeholder="Your Name"/>
    </div>
  )
}

export default App
```

Good Example:
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
