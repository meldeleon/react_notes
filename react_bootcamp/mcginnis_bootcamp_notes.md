# [Tyler McGinnis React Bootcamp](https://ui.dev/free-react-bootcamp)

## Day 1:

- React is a library for building user interfaces. Was initially created in 2014.
- What makes react special?

  1. Compositional mode

  - You can build a punch of components that you composed together. The component model works even for routing.
  - Components are the building blocks for an UI. Reduces complexity, updating one component is more siloed. Highly reusable in different places.
  - When building components think about what state it needs from its parent and what its UI needs to look like.
  - Let's compose, fb profile in plain javascript.
    ```javascript
    function getProfilePic(username) {
      return 'https://photo.fb.com/'+ username
    }
    function getProfileLink(username) {
      return 'https://fb.com/'+ username
    }
    function getAvatarInfo(username) {
      return {
        pic: getProfilePic(username),
        link: getProfileLink(username)
    }
    getAvatarInfo('juiceboxhero')
    ```
  - Now let's compose it in react.

    ```javascript
    function ProfilePic(props) {
      return (
        <img src = {'https://photo.fb.com/' + props.username'} />
      )
    }
    function ProfileLink(props){
      return (
        <a href = {'https://fb.com/' + props.username'} />
      )
    }
    function Avatar(props) {
      return (
        <div>
          <ProfilePic username={props.username}>
          <ProfileLink username={props.username}>
        </div>
      )
    }

    <Avatar username="juiceboxhero">
    ```

  2. Unidirectional Dataflow

  - jquery would set up event handlers, and your state would exist in the dom, and you could update the dom to update state.
  - eventhandlers would update the state, and there was no real structure. shared mutable state throughout the file can create "weird state cases"
  - react is responsible for rendering the UI. Your UI is a function of your state. You state is not updating the ui, it's building it.

  3. Explicit Mutations

  - You can explicitly set the state of any component. react takes care of everything else.

  ```javascript
  this.setState({
    handle: "juiceboxhero",
    auth: true,
  })
  ```

  4. Just Javascript

  - It's mostly just JS, a lot of similar intuition around functions comes into play with component writing.
  - React doesn't like to recreate things that JS already does.

- Building our first react app.
  - check (index.html)[index.html]
  - createElement creates and object representation of a dom node.
  ```javascript
  const headerElement = React.createElement("h1", { id: "header" }, "Tyler")
  ```
  is tantamount to
  ```html
  <h1 id="header>
  Tyler
  </h1>
  ```
- `ReactDOM.render` renders a reac element into the DOM.
- React creates an object representation of the DOM, and can check whether or not the DOM representation has been updated by checking its memory refrences.
- component vs element: a component is a function or a class that optionally accepts inputs and returns a react element.
- you are not putting "html" inside of your js, react needs a compiler that turns html into React.createElement() calls. In this case we use babel.
- props get passed into components, and passes data to the component to be used to generate elements.

## Day 2

- A react element is the most fundamental building block of React.
- jsx is just an abstraction over createElement. Components return elements.
- Components can have their own state, that doesn't get used in any other component. This can help you break up complex states into manageable, bite-sized pieces.
- React need key ids over iterables so that it can tell when something has changed in an iterable.
- Functional vs Class Components
  - if you want to have state that is managed by a react component, you need to use a class component rather than a functional component.
  - class components rely on es6 classes. They are constructed with the following structure:
  ```javascript
  class App extends React.Component {
    constructor(props) {
      super(props)
      this.state = {
        friends: ["jordan", "tru", "chau"],
      }
    }
    render() {
      return (
        <div>
          <FriendsList list={this.state.friends} />
        </div>
      )
    }
  }
  ```
  - class components need a `render` method, in which you describe the UI.
  - class components have built-in state, to set the state you need to call `constructor(props)` and `super(props)` to set the scope for `this`
  - functional components are also called stateless functional components.
  -
