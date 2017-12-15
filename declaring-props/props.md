## If your props are limited in number show defaults and types at the top of the component as documentation if not show them at the bottom.

[https://github.com/facebook/prop-types](https://github.com/facebook/prop-types)


In React props have been pulled out into it's own module. Install prop-types via npm to use as recommended below.

```
import React, { Component } from "react"
import { string, object } from "prop-types"

class App extends Component {
  // Declare propTypes as static properties as early as possible
  static propTypes = {
    model: object.isRequired,
    title: string
  }

  // Default props below propTypes
  static defaultProps = {
    model: {
      id: 0
    },
    title: 'Your Name'
  }

  render() {
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
}

export default App
```

or as a Pure component

```
import React from "react"
import { string, object } from "prop-types"

const App = () => {
  // Declare propTypes as static properties as early as possible
  static propTypes = {
    model: object.isRequired,
    title: string
  }

  // Default props below propTypes
  static defaultProps = {
    model: {
      id: 0
    },
    title: 'Your Name'
  }

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
