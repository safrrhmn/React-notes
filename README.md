# Table of Contents

1. [React.Component](#React.Component)
   
      + [render()](#render)
      + [constructor()](#constructor)
      + [componentDidMount()](#componentDidMount)
      + [componentDidUpdate()](#componentDidUpdate)
      + [componentWillUnmount()](#componentWillUnmount)
      + [setState()](#setState)

2. [Instance Properties](#Instance_Properties)
      + [props](#props)
      + [state](#state)

3. [Important packages](#Important_packages)
      + [PropTypes](#PropTypes)
      + [react-router-dom](#react-router-dom)
      

# [React.Component](https://reactjs.org/docs/react-component.html)
> React component is the most important part. The `React.Component` should be extended in almost all case. React team stringly recommand against creating the base component class. 

## Component Lifecycle: `Common methods`
### [render()](https://reactjs.org/docs/react-component.html#render)
> **The render() method is the only required method in a class component.** When it is called, it examines `this.props` and `this.state` and return *React Element, Arrays and Fragments, Portals, String and number and Booleans or null*
### [constructor()](https://reactjs.org/docs/react-component.html#constructor)
> There is no need to implement constructor if the state is not initialized or the methods not binded. In react

1. Constructor is used to initialize the state and
2. For binding event handler

#### Do not do:
1. Do not call `setState()` inside the constructor
```javascript
constructor(props) {
  super(props);
  // Don't call this.setState() here!
  this.state = { counter: 0 };
  this.handleClick = this.handleClick.bind(this);
}
```
2. Do not copy `props` into the `state`
```javascript
constructor(props) {
 super(props);
 // Don't do this!
 this.state = { color: props.color };
}
```
### [componentDidMount()](https://reactjs.org/docs/react-component.html#componentdidmount)
>`componentDidMount()` is the lifecycle hook that is run right after the component is added to the DOM and should be used if you're fetching remote data or doing an Ajax request. `componentDidMount()` is invoked immediately after a component is mounted. Initialization that requires DOM nodes should go here. If you need to load data from a remote endpoint, this is a good place to instantiate the network request. Setting state in this method will trigger a re-rendering.

```javascript
import React, { Component } from 'react';
import fetchUser from '../utils/UserAPI';

class User extends Component {
  constructor(props) {
    super(props)

    this.state = {
      name: '',
      age: ''
    }
  }

  componentDidMount() {
    fetchUser().then((user) => this.setState({
      name: user.name,
      age: user.age
    }))
  }

  render() {
    return (
      <div>
        <p>Name: {this.state.name}</p>
        <p>Age: {this.state.age}</p>
      </div>
    )
  }
}

export default User;
```

> What's happening here:
You'll notice that this component has a componentDidMount() lifecycle event. This component seems pretty straightforward, but let's walk through the order of how it works:

>The render() method is called which updates the page with a <div> that has one paragraph for the name and one paragraph for the age. What's important to realize is that this.state.name and this.state.age are empty strings (at first), so the name and age don't actually display
Once the component has been mounted, the componentDidMount() lifecycle event occurs
The fetchUser request from the UserAPI is run which sends a request to the user database
When the data is returned, setState() is called and updates the name and age properties
Since the state has changed, render() gets called again. This re-renders the page, but now this.state.name and this.state.age have values
Let's use componentDidMount() to fetch real users from a server in our Contacts app!


### [componentDidUpdate()](https://reactjs.org/docs/react-component.html#componentdidupdate)
### [componentWillUnmount()](https://reactjs.org/docs/react-component.html#componentwillunmount)
### [setState()](https://reactjs.org/docs/react-component.html#setstate)
> This is primary way to update the interface and notify React to rerender the state
```javascript
this.setState((state, props) => {
  return {counter: state.counter + props.step};
});
```
A callback function can also be invoked during `setState()`

```javascript
setState(stateChange[, callback])
```
## [Functional and Class Component](https://reactjs.org/docs/components-and-props.html#function-and-class-components)
> The simplest way to define a component is to write a JavaScript function:

```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```
>We can also use an ES6 class to define a component:

```javascript
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

# [Instance_Properties](https://reactjs.org/docs/react-component.html#instance-properties-1)
### [props](https://reactjs.org/docs/react-component.html#props)
> `this.props` is defined by the caller of this component

```javascript
function Comment(props) {
  return (
    <div className="Comment">
      <UserInfo user={props.author} />
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```
### [state](https://reactjs.org/docs/react-component.html#state)
> It contains the data specific to the component and should be plain javascript object.

## [Controlled Components](https://reactjs.org/docs/forms.html#controlled-components)
>From elements such as `<input>, <textarea>, and <select>` maintain their own state. We can combine the two by making the React state be the “single source of truth”. Then the React component that renders a form also controls what happens in that form on subsequent user input. An input form element whose value is controlled by React in this way is called a “controlled component”.

```javascript
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  //to handle the event in realtime. Follow along the usage in `onChange` in input
  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

# Important_packages:
## [PropTypes](https://www.npmjs.com/package/prop-types)
> It enforces the type of the property and if optional or required
usage:

```javascript
ListContacts.protoType = {
        contacts: PropTypes.array.isRequired,
        onDeleteContact: PropTypes.func.isRequired
}
```
## [react-router-dom](https://www.npmjs.com/package/react-router-dom)
