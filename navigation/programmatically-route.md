## How to programmatically route with React Router (4)

Some times you need to do something before you route such as validation etc. Below is one example of how this can be done.

```
import React from 'react';
import { object } from 'prop-types';

const Example = ( props, { router } ) => {

  // Navigate to an exact route in a new window
  const navToNewWindow = (event) => {
    router.history.push("http://google.com")
  };

  // Navigate to a relative route
  const navTo = (event) => {
    router.history.push("/about")
  };

  // Navigate back a page in the browser history
  const goBack = (event) => {
    router.history.goBack()
  };

  return (
    <div>
      <button onClick={navToNewWindow}>Google</button>
      <button onClick={navTo}>Change route to About</button>
      <button onClick={goBack}>Go Back</button>
    </div>
  );
};

Example.contextTypes = {
  router: object,
}

export default Example;
```
