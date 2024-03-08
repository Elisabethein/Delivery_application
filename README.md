# Delivery_application

This is a front-end project written in Vue.js. The project uses Vite as a build tool.
It is the front-end part of the Delivery API project. The API is written in Java and can be found in the following repository: [Delivery API](https://github.com/Elisabethein/Delivery-API)

The application is a simple web interface for the API. The user can choose a city and vehicle to get the delivery fee.

The design elements are taken from the following websites:
* Photo by <a href="https://unsplash.com/@alexanderstartsev?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Alexander Startsev</a> on <a href="https://unsplash.com/photos/two-burger-with-lettuce-and-tomato-ndNw_6QGR_c?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Unsplash</a>
* Photo by <a href="https://unsplash.com/@debsrainford?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Deborah Rainford</a> on <a href="https://unsplash.com/photos/brown-and-green-vegetable-salad-on-brown-paper-bag-zOlZgELBMRg?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Unsplash</a>
* Photo by <a href="https://unsplash.com/@jonathanborba?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Jonathan Borba</a> on <a href="https://unsplash.com/photos/full-filled-cream-glass-on-table-7TeR1A1MUpM?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Unsplash</a>
* Icons by <a target="_blank" href="https://icons8.com">Icons8</a>


## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur) + [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin).

## Customize configuration

See [Vite Configuration Reference](https://vitejs.dev/config/).

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

### Run Headed Component Tests with [Cypress Component Testing](https://on.cypress.io/component)

```sh
npm run test:unit:dev # or `npm run test:unit` for headless testing
```

### Run End-to-End Tests with [Cypress](https://www.cypress.io/)

```sh
npm run test:e2e:dev
```

This runs the end-to-end tests against the Vite development server.
It is much faster than the production build.

But it's still recommended to test the production build with `test:e2e` before deploying (e.g. in CI environments):

```sh
npm run build
npm run test:e2e
```


