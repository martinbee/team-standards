## App.js empty root layout component

```
import React from "react" // eslint-disable-line no-unused-vars
import { renderRoutes } from "react-router-config"
import { object } from "prop-types"

const App = ({ route }) => <div>{ renderRoutes(route.routes) }</div>

App.propTypes = {
  route: object, // eslint-disable-line react/forbid-prop-types
}
App.defaultProps = {
  route: [],
}

export default App
```
