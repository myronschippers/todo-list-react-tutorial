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

<img src="images/create-new-repo.gif" alt="create new GitHub repository" />

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

# Todo List, Front-End Application

This application is going to be a todo list but it's gonna have some very specific requirements that will change based on new feature requests that come in. As we add more features to our application the complexity will get greater and we'll add new technologies to support that need. Right now we are looking to create an application with a Header, Footer, and Daily Todo List. The concept is that this is a page the user can keep open on their device (computer, tablet, or phone) and check off items as they complete them. We don't really care about making the data persist at this time. 

**Application Requirements:**

1. Header
    * Application bar with the name of the application, "Todo List", and logo
    * Content should be centered
1. Footer
    * Content "© Todo Lit 2019"
1. Daily Todo List
    * Feature:
        * List Title
        * Add Todo to List
        * List of Todos
1. Add Todo to List (feature)
    * `<input>` for Name of Todo
    * `<input>` for Description of Todo
    * "Add Todo" button that will trigger the action of adding the information entered by the user to the list
1. List of Todos (feature)
    * Displays a series of todos in order of item entered with the first item entered displayed at the top of the list
    * Todos will not be displayed side by side but stacked one on top of the other.
1. Todo Item (feature)
    * User should be able to delete a Todo
    * A Todo should be able to be marked as complete
    * Display the name and description of the todo with the name having more visual importance

