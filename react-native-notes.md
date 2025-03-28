# React Native notes

_Status: Published_
_Created: 2017-11-18 11:08:48_
_Tags: javascript, react_

Lifecycle
constructor(props) {
  super(props);
}
render (){}

componentDidMount() {}
componentDidUpdate() {}
componentWillUnmount() {}

React with typoscript
# Make a new directory
$ mkdir react-typescript

# Change to this directory within the terminal
$ cd react-typescript

# Initialise a new npm project with defaults
$ npm init -y

# Install React dependencies
$ npm install react react-dom

# Make index.html and App.tsx in src folder
$ mkdir src
$ cd src
$ touch index.html
$ touch App.tsx

# Open the directory in your favorite editor
$ code .

then index.html
<code>
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>React + TypeScript</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>

<div id="main"></div>
<script src="./App.tsx"></script>
</body>
</html>
</code>


# Install Parcel to our DevDependencies
$ npm i parcel-bundler -D

# Install TypeScript
$ npm i typescript -D

# Install types for React and ReactDOM
$ npm i -D @types/react @types/react-dom

add to pack.json
"scripts": {
    "dev": "parcel src/index.html"
  },


create Counter.tsx
<code>
import * as React from 'react';

export default class Counter extends React.Component {
    state = {
        count: 0
    };

    increment = () => {
        this.setState({
            count: (this.state.count += 1)
        });
    };

    decrement = () => {
        this.setState({
            count: (this.state.count -= 1)
        });
    };

    render () {
        return (
            <div>
                <h1>{this.state.count}</h1>
                <button onClick={this.increment}>Increment</button>
                <button onClick={this.decrement}>Decrement</button>
            </div>
        );
    }
}</code>

app.tsx
<code>
import * as React from 'react';
import { render } from 'react-dom';

import Counter from './Components/Counter';

render(<Counter />, document.getElementById('main'));
</code>

run:
$ npm run dev
