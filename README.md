# Team Standards

## React Code

#### ES6 classes

Pre es6 React.createClass ('this' is autobound)
```javascript
import React from 'react';

const Contacts = React.createClass({
  getInitialState () {

  },
  propTypes: {

  },
  getDefaultProps() {

  },
  onChange() {

  },
  render() {
  }
});

export default Contacts;
```

es6 React Class ('this' needs to be explicitly bound)
```javascript
import React from 'react';

class Contacts extends React.Component {
  constructor() {
    super();
    this.state = {};
    this.onChange = this.onChange.bind(this);
  }

  onChange() {

  }

  render() {
  }
}

Contacts.propTypes = {};

Contacts.defaultProps = {};

export default Contacts;
```

#### Prefer stateless functional components when possible

Non-functional component without state
```javascript
import React, { PureComponent } from 'react';

export default class Contacts extends PureComponent {
  render() {
    return <div>{this.props.thing}</div>;
  }
};
```

Stateless functional component
```javascript
import React from 'react';

const Contacts = props => <div>{props.thing}</div>;

export default Contacts;
```

#### Use container/presentational component paradigm [Dan Abramov Article](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)

Logic and presentation in one component
```javascript
import React, { Component } from 'react';

class CommentListContainer extends Component {
  state = { comments: [] };

  componentDidMount() {
    fetchSomeComments(comments => this.setState({ comments }));
  }

  renderComments() {
    return this.state.comments.map(({ body, author }) => <li>{body}—{author}</li>);
  }

  render() {
    return (
      <ul>
        {this.renderComments()}
      </ul>
    );
  }
}
```

Logic and presentation split into two components
```javascript
import React, { Component } from 'react';
import CommentList from './CommentList';

class CommentListContainer extends Component {
  state = { comments: [] };

  componentDidMount() {
    fetchSomeComments(comments =>
      this.setState({ comments: comments }));
  }

  render() {
    return <CommentList comments={this.state.comments} />;
  }
}

// New file
import React from 'react';

const CommentList = ({ comments }) => {
  const renderComments = () => comments
    .map(({ body, author }) => <li>{body}—{author}</li>);

  return <ul>{renderComments()}</ul>;
};
```

#### Property initializers and fat arrow methods??

No initializers or fat arrow methods
```javascript
class Dropdown extends PureComponent {
  constructor() {
    super();

    this.state = {
      selectedValues: [],
    };

    this.onChange = this.onChange.bind(this);
  }

  componentWillMount() {
    this.setState({ selectedKeys: this.getOptions() });
  }

  onChange(selectedKeys) {
    this.setState({ selectedKeys });

    this.props.onKeyChange(selectedKeys.map(key => key.value));
  }

  ...

  render() {
    ...

    return <Select />;
  }
}

Dropdown.propTypes = {
  selectableKeys: arrayOf(string),
  onKeyChange: func,
};

Dropdown.defaultProps = {
  selectedValues: [],
  onKeyChange: () => console.log('this is a function'),
};

export default Dropdown;
```

With initializers and fat arrow methods
```javascript
export default class Dropdown extends PureComponent {
  static propTypes = {
    selectableKeys: arrayOf(string),
    onKeyChange: func,
  };

  static defaultProps = {
    selectedValues: [],
    onKeyChange: () => console.log('this is a function'),
  };

  state = { selectedValues: [] };

  componentWillMount() {
    this.setState({ selectedKeys: this.getOptions() });
  }

  onChange = (selectedKeys) => {
    this.setState({ selectedKeys });

    this.props.onKeyChange(selectedKeys.map(key => key.value));
  }

  ...

  render() {
    ...

    return <Select />;
  }
}
```

## Linting

Many linting options available. I recommend airbnb

## CI

[CircleCI](https://circleci.com/)
[Travis-CI](https://travis-ci.org/)
[CodeShip](https://codeship.com/)

...and tons more

Need approval from higher ups.

## Testing

## Project Structure

## NPM or Yarn

[NPM](https://www.npmjs.com/)
[Yarn](https://yarnpkg.com/en/)

Security [concerns](http://blog.npmjs.org/post/141702881055/package-install-scripts-vulnerability) with NPM.

#### Use [semantic release](https://github.com/semantic-release/semantic-release)

Instead of writing meaningless commit messages, we can take our time to think about the changes in the codebase and write them down. Following formalized conventions it is then possible to generate a helpful changelog and to derive the next semantic version number from them.

When semantic-release is setup it will do that after every successful continuous integration build of your master branch (or any other branch you specify) and publish the new version for you. This way no human is directly involved in the release process and your releases are guaranteed to be unromantic and unsentimental.

## Github Standards

When working on a story, branch off of develop (using branch naming conventions)
and then pull request that branch back into develop when done. After it is peer
reviewed, it will be merged or commented upon.

#### Branch naming
master
develop
feat/add-example or feature/add-example
fix/correct-example-bug

#### Commit messages relate to semanatic release use [conventional-changelog](https://github.com/conventional-changelog/conventional-changelog/blob/v0.5.3/conventions/angular.md) standards

Example:

- feat: add login page
- fix: remove spurious re-renders
- perf(pencil): remove graphiteWidth option
- style: change margin
- docs: update commit message section