If you want to see a working version of this application you can checkout the [Sample Todo List Application](https://github.com/myronschippers/todo-list-app). It's branch structure is outlined in the `README.md` for that repo. At a high level just be aware that there is a branch for every phase that changes that state of that repo to what it would be at the end of that particular phase and the naming convention is branch `feature-phase-1-1` for **Phase 1.1**.

## Phase 1: Scaffolding our Application

In **Phase 1** we will complete all of the requirements we have been given including the setup of the master layout elements, creating a daily todo list rendered to the DOM, and a way to add items to our daily todo list. We'll start things out by putting together the overall master layout for the Todo List application.

**Major Topics:** 
* Component Creation
* Passing Data to Components via Props
* Working with JSX
* Directory composition

### Phase 1.1: Setting Up Master Layout

In **Phase 1.1** we'll create the master layout that will established the major structure for our application. It will give us an opportunity to talk a little bit more about what JSX is because `create-react-app` sets up our build to accept JSX in our React Javascript code.

Every master layout consists of the same three things a Header, Footer, and Main Body content areas. This configuration may change a little bit from project to project 90% of the time this is the core of our master layout. In some case you need navigation but our application doesn't require a navigation so that's not something we have to worry about.

**Sample Repo Branch:**

* [Todo after Phase 1.1](https://github.com/myronschippers/todo-list-app/tree/feature-phase-1-1)

### Phase 1.1: Setting Up Master Layout

**Editing (files):**

* `App.js` - located at `./src/components/App/App.js`
* `App.css` - located at `./src/components/App/App.css`
* `index.css` - located at `./src/index.css`
* `index.html` - located at `./public/index.html`

We are going to use something called [JSX](https://reactjs.org/docs/introducing-jsx.html) to help us write some HTML elements in our Javascript. JSX is a syntax extension to Javascript and it produces React "element". You can think of it as a way to write HTML in our Javascript. It is extremely handy when using React.

**Example JSX:**

```JSX
const element = <h1>Hello, world!</h1>;
```

Open up `./src/components/App/App.js` so we can begin to flesh out our application elements. Lets start by removing all of the existing markup except the outer most `<div>` and then I can highlight some of what is going on here.

```JS
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

class App extends Component {
    render() {
        return (
            <div className="scaffold">
            </div>
        );
    }
}

export default App;
```

A React Component is created with `class App extends Component` and every class based React Component `extends` the React base Component class to allow access to all of the special React things. Every React component class also must have a `render()` method. The build system will actually throw an error if you do not have one as well as a `return` inside of your `render()` method. Whatever is being returned is what will render as part of your view. All of your JSX normally goes in the `return` but it doesn't have to. You may have cases where you need to conditionally render something and might use the JSX just before the `return` still in the `render()` method.

Another difference you will notice in JSX is the addition of something called `className` it may seem like there is some magic going on there like with our `<div className="scaffold">` but this is just an element attribute representing the `class` attribute we are used to seeing. If you want to add a class(es) to an element you'll need to use the `className` attribute instead.

```JS
class App extends Component {
    render() {
        return (
            <div className="scaffold">
                STUFF
            </div>
        );
    }
}
```

**Outputs HTML:**

```HTML
<div class="scaffold">
    STUFF
</div>
```

I am going to supply you with the HTML markup and styling so that we can expedite the process of setting up the initial content. This initial markup is going to be just an initial layout. Once the mark up is in place we'll begin to look at how we "Componentize" the application and what that means.

First we'll need to add a class to our `index.html` file. This class is specifically for the CSS layout architecture.

**Change from:**

```HTML
<div id="root"></div>
```

**to be:**

```HTML
<div id="root" class="scaffoldPrimer"></div>
```

We have removed the content that `create-react-app` stubs in for us and put in it's place a `<div>` with the content of **STUFF** but now we need to add in those three major master layout areas to our `App.js` JSX content. All we're doing is setting up an HTML structure where we have places for the Header, Footer, and the Main Body content for our application. Eventually the `App.js` component will become our master template.

**In `App.js`:**

```JS
class App extends Component {
    render() {
        return (
            <div className="scaffold">
                <div className="scaffold-hd">
                    HEADER
                </div>
                <div className="scaffold-bd">
                    MAIN BODY
                </div>
                <div className="scaffold-ft">
                    FOOTER
                </div>
            </div>
        );
    }
}
```

With the markup / JSX in place to give our master layout structure, let's add the styling. Starting out in the `./src/index.css` replace all of the existing styles with the following.

```CSS
html,
body {
	height: 100%;
	padding: 0;
	margin: 0;
}

body {
	font-family: 'Open Sans', 'Segoe UI', Tahoma, Geneva, Arial, sans-serif;
}
```

These styles are specifically getting added to the `index.css` because they are base level element styles. Our next set of styling will be replacing all of the styles in `App.css`.

```CSS
/* ----------------------------------------------------------------------
Scaffold Primer
---------------------------------------------------------------------- */

.scaffoldPrimer {
    height: 100%;
    width: 100%;
    padding: 0;
    margin: 0;
}

/* ----------------------------------------------------------------------
Scaffold
---------------------------------------------------------------------- */

.scaffold {
	display: flex;
	height: 100%; /* needed for IE10 */
	min-height: 100%;
	flex-direction: column;
}

.scaffold-hd {
	flex: 0 0 auto;
}

.scaffold-bd {
	flex: 1 0 auto;
}

```

These styles are module specific styling that force the footer content to the bottom of our browser window even if the Main Body content of the page isn't enough content to push the footer to the bottom of the page. If you take a look at the browser where the application is currently loaded up you should see this styling in action. At this point the application should look something like this.

[Code Sample](https://github.com/myronschippers/todo-list-app/tree/feature-phase-1-1)
<img alt="Completing Phase 1.1" src="images/phase1.1-complete.png" />

### Phase 1.2: Header Markup and Styling

In **Phase 1.2** we're gonna update our application page content by creating the header content that will include a logo and name of the application. This concept of all of this content at the top of the page within a solid color block is referred to as an **App Bar** in most design/web shops.

**Sample Repo Branch:**

* [Todo after Phase 1.2](https://github.com/myronschippers/todo-list-app/tree/feature-phase-1-2)

**Editing (files):**

* `App.js` - located at `./src/components/App/App.js`
* `App.css` - located at `./src/components/App/App.css`

One of the things we'll leverage from the React content that `create-react-app` stubbed in for us is the React Logo SVG. We left the logo import at the to of the `App.js` where it says `import logo from './logo.svg';`. When the logo is imported we store it in the `logo` variable so we can use it in our JSX later on. 

```JS
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';
```

In the below code snippet we see the entire App component code but all we're updating is the JSX for the markup displayed to the user in place of the `HEADER` text we hand in there as a placeholder before. This new content starts with the `<header className="appBar">` element.

```JS
class App extends Component {
    render() {
        return (
            <div className="scaffold">
                <div className="scaffold-hd">
                    <header className="appBar">
                        <div className="appBar-identity">
                            <img src={logo} className="logoIcon" alt="logo" />
                            <h1 className="primeHdg">Todo List</h1>
                        </div>
                    </header>
                </div>
                <div className="scaffold-bd">
                    MAIN BODY
                </div>
                <div className="scaffold-ft">
                    FOOTER
                </div>
            </div>
        );
    }
}
```

Let's take a look at some of what is going on in our JSX code. Take particular notice of the `<img>` tag inside of `<div className="appBar-identity">`. For our `src` attribute you'll notice that we are using curly brackets after the `=` instead of quotes like in our standard HTML. We open up curly brackets (`src={}`) any time we want to insert Javascript into our JSX. This is a generalization but it's a good way to think about it. In this particular scenario it's the `logo` that we have imported with Javascript that we want to ser as the `src={log}` for our logo.

The other thing you may have noticed is that we aren't using a `class` attribute on our elements but are instead using an attribute of `className`. In JSX if we want to add a class for styling an element we have to use `<div className="style-class">`.

If we had stored a set of class names in a variable:

*example code not part of application:*

```JS
render() {
    const largeBtn = 'btn btn_big';

    return (
```

we could use that variable for the value of the class name:

*example code not part of application:*
```JS
render() {
    const largeBtn = 'btn btn_big';

    return (
        <div className={largeBtn}>
```

This approach becomes particularly helpful when we need to conditionally alter the classes being used on our elements.

All of our markup is in place but let's add some styling to the bottom of `App.css` in order to make our header content look a little more like an application.

```CSS
/* ----------------------------------------------------------------------
App Bar
---------------------------------------------------------------------- */

.appBar {
    display: flex;
    flex-flow: row wrap;
    justify-content: center;
    align-items: center;
    box-sizing: border-box;
    width: 100%;
    padding: 0 20px 0;
    background: #4682B4;
    box-shadow: 0px 2px 6px rgb(0, 0, 0, 0.2);
    position: relative;
    z-index: 800;
}

.appBar-identity {
    padding: 6px 0;
    color: #f0f8ff;
}

.appBar-actions {
    padding: 0;
}

/* ----------------------------------------------------------------------
Primary Heading (app bar content)
---------------------------------------------------------------------- */

.primeHdg {
    display: inline-block;
    margin: 0;
    padding: 0 4px;
    font-size: 1.4rem;
    vertical-align: middle;
}

/* ----------------------------------------------------------------------
Logo Icon (app bar content)
---------------------------------------------------------------------- */

.logoIcon {
    display: inline-block;
    width: 3.5rem;
    vertical-align: middle;
}

```

Let's check our browser again to make sure there are no errors and that our styles are showing up correctly for our new header content. It should look something like this.

[Code Sample](https://github.com/myronschippers/todo-list-app/tree/feature-phase-1-2)
<img alt="Application after completing Phase 1.2" src="images/phase1.2-complete.png" />
