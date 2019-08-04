# Todo List React Tutorial

This tutorial will teach ReactJS by building a Todo List. We will start by building the Front-End and then build on top of it little by little demonstrating Back-End and database technologies along the way. We will be building the Todo List from the ground up leveraging `create-react-app` for our Front-End bundling system.

## Getting Started

**Technologies**

* [`create-react-app`](https://github.com/facebook/create-react-app)
* [`redux`](https://redux.js.org/)
* [`react-router-dom`](https://www.npmjs.com/package/react-router-dom)

### Setup Bundler and Initialize Repository

Open your terminal and navigate to the directory where you want your application to live.

**run (in terminal):**

```
npx create-react-app todo-list-app
```

This line of code will create a directory called `todo-list-app` inside the directory you navigated to. Not only did it create the application directory for you but if you look inside the directory you'll notice it has also scaffolded the initial application code you will need.

```
todo-list-app
├── README.md
├── node_modules
├── package.json
├── .gitignore
├── public
│   ├── favicon.ico
│   ├── index.html
│   └── manifest.json
└── src
    ├── App.css
    ├── App.js
    ├── App.test.js
    ├── index.css
    ├── index.js
    ├── logo.svg
    └── serviceWorker.js
```

Navigate into the the `todo-list-app` application directory from the terminal.

**run (in terminal):**

```
cd todo-list-app
```

There are some dependencies that we are going to need to add. From the terminal now that we are in the `todo-list-app` directory we'll use `npm` to install the necessary dependencies by running the following command.

**run (in terminal):**

```
npm install --save redux react-router-dom 
```

This one command installs `redux` and `react-router-dom` as dependencies in our project. The `README.md` in your `todo-list-app` application directory has details on all of the scripts available for running the build but we're going to take a look at just one of them for now. Go ahead and run the following command from your terminal in the `todo-list-app` directory.

**run (in terminal):**

```
npm start
```

When this is down building the Front-End files it will automagically launch a new tab in your web browser serve up a local version of the site. The start command has integrated into it a watch so when you save changes to your code it will run a live refresh of the webpage. At this point you could start developing anything you want.

SWEET!!!

Let's go ahead and setup your the repository now. From your terminal while still in the `todo-list-app` directory run the following.

**run (in terminal):**

```
git init
```

Open the `todo-list-app` in your favorite editor. I personally recommend VS Code in case you're looking for a recommendation. We're going to be adding some lines of code to the `.gitignore` file. Add the following to the file under the `# dependencies` section. We already have a lot of different things listed in there so we only need to add the one extra thing.

**add to `.gitignore`:**

```
/package-lock.json
```

With this addition we simply need to commit the initial state of our code. From the terminal run the following.

**run (in terminal):**

```
git add .
git commit -m "initial application codebase"
```

With this we have a local repository instantiated on our machine but we need to get it up on GitHub. Open your browser and navigate to you GitHub page. In the top right corner you will see a "+" icon. Go ahead and click on the plus. In the dropdown select **New repository**. In the **Repository name** field enter in "todo-list-app" then scroll to the bottom of the page and click on the green **Create repository** button.

GitHub will create the repository for you and then all we need to do is git our local repository pushed up to this new remote repository. We'll do this by running these two lines of code in our terminal.

**run (in terminal):**

```
git remote add origin https://github.com/myronschippers/todo-list-app.git
```

**then run:**

```
git push -u origin master
```

We're not going to worry about branching strategies with this tutorial but if you want to use a branching strategy please feel free. For the rest of us will just be working on the `master` branch.

### Restructuring the Base Application Code

With the code up and running I am going to walk you through some structure updates because I like to work in a little different of a structure for my projects in order to keep things organized. After that I am going to change the components from functional components to class based components so that we can focus on a more Object Oriented Programming approach. I know know functional components are the new hotness but just bare with me. First let's move some files around. 

Create a new director called `components` inside of the `src` directory.

```
todo-list-app
└── src
    └── components
```

Inside of the `components` directory create another directory called `App`.

```
todo-list-app
└── src
    └── components
        └── App
```

Move `./src/App.js`, `./src/App.css`, `./src/App.test.js`, and `./src/logo.svg` into `./src/components/App`. Our directory structure should look something like this:

```
todo-list-app
├── README.md
├── node_modules
├── package.json
├── .gitignore
├── public
│   ├── favicon.ico
│   ├── index.html
│   └── manifest.json
└── src
    ├── components
    │   └── App
    │       ├── App.css
    │       ├── App.js
    │       ├── App.test.js
    │       └── logo.svg
    ├── index.css
    ├── index.js
    └── serviceWorker.js
```

Your browser would have refreshed after you made those changes and if we take a look we'll likely see some errors because we have to update the file paths.

Open up `./src/index.js`.

**Change:**

```JS
import App from './App';
```

**to be:**

```JS
import App from './components/App/App';
```

If you look back at the browser again everything should be working just fine. This is something that is setup in the `create-react-app` build where it will surface any JS error or React errors directly in your browser window. This will help us debug errors as we come across them.

Open up `./src/components/App/App.js` so we can convert it to being a class based component instead of a functional component.

**Change:**

```JS
import React from 'react';
```

**to be:**

```JS
import React, { Component } from 'react';
```

**AND**

**Change:**

```JS
function App() {
    return (
        <div className="App">
            <header className="App-header">
                <img src={logo} className="App-logo" alt="logo" />
                <p>
                    Edit <code>src/App.js</code> and save to reload.
                </p>
                <a
                className="App-link"
                href="https://reactjs.org"
                target="_blank"
                rel="noopener noreferrer"
                >
                    Learn React
                </a>
            </header>
        </div>
    );
}
```

**to be:**

```JS
class App extends Component {
    render() {
        return (
            <div className="App">
                <header className="App-header">
                    <img src={logo} className="App-logo" alt="logo" />
                    <p>
                        Edit <code>src/App.js</code> and save to reload.
                    </p>
                    <a
                    className="App-link"
                    href="https://reactjs.org"
                    target="_blank"
                    rel="noopener noreferrer"
                    >
                        Learn React
                    </a>
                </header>
            </div>
        );
    }
}
```

From here we're ready to start getting into the actual application and write some of our own components.

### Scaffolding our Application Layout and Router
