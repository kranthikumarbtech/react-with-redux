This project was bootstrapped with [Create React App](https://github.com/facebookincubator/create-react-app).

## Folder Structure

The project should look like this:

```
my-app/
  README.md
  node_modules/
  package.json
  public/
    index.html
    favicon.ico
  src/
    App.css
    App.js
    App.test.js
    containers/
      about/
        index.js
      app/
        index.js
      home/
        index.js
    index.css
    index.js
    logo.svg
    modules/
      counter.js
      index.js
    store.js
```

For the project to build, **these files must exist with exact filenames**:

* `public/index.html` is the page template;
* `src/index.js` is the JavaScript entry point.

You can delete or rename the other files.

You may create subdirectories inside `src`. For faster rebuilds, only files inside `src` are processed by Webpack.<br>
You need to **put any JS and CSS files inside `src`**, otherwise Webpack won’t see them.

Only files inside `public` can be used from `public/index.html`.


## Available Scripts

In the project directory, you can run:

### `npm start` 
or
###  `yarn start`

Runs the app in the development mode.<br>
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.<br>
You will also see any lint errors in the console.

### `npm test`
or
###  `yarn test`

Launches the test runner in the interactive watch mode.<br>
See the section about [running tests](#running-tests) for more information.

### `npm run build`
or
###  `yarn build`

Builds the app for production to the `build` folder.<br>
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.<br>
Your app is ready to be deployed!

## Installing a Dependency

The generated project includes React and ReactDOM as dependencies.
To install additional dependencies for routing need to include Redux, React Router & Redux Thunk

```sh
yarn add redux react-redux react-router-dom react-router-redux@next redux-thunk history redux-devtools-extension
```

## Step one: Create Store.

Everything in Redux belong in a single store.
Let's configure a `store` to understand `react-router` and `redux-thunk`.
Within a `store`, we're importing a few core modules from Redux that allows to create a custom global store.
`react-router-redux` and `redux-thunk` are both known as middleware to Redux and we need to configure our store to treat them that way.
Call rootReducer,this is essential to Redux.
Create a file called './src/modules/index.js', so it can satisfy a Store.

The `store` const creates a store using the Redux `createStore` function. It accepts a `rootReducer`, initialState.

The `history` const syncs our `browserHistory` with a `store` and must be exported so we can use it within a routes later.

Export a `store` const as the default module so that it can also be used later.
./src/store.js

## Step two: Create Routes.

This app uses React Router v4 which allows to mount components anywhere inside a application when a given URL matches to defined parameters.
In previous versions of React Router we might see files like `routes.js` which contain a long list of nested routes but React Router v4 does routing a little differently.
The router history is managed inside a Redux store and is passed down via called `ConnecteRouter`.

## Step three: Containers.

 Create a `App` component that renders navigation and any matching routes inside a main tag.
 ./src/containers/app/index.js
 <br>
 Create a `Home` component that we defined to show at the exact path of /.
 This is straight forward for those who have used Redux before but here a special in this App we can import `push` from `react-router` and use within a action creator.
 Since a Store knows about `react-router-redux` it can manage and act on routing actions.
 ./src/containers/home/index.js
 <br>
 Create a `About` component that wiil allow to show About Us page.
 ./src/containers/about/index.js

## Step four: Rendering a App.

 This is to mount a application.
 We need to tell `react-dom` to render a appllication with the correct store and browser history data. This can be done by using the `ConnectedRouter` export given by React router v4. `ConnectedRouter` has access to the `store` given to `Provider` so we need not to warry about passing data through ant additional props.
 ./src/index.js

## Step five: Adding Redux thunk.

 `Redux Thunk` is middleware for Redux that allows you to write action creators that return a function instead of an action.
 The `incrementAsync` and `decrementAsync` functions return a Thunk. First dispatch an action and wrap another function within `setTimeout()` which dispatches when the timer is up.
 ./src/modules/counter.js
 <br>
 We’ll need to hook up our `counter.js` to our `rootReducer` so our store can manage our state.
 ./src/modules/index.js
 