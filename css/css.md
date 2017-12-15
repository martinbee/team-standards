## We use SCSS at this timerExample

Turning CSS into JS in our eyes is not fully baked so we recommend using scss and inporting those into a single .css file so you can reference vars.
CSS/JS hybrids also don't allow css experts to walk into a project and be proficient of the bat.

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
