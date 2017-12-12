## LayoutEmpty.js Empty page template

```
import React from "react" // eslint-disable-line no-unused-vars
import { renderRoutes } from "react-router-config"
import PropTypes from "prop-types"

const LayoutEmpty = ({ route }) => (
  <div>
    {renderRoutes(route.routes)}
  </div>
)

LayoutEmpty.propTypes = {
  route: PropTypes.object, // eslint-disable-line react/forbid-prop-types
}

LayoutEmpty.defaultProps = {
  route: {},
}

export default LayoutEmpty
```
