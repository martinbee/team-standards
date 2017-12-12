## Working with dates in js/moment

```
import React from 'react';
import moment from 'moment';

const Example = (props) => {
  const today = new Date()
  const dd = today.getDate()
  const mm = today.getMonth()+1 // January is 0!
  const yyyy = today.getFullYear()
  const createdAt = 1513108674

  return (
    <div>
      <p>Today is: {yyyy}</p>
      <p>The day is: {dd}</p>
      <p>The month is: {mm}</p>
      <p>The year is: {yyyy}</p>
      {moment(createdAt).fromNow()}
    </div>
  )
}

export default Example
```
