# Team Standards

## React Code

#### ES6 classes vs React.createClass (article on differences: https://toddmotto.com/react-create-class-versus-component/)

Pre es6 React.createClass ('this' is autobound)
```jsx
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

------

es6 React Class ('this' needs to be explicitly bound)
```jsx
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

------

#### Prefer stateless functional components when possible ([Benefits](https://hackernoon.com/react-stateless-functional-components-nine-wins-you-might-have-overlooked-997b0d933dbc))

Non-functional component without state
```jsx
import React, { PureComponent } from 'react';

export default class Contacts extends PureComponent {
  render() {
    return <div>{this.props.thing}</div>;
  }
};
```

Stateless functional component
```jsx
import React from 'react';

const Contacts = props => <div>{props.thing}</div>;

export default Contacts;
```

------

#### Use container/presentational component paradigm ([Dan Abramov Article](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0))

Logic and presentation in one component
```jsx
import React, { Component } from 'react';

class CommentList extends Component {
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

------

Logic and presentation split into two components
```jsx
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

export default CommentList;
```

------

#### Property initializers/arrow methods or es6 (for [reference](http://www.michalzalecki.com/react-components-and-class-properties/))

No initializers or fat arrow methods
```jsx
import React, { PureComponent } from 'react';
import { arrayOf, func, string } from 'prop-types';

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

------

With initializers and fat arrow methods
```jsx
import React, { PureComponent } from 'react';
import { arrayOf, func, string } from 'prop-types';

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

------

#### Performance Boosts (for [reference](https://facebook.github.io/react/docs/react-api.html#react.purecomponent))

When dealing with complex components, avoid stateless functional components and
instead use PureComponent or explicit shouldComponentUpdate checks. Be careful
with PureComponent as it only diffs props shallowly, which, if used incorrectly,
could lead to improper ui states/rendering.

shouldComponentUpdate example for deep comparisons

```jsx
import React, { Component } from 'react';

import ResultsList from './ResultsList';

export default class ResultsListContainer extends Component {
  state = { data: [] };

  componentWillMount() {
    this.getListDataOnAPoll();
  }

  getListDataOnAPoll() {
    const data = getDataFromApi(urlExample, timerExample);

    this.setState({ data });
  }

  render() {
    return <ResultsList data={this.state.data} />;
  }
}

// new file
import React, { Component } from 'react';
import { arrayOf, shape, string, number } from 'prop-types';
import { isEqual } from 'lodash';

export default class ResultsList extends Component {
  static propTypes = {
    data: arrayof(
      shape({
        id: string.isRequired,
        total: number,
      })
    ),
  };

  shouldComponentUpdate(nextProps) {
    const currentData = this.props.data;
    const newData = nextProps.data;

    // _.isEqual, lodash's isEqual performs a deep comparison between two values
    if (isEqual(currentData, newData)) return false;

    return true;
  }

  renderListItems() {
    return this.props.data.map(({ id, total }) => (
      <li>Item with id {id} has a total of {total}</li>
    ));
  }

  render() {
    return <ul>{this.renderListItems()}</ul>;
  }
}
```

------

## Linting

Many linting options are available. I recommend using [eslint](https://github.com/eslint/eslint) with [airbnb](https://github.com/airbnb/javascript) using [eslint-config-airbnb](https://www.npmjs.com/package/eslint-config-airbnb).

Eslint can be enabled for most IDEs/text editors
- [Webstorm](https://www.jetbrains.com/help/webstorm/2017.1/eslint.html)
- [Atom](http://www.acuriousanimal.com/2016/08/14/configuring-atom-with-eslint.html)
- [Vim](http://remarkablemark.org/blog/2016/09/28/vim-syntastic-eslint/)

Airbnb's [style guide](https://github.com/airbnb/javascript) is wildly popular
and contains some useful standards. So far the rules that I am disabling are:

```javascript
"react/jsx-filename-extension": [1, { "extensions": [".js", ".jsx"] }],
"react/require-default-props": 0,
"spaced-comment": 0
```

There are other [options](http://noeticforce.com/best-javascript-style-guide-for-maintainable-code) for style guides, including google's, node's, idiomatic, etc.

Regardless of the standard we follow, if, while developing, we come across some
rules that we think are ridiculous, we can discuss modifying/disabling them.

------

## CI

[CircleCI](https://circleci.com/)

[Travis-CI](https://travis-ci.org/)

[CodeShip](https://codeship.com/)

...and tons more

We need approval from higher ups <cough>Lance<cough>.

------

## Testing

Good [article](http://amzotti.github.io/testing/2015/03/16/what-is-the-difference-between-a-test-runner-testing-framework-assertion-library-and-a-testing-plugin/) on testing software classification.

#### Test Runners

Setup testing environment and run the tests. Some frameworks have built in test
runners.

- [Karma](http://karma-runner.github.io/1.0/index.html)

------

#### Testing Frameworks

What runs inside the testing server. All the methods and language used to
surround the assertion. Frameworks often include built in test running.

As an example, below is a snippet of Mocha. Everything, besides the code inside
the 'it' block comes from the testing framework. The code in the 'it' block
belongs to the assertion library.

```
describe('the todo.App', function() {
  context('the todo object', function(){

    it('should have all the necessary methods', function(){
      var msg = "method should exist";
      expect(todo.util.trimTodoName, msg).to.exist;
      expect(todo.util.isValidTodoName, msg).to.exist;
      expect(todo.util.getUniqueId, msg).to.exist;
    });
  });
});
```

- [Mocha](https://mochajs.org/)
- [Jasmine](https://jasmine.github.io/)
- [Jest](http://facebook.github.io/jest/)

------

#### Assertion Libraries

The assertion library is what actually runs the specs and determines whether any
given condition is valid or not. Ultimately, every test is ran by methods which
are derived from our assertion library. It is worth mentioning though, not every
framework needs an external assertion library. In these cases there is a
trade off between initial complexity and flexibility.

- [Chai](http://chaijs.com/)
- [Expect](https://github.com/mjackson/expect)
- [Jasmine](https://jasmine.github.io/)
- [Jest](http://facebook.github.io/jest/)

------

#### React component testing

- [Enzyme](https://github.com/airbnb/enzyme)
- Test Utils

------

#### Mocking support/Addons

- [Sinon](http://sinonjs.org/)
- [Jest](http://facebook.github.io/jest/)

------

#### Common testing patterns

- Karma, Mocha, Chai, Enzyme
- Jest, Enzyme
- Karma, Jasmine, Enzyme

------

## Project Structure

There are three main popular react project structure patterns:

------

### Filetype/component

- [example 1](https://survivejs.com/react/advanced-techniques/structuring-react-projects/)

There is a lot of variety within this category but it is characterized by
organizing files based on file type (i.e. components in components/ actions in
actions/, etc.).

#### Some code examples

Separated by file type with component individual directories
```
/src
  /actions
    /notifications.js
  /components
    /Header
    /Notifications
      /index.js
  /containers
    /Home
    /Notifications
      /index.js
  /images
    /logo.png
  /reducers
    /login.js
    /notifications.js
  /styles
    /header.scss
    /notifications.scss
  /utils
  index.js
