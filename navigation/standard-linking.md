## Standard Menu using RR4 NavLink Component

Simple Example
```
import React from "react"
import { NavLink } from "react-router-dom"

const Menu = () => (
  <div>
    <NavLink to="/">Home</NavLink>
    <NavLink to="/about">About</NavLink>
  </div>
)

export default Menu
```

Advanced Example
```
import React from "react"
import { NavLink } from "react-router-dom"

const menuObject = [
  {
    "Name": "Home",
    "URL": "/",
  },
  {
    "Name": "About",
    "URL": "/about",
  },
]

const Menu = (menuObject) => (
  <div>
    {menuObject.map(({ Name, URL }) => (
      <NavLink to={URL}>{Name}</NavLink>
    ))}
  </div>
)

export default Menu
```
