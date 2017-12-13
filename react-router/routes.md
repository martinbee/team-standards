## Route object file routes.js

Simple example
```
import Root from './Root';
import Home from './Home/';
import About from './About/';
import Search from './Search/';
import Blog from './Blog/';

export default [
  { component: Root,
    routes: [
      { path: '/',
        exact: true,
        component: Home
      },
      {
        path: '/about',
        component: About,
        name: 'About',
      },
      {
        path: '/search',
        component: Search,
        name: 'Search',
      },
      {
        path: '/blog',
        component: Blog,
        name: 'Blog',
      },
    ]
  }
]
```

Advanced example using modules
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
        routes: [
          {
            path: "/empty",
            exact: true,
            component: pages.Home,
            name: "Home",
          },
          {
            component: core.NotFound,
            name: "Not Found",
          },
        ],
      },
      {
        path: "/",
        component: core.LayoutStandard,
        routes: [
          {
            path: "/",
            exact: true,
            component: pages.Home,
            name: "Home",
          },
          {
            path: "/search",
            exact: true,
            component: pages.Search,
            name: "Search",
          },
          {
            component: core.NotFound,
            name: "Not Found",
          },
          {
            path: "/child/:id",
            component: pages.Home,
            routes: [
              {
                path: "/child/:id/grand-child",
                component: pages.Home,
              },
            ],
          },
        ],
      },
    ],
  },
]
```