```

------

Separated by file type with css encapsulated
```
/src
  /actions
    /notifications.js
  /components
    /Header
    /Notifications
      /index.js
      /notifications.scss
  /containers
    /Home
    /Notifications
      /index.js
  /images
    /logo.png
  /reducers
    /login.js
    /notifications.js
  /utils
  index.js
```

------

Separated by file type with flat components
```
/src
  /actions
    /notifications.js
  /components
    /Header.jsx
    /Notifications.jsx
  /containers
    /Home
    /Notifications
      /index.js
  /images
    /logo.png
  /reducers
    /login.js
    /notifications.js
  /styles
    notifications.scss
  /utils
  index.js
```

------

### Feature/Pods

- [example 1](https://jaysoo.ca/2016/02/28/organizing-redux-application/)
- [example 2](http://engineering.kapost.com/2016/01/organizing-large-react-applications/https://jaysoo.ca/2016/02/28/organizing-redux-application/)

This project structure is based on separating files by what feature or pods they
are concerned with (i.e. authentication, comments, profiles)

#### Some code examples

Separates files by what feature or pod they are concerned with
```
app/
  app.jsx
  authentication/
    authenticationContainer.jsx
    actions/
    ...
  comments/
    commentsContainer.jsx
    actions/
    ...
```

------

### Domain/view/route

- [example 1](https://marmelab.com/blog/2015/12/17/react-directory-structure.html)
- [example 2](https://survivejs.com/react/advanced-techniques/structuring-react-projects/)

This project structure can have some overlap with the feature structure but it
is narrowly focused on splitting code into the views and routes that are used

#### Some code examples

```
app/
  app.jsx
  authentication/
    authenticationContainer.jsx
    actions/
    ...
  comments/
    commentsContainer.jsx
    actions/
    ...
```

------

#### Extra articles
- https://medium.com/@msandin/strategies-for-organizing-code-2c9d690b6f33

------

## NPM or Yarn

[NPM](https://www.npmjs.com/)

[Yarn](https://yarnpkg.com/en/)

Security [concerns](http://blog.npmjs.org/post/141702881055/package-install-scripts-vulnerability) with NPM.

------

#### Use [semantic release](https://github.com/semantic-release/semantic-release)

Instead of writing meaningless commit messages, we can take our time to think about the changes in the codebase and write them down. Following formalized conventions it is then possible to generate a helpful changelog and to derive the next semantic version number from them.

When semantic-release is setup it will do that after every successful continuous integration build of your master branch (or any other branch you specify) and publish the new version for you. This way no human is directly involved in the release process and your releases are guaranteed to be unromantic and unsentimental.

------

## Github Standards

When working on a story, branch off of develop (using branch naming conventions)
and then pull request that branch back into develop when done. After it is peer
reviewed, it will be merged or commented upon.

#### Branch naming
- master
- develop
- feat/add-example or feature/add-example
- fix/correct-example-bug

------

#### Commit messages relate to semantic release use [conventional-changelog](https://github.com/conventional-changelog/conventional-changelog/blob/v0.5.3/conventions/angular.md) standards

Examples:

- feat: add login page
- fix: remove spurious re-renders
- perf(pencil): remove graphiteWidth option
- style: change margin
- docs: update commit message section
