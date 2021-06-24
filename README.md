# Nhost Vue Apollo

## Installation

To install simply run `npm install --save nhost-vue-apollo`

## Usage

### Vue.js v3

We will use the Composition Api to set up Apollo in Vue 3.

#### Dependencies ####

```bash
npm install --force @vue/apollo-composable
npm install graphql-tag
```

#### Setup ####

In main.js, set up your Vue app as follows:

```vue
import { createApp, provide, h } from 'vue'
import { DefaultApolloClient } from '@vue/apollo-composable'
import gql from "graphql-tag";
import { generateNhostApolloClient } from "nhost-vue-apollo"
import App from "./App.vue";

const nhostClient = generateNhostApolloClient({ gqlEndpoint: "https://hasura-YOUR_HASURA_ENDPOINT.nhost.app/v1/graphql"}).client;

createApp({
  setup() {
    provide(DefaultApolloClient, nhostClient)
  },
  render() {
    return h(App)
  }
}).mount("#app");
```

Now, you can use Apollo throughout your app according to the [Vue-Apollo Composition API](https://v4.apollo.vuejs.org/guide-composable/).

Also, check out the [Vue.js v3 example app](https://google.com).

### Vue.js v2

#### Dependencies ####

```bash
npm install vue-apollo
npm install graphql-tag
```

#### Setup ####

In main.js, set up your Vue app as follows:

```vue
import Vue from 'vue'
import App from './App.vue'
import { generateNhostApolloClient } from "nhost-vue-apollo"
import VueApollo from "vue-apollo"

Vue.use(VueApollo)

const nhostClient = generateNhostApolloClient({ gqlEndpoint: "https://hasura-YOUR_HASURA_ENDPOINT.nhost.app/v1/graphql"}).client;

const apolloProvider = new VueApollo({
  defaultClient: nhostClient
})

new Vue({
  apolloProvider,
  render: h => h(App),
}).$mount('#app')
```

Now, you can use Apollo throughout your app according to the [Vue-Apollo Standard API](https://apollo.vuejs.org/guide/).