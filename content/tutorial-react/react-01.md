# Tutorial 01 - Getting Started

Welcome to the first exercise in the **React Track** of this Apollo Client Tutorial! If you prefer React Native or Angular 2 over React, head over to the respective tutorial track.

## Goal

The **goal** of this first exercise is to install a React App and run it afterwards. You will get familiar with the infrastructure surrounding Apollo Client for React and with the App structure of the Pokedex.

We will see a generic greeting in our pokedex at the end of this exercise:
![](../images/react-exercise-01-pokedex.png)

## Introduction

If you signed up with GitHub, should have received your own `pokedex-react`. Alternatively, clone the [repository from GitHub](https://github.com/learnapollo/pokedex-react).

<!-- __DOWNLOAD_REACT__ -->

Now change to the first exercise, install the dependencies and start the app from your console

```sh
cd pokedex-react/exercise-01
yarn install # or npm install
yarn start # or npm start
```

## Getting Familiar with the App

Let's take a moment to get more familiar with the structure of the app before we run it.

The starting point for our App is `src/index.js` At the moment, all that happens here is setting up the router to render the `Pokedex` component for the `/` route path:

```js
ReactDOM.render((
  <Router history={browserHistory}>
    <Route path='/' component={Pokedex} />
  </Router>
  ),
  document.getElementById('root')
)
```

## Adding Apollo Client to the App

Let's see how we can add Apollo Client to our App together by adding these changes to `src/index.js`.

### Package Dependencies

Open `src/package.json` to have a look what packages we are using.

* `apollo-client` - the core package exposes the vanilla JS Apollo Client which provides the core functionality
* `react-apollo` - the React integration exposes the `ApolloProvider` that can be used to wrap other React components, allowing them to send queries and mutations

Now go ahead and import the following things at the top of `src/index.js`:

```js
import ApolloClient, { createNetworkInterface } from 'apollo-client'
import { ApolloProvider } from 'react-apollo'
```

### Configuring Apollo Client with our GraphQL server

Now we can connect Apollo Client with our GraphQL server in `src/index.js` by configuring the network layer

```js
const client = new ApolloClient({
  networkInterface: createNetworkInterface({ uri: 'https://api.graph.cool/simple/v1/__PROJECT_ID__'}),
})
```

If you signed up with GitHub and downloaded the example, we already inserted your individual GraphQL endpoint.

### Connecting Apollo Client to our React Components

To allow our React components to issue GraphQL queries and mutations through the client we wrap them with the `ApolloProvider` component in `src/index.js `from the `react-apollo` package.

```js
ReactDOM.render((
  <ApolloProvider client={client}>
    <Router history={browserHistory}>
      <Route path='/' component={Pokedex} />
    </Router>
  </ApolloProvider>
  ),
  document.getElementById('root')
)
```

As we are using `react-router` to handle our routes, we wrap the `Router` component. Note that the `/` route points to the `Pokedex` component.

> Note: You don't have to put `ApolloProvider` on the highest level of the component hierarchy - however, every component that wants to use Apollo Client needs to be a direct or indirect child of `ApolloProvider` in the component hierarchy.

Our Pokedex component lives in `'src/components/Pokedex.js'`. Currently, it only contains a generic greeting, but that will change soon! We will further expand this component in the following exercises to give an overview about all the pokemon in your Pokedex as well as the possibility to add new pokemons or update existing ones. But for now, let's make sure you are ready to go.

## Starting the App

To confirm your environment is all correctly setup, open [http://localhost:3000](http://localhost:3000) in your browser and you should see the greeting from the Pokedex component.

## Recap

Great, you did it! You successfully ran the React App and got familiar with its general structure. Let's quickly summarize what we learned so far:

* To use **Apollo Client**, we need to import it from `apollo-client` and setup its **networkInterface**
* We can **issue queries and mutations** in our React components by wrapping them in the **Apollo Provider** found in `react-apollo`
* We will use the **Pokedex component** to list our pokemons and to offer other features