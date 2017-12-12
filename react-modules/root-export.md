## You can export a group of components in a /components folder with a root export like below:

./core/index.js example
```
import * as components from "./components"

const constants = {
  NAME: "core",
}

export { components }
export default { components, constants }
```

./core/components/index.js example
```
export { default as App } from "./App"
export { default as Header } from "./Header"
export { default as Footer } from "./Footer"
export { default as LayoutEmpty } from "./LayoutEmpty"
export { default as LayoutStandard } from "./LayoutStandard"
export { default as NotFound } from "./NotFound"
```

And then you can import a whole section such as "core" and namespace to them as in this example:

```
import { components as core } from "./core"
import { components as pages } from "./pages"

// A route config is just data passed into the <Route>
export default [
  {
    component: core.App,
    routes: [
      {
        path: "/empty",
        component: core.LayoutEmpty,
        ...
```
