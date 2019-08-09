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

1. Landing Page
    * Splash Hero Image with a button that says **Get Started**
    * On click of the **Get Started** button user is taken to the **Dashboard**
1. Header
    * Colored application bar at the top of the page
    * Text on the left that says, "Todo List"
    * Navigation on the right with three links; "Daily", "Categories", & "Dashboard"
1. Footer
    * Centered text saying, `&copy; Todo List 2019`
1. Custom Todo List (feature)
    * Completed items should be displayed at the bottom of the list
    * Incomplete items should be displayed toward the top of the list
    * List data structure

    ```JS
    {
        name: '',
        createdOn: '',
        todos: [
            {}, // todo item
        ],
    }
    ```

1. Todo Item (feature)
    * Each item has 4 major features; **Title**, **Details**, **Status**, & **Delete**
    * Visually starting on the left
        * Checkbox representing the item status
        * Title text with the detail text just below
        * Delete button / icon
    * Data structure

    ```JS
    {
        title: 'string',
        details: 'string',
        complete: false,
    }
    ```

1. Add Todo Item (feature)
    * There should be fields to enter in **Title** & **Details** along with a button for the user to click when they have entered in the necessary information
    * On the click of the **Add Todo** button a data item is created and added to the appropriate Todo List
1. Make Custom Todo List (feature)
    * Has fields to enter in a **Name** and **Description** for the new todo list but only the **Name** is required
    * On click of the **Make List** button create a new todo list for the user to add items to. once the list has been created make sure to 
1. Daily (page)
    * Single Todo List that would only display the todo items for the day. This is not a todo list the user can change any other details of the list.
    * Features:
        * Add Todo item
        * Todo List
        * Todo Item
1. Categories (page)
    * A list of all the custom todo lists that the user has created.
    * The individual todo category/grouping will display:
        * Name of Category
        * Percentage Complete
        * Total Number of Todos
        * Number of Completed Todos
        * A Delete Button
