# propTypes and defaultProps

## propTypes

- use for all props

## defaultProps

- use defaultProps for all non-required props and even for required props if you
  are at all concerned about that prop not being passed to your component. This
  allows you to not worry about type checking and to ensure that your component
  gets the proper props. Particularly useful for async operations.

```
import React from 'react';
import {
  string,
  number,
  arrayOf,
  shape,
} from 'prop-types';

const BlogPost = ({
  blogRanking,
  content,
  comments,
}) => {
  const {
    header,
    message,
  } = content;

  const renderComments = () => comments.map(({ user, comment }) => (
    <div key={user}>
      {user}: {comment}
    </div>
  ));

  return (
    <div>
      <h1>{header}</h1>
      <p>{message}</p>
      <span>{blogRanking}</span>
      {renderComments()}
    </div>
  );
};

BlogPost.propTypes = {
  content: shape({
    header: string.isRequired,
    message: string.isRequired,
  }).isRequired,
  blogRanking: number.isRequired,
  comments: arrayOf(
    shape({
      user: string.isRequired,
      comment: string.isRequired,
    }).isRequired,
  ).isRequired,
};

BlogPost.defaultProps = {
  content: {
    header: '',
    message: '',
  },
  comments: [],
  blogRanking: 1,
};

export default BlogPost;
```

## Destructuring props

Props can and should be destructured for smaller components.

```
const BlogPost = ({ blogRanking, message }) => <div>{message} {blogRanking}</div>;
```

While destructuring, you can assign default values to props, but if you have a ton
of props, use default props instead.

- Fine
```
const BlogPost = ({ blogRanking = 0, message = '' }) => (
  <div>{message} {blogRanking}</div>;
);
```

- Not Okay (use default props)
```
const BlogPost = ({
  blogRanking = 0,
  message = ''
  content: {
    comments = [],
    media: {
      process: '',
      example: [],
      foo: {
        bar: '',
      } = {},
    } = {},
  } = {}
}) => (
  ...renderLogic
);
```
