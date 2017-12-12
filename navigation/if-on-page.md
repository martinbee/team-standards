## Judge if you are on a page to show template partial etc.

```
import React, { Component } from "react"
import PropTypes from "prop-types"

class App extends Component {
  static propTypes = {
    match: PropTypes.object.isRequired,
    location: PropTypes.object.isRequired,
    history: PropTypes.object.isRequired
  }
  render() {
    const { match, location, history } = this.props
    const onPage = location.pathname === "/page"
    const pageTemplate = <h1>On Page</h1>
    const notPageTemplate = <h1>Not On Page</h1>
    return (
      <div>
        {onPage ? pageTemplate : notPageTemplate}
      </div>
    )
  }
}

export default App
```
