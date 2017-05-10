# Team Standards

## React Code

#### ES6 classes
```javascript
var s = "JavaScript syntax highlighting";
alert(s);
```
#### Prefer stateless functional components when possible
```javascript
var s = "JavaScript syntax highlighting";
alert(s);
```

#### Use container/presentational component paradigm [Dan Abramov Article](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)
```javascript
var s = "JavaScript syntax highlighting";
alert(s);
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

## CI

## Testing

## Project Structure

## NPM or Yarn

#### Use [semantic release](https://github.com/semantic-release/semantic-release)

## Github Standards

#### Branch naming


#### Commit messages relate to semanatic release use [conventional-changelog](https://github.com/conventional-changelog/conventional-changelog/blob/v0.5.3/conventions/angular.md) standards
