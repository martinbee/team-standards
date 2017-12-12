## Sample index.js file

```
import React from "react" // eslint-disable-line no-unused-vars
import ReactDOM from "react-dom"
import { BrowserRouter as Router } from "react-router-dom"
import { renderRoutes } from "react-router-config"
import registerServiceWorker from "./registerServiceWorker"
import routes from "./routes"

const Root = () => (
  <Router>
    {renderRoutes(routes)}
  </Router>
)

ReactDOM.render(<Root />, document.getElementById("root"))
registerServiceWorker()
```
