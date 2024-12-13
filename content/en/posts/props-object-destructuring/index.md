---
title: "Props Object Destructuring"
date: 2024-11-27
draft: false
hideToc: true
tags: ["Frontend", "React", "Components", "Props", "JavaScript", "Object", "Destructuring"]
---

# Greetings

Greetings from a passionate beginner front-end engineer to every single of you. I hope that you are having a wonderful day, you are improving yourself and wining your silent battles.

# Intro
After finishing the *React Basics* course provided by *Meta* on Coursera platform, which is part of the *Front-end Developer Professional Certificate*, I ended up being puzzled about the way that a component accepts a parameter. In *React* language, the way that a component accepts prop data.

# CurrentMessage React Component
Consider the following React component:
```JavaScript
function CurrentMessage( {day} ){
    let message;

    if(day == 1){
        message = <h1>Here we go again!</h1>
    }
    ...
    ...
    ...

    return(
        <div>
            { message }
        </div>
    );
};

export default CurrentMessage;
```

When I saw the `CurrentMessage( { day } )` I wondered:
- *Is this a JSX expression?*
- *Am I passing a JavaScript object as a parameter?*

Therefore, I did a little research.
So buckle up and allow me to show what I found ;)

# Props
As you may already know, in React, data flows from the parent component to the child component, constructing a parent-child relationship. This is done via **props**.

**props** are immutable, that is read-only, therefore the child cannot operate on them but only to consume/read them. This data comes from the outside of the child component and passed by the parent component.

Consider this simple example:
```JavaScript
// App.js
import ChildComponent from './ChildComponent';

function App(){
    return(
        <div>
            <ChildComponent data={'Hello'} />
        </div>
    );
};

export default App;
```
```JavaScript
function ChildComponent(props){
    return(
        <h1>I received: {props.data}</h1>
    );
};

export default ChildComponent;
```

So far so good! It is known that a child accepts data from its parent through props, this is why `props` parameter is added in the definition of the component.

Therefore, what is the *day* we saw in `CurrentMessage( { day } )`?

# Object Destructuring
Consider the following simple example, which illustrates object destructuring in JavaScript:
```JavaScript
const user = {firstName: "John",
              lastName: "Doe",
              username: "un1d3nt1f13d"
             }

let {firstName: first,
     lastName: last,
     username
    } = user;

console.log(`The user ${first} ${last} has the following username, ${username}`);
```

The above is a simple example of destructuring an object in vanilla JavaScript. The only thing that may need a little elaboration is the way that the destructuring happened.

When we want to destructure the object properties to variables that have a different name we use the following mapping:
```JavaScript
let {sourceProperty: targetVariable} = object;
```

In any other case, the property names are used as variables:
```JavaScript
let { username, firstName, lastName } = user;
// The order does not matter
```

# Props Object
Back to our example in React, some data were passed to the `ChildComponent` component. Therefore, `props` is an object with a `data` property:
```JavaScript
{"data": 'Hello'} // props object
```
# Solving The Mystery
Therefore, incorporating the above knowledge, the `CurrentMessage( { day } )` performs an object destructuring of the `props` object.

Thus, the `ChildComponent` can be modified as such in order to use the data directly:
```JavaScript
function ChildComponent( { data } ){
    return(
        <h1>I received: { data }</h1>
    );
};

export default ChildComponent;
```