---
layout: post
title:      "Redux: mapStateToProps and mapDispatchToProps Explained"
date:       2017-11-18 21:58:07 +0000
permalink:  redux_mapstatetoprops_and_mapdispatchtoprops_explained
---

**mapStateToProps**

When learning Redux, we are first introduced to mapStateToProps.  A little confusing at first, but upon closer inspection, it is just a simple function (no imported library) that simply returns a specified part of the current state.

```
const mapStateToProps = (state) => {
     return { things: state.things }
};
```

When used with the Redux connect() function to export a component such as:

```export default connect(mapStateToProps)(MyComponent);```

we are exporting the combination of a component that is connected to the store.  Think of connect() as the glue or interface between the component and the store.  Any changes to the state will be reflected in the component because it is "connected" to mapStateToProps and that information is now made available to the component through a prop.  Keep in mind that is requires a React-Redux <Provider> component to be wrapped around the container component (using the 'App' component in the index.js).

Why do this? It allows the component to be agnostic to the fact it is part of a Redux app, and thus makes the component reusable.

Analogous to "reading" data, mapStateToProps gets the data that is fed to its component. 

But what if the component wants change the state?

That is where mapDispatchToProps comes in.

**mapDispatchToProps**

As implied in its name, this function directs the dispatching or sending of an action by pointing it to an action creator. For example:

```
const mapDispatchToProps = () => {
     return {
          addThing: addThing,
          doAnotherThing: doAnotherThing
     }
}
```

The action creator is made available to the component as a prop, which is usually tied to an event handler function contained in the component:

```
handleOnClick() {
     this.props.addThing();
};
```

However, returning the action creator is only one part.  We also want the send that returned action to the store.  How do we do that?

We use Redux's bindActionCreators(). To implement it, we:

```
import { bindActionCreators } from 'redux';
...
const mapDispatchToProps = (dispatch) => {
  return bindActionCreators({
         addThing: addThing,
         doAnotherThing: doAnotherThing
         }, dispatch);
};
```

The bindActionCreators() function accepts the action creator and the store's dispatch function as arguments, and returns a dispatch function that uses the return value of the action creator as its arguments.

Tying this all together is the connect() function, in which we pass mapDispatchToProps as a second argument.  For example:

 ```export default connect(mapStateToProps, mapDispatchToProps)(MyComponent);```
 
which will export a component that can both get the current state from the store, and dispatch an action to the store to trigger and update to the state.