1. Specific Category (page)
    * Custom todo list created by the user. It will have an overall level of completion based on the number of todo items completed. This will also have a name displayed on the page that is used to identify the list.
    * Features:
        * Heading displaying the name of the list.
            * The name should be editable allowing the user to change it if needed.
        * Visualization of level of completion (# of completed todos / total # of todos)
        * Add Todo Item
        * Todo List
1. Dashboard (page)
    * Features
        * Daily List (heading)
        * Add Todo Item - for adding to the daily todo list
        * Todo List - for the daily todos
        * "Custom Todo Lists" (heading)
        * Make Todo List
        * List of custom todo lists
        * Individual Custom Todo List Each shows the list's name and the percentage of completion and a button that says "Open"

If you want to see a working version of this application you can checkout the [Sample Todo List](https://github.com/myronschippers/todo-list-app). It's branch structure is outlined in the `README.md` for that repo but at a high level just be aware that there is a branch for every phase that changes that state of that repo to what it would be at the end of that particular phase.

## Phase 1: Scaffolding our Application

We'll be putting together the overall master layout for the Todo List application. In this phase we will also be stubbing in all of the pages we'll need and hook up the Front-End routes needed to navigate to the different pages.

**Major Topics:** 
* Component Creation
* Component Props
* React Router

### Phase 1.1: Adding Layout Markup JSX

In Phase 1.1 we'll create the master layout that will established the major structure for our application. It will give us an opportunity to talk a little bit more about what JSX is because `create-react-app` sets up our build to accept JSX in our React Javascript code.

**Sample Repo Branch:**

* [Todo after Phase 1.1](https://github.com/myronschippers/todo-list-app/tree/feature-phase-1-1)

**Editing (files):**

* `App.js` - located at `./src/components/App/App.js`
* `App.css` - located at `./src/components/App/App.css`
* `index.html` - located at `./public/index.html`

We are going to use something called [JSX](https://reactjs.org/docs/introducing-jsx.html) to help us write some HTML elements in our Javascript. JSX is a syntax extension to Javascript and it produces React "element". You can think of it as a way to write HTML in our Javascript. It is extremely handy when using React.

**Example JSX:**

```JSX
const element = <h1>Hello, world!</h1>;
```

Open up `./src/components/App/App.js` so we can begin to flesh out our application elements. Lets start by removing all of the existing markup except the outer most `<div>` and then I can highlight some of what is going on here.

```JS
import React, { Component } from 'react';
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

First we'll need to add a class to our `index.html` file.

**Change from:**

```HTML
<div id="root"></div>
```

**to be:**

```HTML
<div id="root" class="scaffoldPrimer"></div>
```

Before we start adding the content to our `App.js` document I am going to give you some base styles that we'll be using for this first part. This is just so you don't have to worry about putting them in yourself and we can jump right into the React content. Make sure to copy these styles over to your `App.css` stylesheet replacing all of the styles that are already in there.

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

Use the below code block to make updates to your `App.js` file. All we're doing is setting up an HTML structure where we have places for the Header, Footer, and Page Body content for our application. Eventually the `App.js` component will become our master template.

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
                    PAGE BODY
                </div>
                <div className="scaffold-ft">
                    FOOTER
                </div>
            </div>
        );
    }
}
```

If you look in your browser window with the application running it should look something like this.

[Code Sample](https://github.com/myronschippers/todo-list-app/tree/feature-phase-1-1)
<img alt="Completing Phase 1.1" src="images/phase1.1-complete.png" />

### Phase 1.2: Header Markup and Styling

In **Phase 1.2** we're gonna update our application page content by creating header content that will include a logo, text (that tells us what the application is), and navigation. This concept of all of this content at the top of the page within a solid color block is referred to as an App Bar. We'll need to make edits to the files listed below.

**Sample Repo Branch:**

* [Todo after Phase 1.2](https://github.com/myronschippers/todo-list-app/tree/feature-phase-1-2)

**Editing (files):**

* `App.js` - located at `./src/components/App/App.js`
* `App.css` - located at `./src/components/App/App.css`

We'll start off by updating the `App.css` with the new styles in the below code snippet. Paste these styles in at the bottom of the `App.css` file in your Todo List application repository.

```CSS
/* ----------------------------------------------------------------------
App Bar
---------------------------------------------------------------------- */

.appBar {
    display: flex;
    flex-flow: row wrap;
    justify-content: space-between;
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

.primeHd {
    display: inline-block;
    margin: 0;
    padding: 0 4px;
    font-size: 1.4rem;
    vertical-align: middle;
}

.logoIcon {
    display: inline-block;
    width: 3.5rem;
    vertical-align: middle;
}

/* ----------------------------------------------------------------------
Navigation
---------------------------------------------------------------------- */

.nav {
    display: block;
    text-align: right;
}

.nav-list {
    display: flex;
    flex-flow: row nowrap;
    justify-content: flex-end;
    align-items: center;
    margin: 0;
    padding: 0;
    font-size: 0; /* fixes a spacing issue */
    list-style: none;
}

.nav-list > * {
    margin: 0;
    padding: 0;
    font-size: 1rem;
}

.nav-list > * + * {
    margin: 0 0 0 8px;
}

.navLink {
    display: block;
    padding: 12px 8px;
    box-sizing: border-box;
    border-bottom: 4px solid #8fc9f7;
    color: #8fc9f7;
    font-size: 1.2rem;
    font-weight: 700;
    line-height: 1.3;
    text-decoration: none;
    text-align: left;
}

.navLink:hover {
    border-color: #f0f8ff;
    color: #f0f8ff;
    text-decoration: none;
}

```

With our styling in place we can start editing our `App.js` content with the header markup. One of the things we'll make use of the React logo SVG that was given to us originally for our application logo. The logo gets imported using `import logo from './logo.svg';` at the top of our `App.js` document. When the logo is imported we store it in the `logo` variable so we can use it in our JSX later on. 

```JS
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';
```

In the below code snippet we see the entire App component code but all we're updating is the JSX for the markup displayed to the user in place of the `HEADER` text we hand in there as a placeholder before.

```JS
class App extends Component {
    render() {
        return (
            <div className="scaffold">
                <div className="scaffold-hd">
                    <header className="appBar">
                        <div className="appBar-identity">
                            <img src={logo} className="logoIcon" alt="logo" />
                            <h1 className="primeHd">Todo List</h1>
                        </div>
                        <div className="appBar-actions">
                            <nav className="nav">
                                <ul className="nav-list">
                                    <li>
                                        <a href="/Daily" className="navLink">Daily</a>
                                    </li>
                                    <li>
                                        <a href="/Categories" className="navLink">Categories</a>
                                    </li>
                                    <li>
                                        <a href="/Dashboard" className="navLink">Dashboard</a>
                                    </li>
                                </ul>
                            </nav>
                        </div>
                    </header>
                </div>
                <div className="scaffold-bd">
                    PAGE BODY
                </div>
                <div className="scaffold-ft">
                    FOOTER
                </div>
            </div>
        );
    }
}
```

Let's check our browser again to make sure there are no error and that our styles are showing up correctly for out new header content. It should look something like this.

[Code Sample](https://github.com/myronschippers/todo-list-app/tree/feature-phase-1-2)
<img alt="Application after completing Phase 1.2" src="images/phase1.2-complete.png" />

### Phase 1.3: Footer Markup and Styling

In **Phase 1.3** we're gonna update our application page content by creating footer content that will simply be a copyright statement that says, "© Todo List 2019". Our layout styling is already taking care of forcing our footer content to the bottom of the page but we'll also add som decorative styles to give it some visual presence.

**Sample Repo Branch:**

* [Todo after Phase 1.3](https://github.com/myronschippers/todo-list-app/tree/feature-phase-1-3)

**Editing (files):**

* `App.js` - located at `./src/components/App/App.js`
* `App.css` - located at `./src/components/App/App.css`

The below code snippet has all of the styling we'll use for the footer. Copy the code snippet and paste it to your `App.css` for your Todo List application.

```CSS
/* ----------------------------------------------------------------------
App Base
---------------------------------------------------------------------- */

.appBase {
    display: block;
    box-sizing: border-box;
    width: 100%;
    padding: 15px 20px 20px;
    background: #f8f8ff;
    font-size: 0.8rem;
    text-align: center;

    position: relative;
}

.appBase:before {
    content: " ";
    width: 70%;
    height: 1px;
    border-radius: 1px;
    background: #c0c0c0;

    /* CSS Centering */
    position: absolute;
    left: 50%;
    top: 0;
    transform: translate(-50%, 0);
}

```

With our styling in place let's update the footer content in the `App.js` JSX content. You can see the code updates in the snippet below. Please note that the header content has been replaced with `{/* ... HEADER JSX CODE (see Phase 1.2) ... */}` in the code snippet only to save space your file should have the actual content. We will see this several times throughout this tutorial.

```JS
class App extends Component {
    render() {
        return (
            <div className="scaffold">
                <div className="scaffold-hd">
                    {/* ... HEADER JSX CODE (see Phase 1.2) ... */}
                </div>
                <div className="scaffold-bd">
                    PAGE BODY
                </div>
                <div className="scaffold-ft">
                    <footer className="appBase">
                        &copy; Todo List 2019
                    </footer>
                </div>
            </div>
        );
    }
}
```

That's not a lot of content but if we look out our application in the browser that styling we implemented helps to give the footer content more visual presence.

[Code Sample](https://github.com/myronschippers/todo-list-app/tree/feature-phase-1-3)
<img alt="Application after completing Phase 1.3" src="phase1.3-complete.png" />

### Phase 1.4: Landing Page Content and Styling

In **Phase 1.4** we're gonna update our application **PAGE BODY** content by creating a splash image that takes up the entire body content area and has text with a button sitting on top of the splash image.

**Sample Repo Branch:**

* [Todo after Phase 1.4](https://github.com/myronschippers/todo-list-app/tree/feature-phase-1-4)

**Editing (files):**

* `App.js` - located at `./src/components/App/App.js`
* `App.css` - located at `./src/components/App/App.css`

**Adding (files):**

* `street-in-motion.jpg` - located at `./public/images/street-in-motion.jpg`

We are going to be using an image I pulled off of [Unsplash.com](https://unsplash.com/) for the hero/splash image on our home/landing page. Go into the `images` directory in this tutorial and copy the `street-in-motion.jpg` file over to the `./public/images` directory in your Todo List application.

Move `./images/street-in-motion.jpg` to your `./public/images/` directory.

Once again it's styling time. Copy the below code snippet to the bottom of the `App.css` file. The styling snippet is what will get our splash image to cover the entire content area and positions that splash text with button content overtop of the image.

```CSS
/* ----------------------------------------------------------------------
Splash
---------------------------------------------------------------------- */

.splash {
    width: 100%;
    height: 100%;
    box-sizing: border-box;
    padding: 20px;
    background: url("/images/street-in-motion.jpg");
    background-position: center bottom;
    background-size: cover;
    position: relative;
}

.splash:before {
    content: " ";
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    background: rgb(0, 0, 0, 0.4);
}

.splash-content {
    width: 400px;
    max-width: 70%;
    position: absolute;
    top: 50%;
    left: 10%;
    transform: translate(0, -100%);
    color: #ffffff;
}

.splash-content-hdg {
    margin: 0 0 30px;
    font-size: 2.3rem;
    font-weight: 400;
    color: #f0f8ff;
    text-shadow: 0px 1px 2px rgba(0, 0, 0, 0.3);
}

/* ----------------------------------------------------------------------
Button
---------------------------------------------------------------------- */

.btn {
    /* block */
    padding: 10px 14px;
    margin: 0;
    border-width: 0;
    border-bottom: 1px solid #20558a;
    /* decoration */
    border-radius: 3px;
    background: #1E90FF;
    box-shadow: 0px 2px 3px rgb(0, 0, 0, 0.2);
    /* font / text */
    line-height: 1.1;
    color: rgb(0,0,0,0.7);
    font-size: 1.1rem;
    font-weight: 800;
    text-shadow: 0px 1px 0px rgb(255, 255, 255, 0.2);
    cursor: pointer;
}

.btn_big {
    padding: 14px 18px;
    text-transform: uppercase;
    font-size: 1.4rem;
    font-weight: 800;
}

```

That's great but we need content for the styles to be effective so let's replace the **PAGE BODY** text in our `App.js` with the JSX content in the code snippet below.

```JS
class App extends Component {
    render() {
        return (
            <div className="scaffold">
                <div className="scaffold-hd">
                    {/* ... HEADER JSX CODE (see Phase 1.2) ... */}
                </div>
                <div className="scaffold-bd">
                    <div className="splash">
                        <div className="splash-content">
                            <h2 className="splash-content-hdg">Keep yourself organized</h2>
                            <button className="btn btn_big">Get Started</button>
                        </div>
                    </div>
                </div>
                <div className="scaffold-ft">
                    {/* ... FOOTER JSX CODE (see Phase 1.3) ... */}
                </div>
            </div>
        );
    }
}
```

We should now have what looks like a full application in our web browser. Unfortunately there is no content yet but we'll get there.

[Code Sample](https://github.com/myronschippers/todo-list-app/tree/feature-phase-1-4)
<img alt="Application after completing Phase 1.4" src="phase1.4-complete.png" />

### Phase 1.5: Componentize Hero for Landing Page

With all of the content in place for the master layout, header, footer, and landing page we can now talk about a key process in React. Most refer to it as componentizing. This is where we take the content we have in place and break it out into different components. You can choose to do this for a bunch of different reasons like reuse, maintenance, separation of concerns, and many others. For **Phase 1.5** we'll start by componentizing the splash image content for the page body that will eventually make up our Landing page.

**Sample Repo Branch:**

* [Todo after Phase 1.5](https://github.com/myronschippers/todo-list-app/tree/feature-phase-1-5)

**Editing (files):**

* `App.js` - `./src/components/App/App.js`
* `App.css` - `./src/components/App/App.css`

**Adding (files):**

* `SplashImg.js` - `./src/components/SplashImg/SplashImg.js`
* `splash.css` - `./src/components/SplashImg/splash.css`
* `Template.js` - `./src/components/Template/Template.js`

Let's examine our code and see what all makes up the page body content for the splash image used for the Landing page.

```JS
<div className="splash">
    <div className="splash-content">
        <h2 className="splash-content-hdg">Keep yourself organized</h2>
        <button className="btn btn_big">Get Started</button>
    </div>
</div>
```

For now let's simply extract this code into a new React component. Start by creating a new Javascript file for the component (`./src/components/SplashImg/SplashImg.js`).

```JS
import React, { Component } from 'react';

class SplashImg extends Component {
    render() {
        return (
            <div className="splash">
                <div className="splash-content">
                    <h2 className="splash-content-hdg">Keep yourself organized</h2>
                    <button className="btn btn_big">Get Started</button>
                </div>
            </div>
        );
    }
}

export default SplashImg;
```

Because this is such a specialized component let's extract the styles from `App.css` as well. The styling is actually comprised of both the `.splash` and `.btn` style modules. The button styling however might be something we might want to use in other places so let's leave that in `App.css` and just move the `.splash` styles into a new file at `./src/SplashImg/splash.css`.

`splash.css`:

```CSS
/* ----------------------------------------------------------------------
Splash
---------------------------------------------------------------------- */

.splash {
    width: 100%;
    height: 100%;
    box-sizing: border-box;
    padding: 20px;
    background: url("/images/street-in-motion.jpg");
    background-position: center bottom;
    background-size: cover;
    position: relative;
}

.splash:before {
    content: " ";
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    background: rgb(0, 0, 0, 0.4);
}

.splash-content {
    width: 400px;
    max-width: 70%;
    position: absolute;
    top: 50%;
    left: 10%;
    transform: translate(0, -100%);
    color: #ffffff;
}

.splash-content-hdg {
    margin: 0 0 30px;
    font-size: 2.3rem;
    font-weight: 400;
    color: #f0f8ff;
    text-shadow: 0px 1px 2px rgba(0, 0, 0, 0.3);
}
```

Import the `splash.css` into `SplashImg.js`:

```JS
import React, { Component } from 'react';
import './splash.css';
```

Take note that our splash styles got imported by simply using the path like so `import './splash.css';`. We saw this in `App.js` with the importing of `App.css`. The styles don't need to be used in a specific spot in our Javascript we just simply need to make sure our bundler is including it when a specific component is being used so we just need to import the file path. This will ensure our styles are being included.

With the new component all packaged up we can replace the content in the `App.js` body content area with the new SplashImg component.

Import our new component:

```JS
import React, { Component } from 'react';
import SplashImg from '../SplashImg/SplashImg';

import logo from './logo.svg';
import './App.css';
```

Replace the splash content with the newly imported component:

```JS
<SplashImg />
```

If we double check the browser at this point the site should look exactly the same as before. This is a straight forward way to simply separate out the splash image code and even potentially reuse it. How do we make it more flexible though? What if we wanted to change out the image being used in the background or the text that is overlaid on top of the image. This is where component **props** come in. This is a feature of React components that allow us to pass custom data to our components.

We'll start by making the heading and button class editable using props. These props get passed to the component by creating a custom attribute on the custom component element in our `App.js`.

```JS
    ...
</div>
<div className="scaffold-bd">
    <SplashImg hdgText="Keep yourself organized" btnText="Get Started" />
</div>
<div className="scaffold-ft">
    ...
```

These custom attributes can now be used inside of our component by calling to `this.props.hdgText` and `this.props.btnText`. The React `Component` that we are using as our base ensures that all of these custom attributes get attached to `this.props`. Let's try replacing the text content with these props.

```JS
class SplashImg extends Component {
    render() {
        return (
            <div className="splash">
                <div className="splash-content">
                    <h2 className="splash-content-hdg">{this.props.hdgText}</h2>
                    <button className="btn btn_big">{this.props.btnText}</button>
                </div>
            </div>
        );
    }
}
```

The page should look the same but let's try changing the value on our `btnText` prop to "Jump In" instead of "Get Started". We should see the text for the button on the rendered page get updated. Finally let's see how we can update the image being used in the background.

Add a new attribute for a background image prop (`bgImg`):

```JS
    ...
</div>
<div className="scaffold-bd">
    <SplashImg hdgText="Keep yourself organized" btnText="Get Started" bgImg="street-in-motion.jpg" />
</div>
<div className="scaffold-ft">
    ...
```

With this many attributes the element is getting a little long. We can break it up a little bit by putting each of the attributes on a separate line.

```JS
    ...
</div>
<div className="scaffold-bd">
    <SplashImg
        hdgText="Keep yourself organized"
        btnText="Get Started"
        bgImg="street-in-motion.jpg"
    />
</div>
<div className="scaffold-ft">
    ...
```

This will give us access to the image file name in the Javascript but we can't use that in our CSS directly so we'll need to leverage inline styles even though I loath inline styles. For this particular instance it's our best method.

```JS
class SplashImg extends Component {
    render() {
        const splashStyling = {
            backgroundImage: `background-image: url("/images/${this.props.bgImg}")`,
        };

        return (
            <div className="splash"
                style={splashStyling}
            >
                <div className="splash-content">
                    <h2 className="splash-content-hdg">{this.props.hdgText}</h2>
                    <button className="btn btn_big">{this.props.btnText}</button>
                </div>
            </div>
        );
    }
}
```

The implementation for a style attribute looks different from a normal attribute. Style attribute properties have to be implemented as an object. The style attribute won't accept a string value but only an object and you will see an error displayed on in the browser reflecting such. 


### Phase 1.6: Setup React Router and Create "Landing", "Daily", "Categories", & "Dashboard" Pages

With the page content componentized it will be easier to setup the various pages for our application. In **Phase 1.6** we'll be setting up the Front-End router for our application and stubbing in the pages that will eventually be needed in our Todo List application.

**Sample Repo Branch:**

* [Todo after Phase 1.6](https://github.com/myronschippers/todo-list-app/tree/feature-phase-1-6)

**Editing (files):**

* `App.js` - `./src/components/App/App.js`

**Adding (files):**

* `LandingPage.js` - `./src/components/LandingPage/LandingPage.js`
* `DailyListPage.js` - `./src/components/DailyPage/DailyPage.js`
* `CustomListsPage.js` - `./src/components/CustomListsPage/CustomListsPage.js`
* `CustomListDetailPage.js` - `./src/components/CustomListsPage/CustomListDetailPage.js`
* `DashboardPage.js` - `./src/components/DashboardPage/DashboardPage.js`

For our pages we need to start talking about the `react-router-dom` dependencies that we installed during the setup of our project. There are a few different components we'll need to make sure we have access to when we import the `react-router-dom` dependencies. 

```JS
import React, { Component } from 'react';
import SplashImg from '../SplashImg/SplashImg';
import {
    HashRouter as Router,
    Route,
    Link,
} from 'react-router-dom';
```

We will use the `<Router>` component to wrap the entire `App.js` content so that it is the outer most element. This will give us our shell for the router allowing us to load particular content up based on the hash in our URL route.

```JS
class App extends Component {
    render() {
        return (
            <Router>
                <div className="scaffold">
                    <div className="scaffold-hd">
                        {/* ... HEADER (see Phase 1.3) ... */}
                    </div>
                    <div className="scaffold-bd">
                        <SplashImg hdgText="Keep yourself organized" btnText="Get Started" />
                    </div>
                    <div className="scaffold-ft">
                        {/* ... FOOTER (see Phase 1.3) ... */}
                    </div>
                </div>
            </Router>
        );
    }
}
```

Now we need page that we can hook up to our router. We are going to create 5 files, one for each of our pages. They will each look very similar apart from their text content will be that of the individual pages name. Let's start with the landing page and then I will give you a list of the rest of the pages to do on your own. If you run up against some trouble take a look at the [Sample Code](https://github.com/myronschippers/todo-list-app/tree/feature-phase-1-6).

Create `LandingPage.js` component as a new file at `./src/components/LandingPage/LandingPage.js` with the following code:

```JS
import React, { Component } from 'react';

class LandingPage extends Component {
    render() {
        return (
            <div>
                LANDING PAGE
            </div>
        );
    }
}

export default LandingPage;
```

A couple of things to keep in mind with these class component declarations is that the name of the class will usually mirror the the name of the Javascript file. This helps with organization and to know that at a glance we're working with a class component (classes are named in uppercase camel case).

Repeat the steps that you just executed for creating the `LandingPage.js` for the othe four pages we're going to need in our `DailyTodosPage.js`, `CustomTodosPage.js`, `CustomTodosDetailPage.js`, and `DashboardPage.js`.

**Create all pages:**

1. `./src/components/DailyTodosPage/DailyTodosPage.js`
1. `./src/components/CustomTodosPage/CustomTodosPage.js`
1. `./src/components/CustomTodosDetailPage/CustomTodosDetailPage.js`
1. `./src/components/DashboardPage/DashboardPage.js`

CREATE THE PAGE COMPONENTS ON YOUR OWN...

At this point you should have all of your pages stubbed in as components but we're not using any of them in our application yet. We'll be addressing how to use these new components as Front-End routes. What is a Front-End route in our browser though? We are most used to seeing routes like `http://www.website.com/page` but if this website were leveraging a Front-End route for `/page` instead of the server we would use something called a hash route. A hash route is everything that comes after `/#` in your browser URL. Making the `/page` route into a Front-End route would look like `http://www.website.com/#/page`. How do we get react to leverage these hash routes? I'm glad you asked.

We will leverage the `Router`, `Route`, and `Link` components that were imported from the `react-router-dom` dependency. The `<Router>` component was already added to the application wrapping all of our content. As we place `<Route />` components in our `App.js` keep in mind that each of these represents a hash route that we want to use and tells us what content to load up for that particular route.

Let's make the home or landing page route. Add a `<Route />` component just above our `<SplashImg />` component.

```JS
    ...
</div>
<div className="scaffold-bd">
    <Route />
    <SplashImg hdgText="Keep yourself organized" btnText="Get Started" />
</div>
<div className="scaffold-ft">
    ...
```

`<Route />` accepts different props but we're only going to be concerned with `path` and `component` for now. The `path` prop is a string value that represents the hash route that we want our content to load up at. The `component` prop takes in the physical component that you have imported and represents that actual content you want to load at that particular hash route. Before updating these attributes make sure to import the `LandingPage.js` component. 

```JS
import {
    HashRouter as Router,
    Route,
    Link,
} from 'react-router-dom';
import LandingPage from '../LandingPage/LandingPage';
```

Add `path="/landing"` and `component={LandingPage}` to the `<Route />` component and we're going to remove the `<SplashImg />` component.

```JS
    ...
</div>
<div className="scaffold-bd">
    <Route path="/landing" component={LandingPage} />
</div>
<div className="scaffold-ft">
    ...
```

You will notice your browser has no body content anymore but if we navigate to `http://localhost:3000/#/landing` in your URL you will see the "LANDING PAGE" text that we entered in on our stubbed in component. YAY, we made a new page!!! With the page in place we can update the `path` so that `LandingPage.js` will load up as our home/landing page.

```JS
    ...
</div>
<div className="scaffold-bd">
    <Route path="/" component={LandingPage} />
</div>
<div className="scaffold-ft">
    ...
```

But we really want our `<SplashImg />` component to show up so let's go over to our `LandingPage.js` and replace the "**LANDING PAGE**" text with our `<SplashImg />` component. 

**in `./src/components/LandingPage/LandingPage.js`:**

```JS
import React, { Component } from 'react';
import SplashImg from '../SplashImg/SplashImg';

class LandingPage extends Component {
    render() {
        return (
            <SplashImg hdgText="Keep yourself organized" btnText="Get Started" />
        );
    }
}

export default LandingPage;
```

That's great no our splash image shows up and our home page is all set. How about we add another page to our application. Import your `DailyTodosPage.js` into `App.js` first so we can make our Daily todos route.

```JS
import React, { Component } from 'react';
import {
    HashRouter as Router,
    Route,
    Link,
} from 'react-router-dom';
import LandingPage from '../LandingPage/LandingPage';
import DailyTodosPage from '../DailyTodosPage/DailyTodosPage';
```

With our page component imported go ahead and add the new `<Route />` for Daily todos.

```JS
    ...
</div>
<div className="scaffold-bd">
    <Route path="/" component={LandingPage} />

    <Route path="/daily-todos" component={DailyTodosPage} />
</div>
<div className="scaffold-ft">
    ...
```

With that in place let's go ahead and test our new page by navigating to `http://localhost:3000/#/daily-todos`.

### Phase 1.7: Componentize Application Header

In **Phase 1.7** 

**Sample Repo Branch:**

* [Todo after Phase 1.7](https://github.com/myronschippers/todo-list-app/tree/feature-phase-1-7)

**Editing (files):**

* fileName - filePath

**Adding (files):**

* fileName - filePath

### Phase 1.8: Componentize Application Footer

Short Description

**Sample Repo Branch:**

* [Todo after Phase 1.8](https://github.com/myronschippers/todo-list-app/tree/feature-phase-1-8)

**Editing (files):**

* fileName - filePath

**Adding (files):**

* fileName - filePath

## Phase 2: Creating Daily Todo List

## Phase 3: Creating Custom Todo Lists

## Phase 4: Creating Dashboard
