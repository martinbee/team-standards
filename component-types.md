## React Component Templates in es6

The following 6 templates show best practices when assembling react components.

There are two types: Here is a summary of the two.

Container components use the "class <NameOfConponent> extends Component" prefix and support the full React render lifecycle including the most popular "componentDidMount". This is the area where ajax calls take place and initial state is set. The is also the area where your methods are written that listen for events to bubble up from the Display components.

Display components are also referred to as dumb or pure components because they are fed data properties or "props" who's data never changes. They can have event listener that can send events like "onClick" or "onChange" up to their parent Container component they are nested in. It can sometimes be helpful to think of these are templates and their parents as the change method center controlling the "state" of the app.




### Container component with componentDidMount lifecycle hook
```
import React, { Component } from "react"

class Container extends Component {
  componentDidMount() {
    console.log("Container just loaded, sweet.")
  }
  render() {
    return (
      <div>
        <h1>Hello from Container</h1>
      </div>
    )
  }
}

export default Container
```

### Container component with nested display/pure component
```
import React, { Component } from "react"
import Display from "./displayComponent"

class Container extends Component {
  componentDidMount() {
    console.log("Container just loaded, sweet.")
  }
  render() {
    return (
      <div>
        <Display />
      </div>
    )
  }
}

export default Container
```

### Self returning display/pure component
```
import React from "react"

const Display = () => (
  <div>
    <h1>Hello World</h1>
  </div>
)

export default Display
```

### Display/pure component with const inside and return for seperation
```
import React from "react"

const Display = () => {
  const title = "Once upon a time..."
  return (
    <div>
      <h1>{title}</h1>
    </div>
  )
}

export default Display
```


### Nesting display/pure component inside display/pure component
```
import React from "react"
import DisplaySub from "./displaySubComponent.js"

const DisplayParent = () => (
  <div>
    <DisplaySub />
  </div>
)

export default DisplayParent
```


### Self returning display/pure sub component
```
import React from "react"

const DisplaySub = () => (
  <div>
    <h2>Sub Component</h2>
  </div>
)

export default DisplaySub
```
