# vuex-playlist

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```


```
# Vuex Tutorial
IN your main.js
Make sure you import the store and register it

import Vue from 'vue'
import App from './App.vue'
import { store } from './store/store';  --> Here

new Vue({
  el: '#app',
  store: store, --> Here
  render: h => h(App)
})


# 1. Create  Folder Called Store
# 2. Create a File Called Store.js

# In the store.js input the following file

  
import Vue from 'vue';
import Vuex from 'vuex';

Vue.use(Vuex);

export const store = new Vuex.Store({
    strict: true,
    state: {
        products: [
            {name: 'Banana Skin', price: 20},
            {name: 'Shiny Star', price: 40},
            {name: 'Green Shells', price: 60},
            {name: 'Red Shells', price: 80}
        ]
    },
    getters: {
        saleProducts: (state) => {
            var saleProducts = state.products.map( product => {
                return {
                    name:  '**' + product.name + '**',
                    price: product.price / 2,
                };
            });
            return saleProducts;
        }
    },

...

# In your component, have something like this

<template>
    <div id="product-list-two">
        <h2>Product List Two</h2>
        <ul>
            <li v-for="product in saleProducts">
                <span class="name">{{ product.name }}</span>
                <span class="price">£{{ product.price }}</span>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    computed: {
        products(){
            return this.$store.state.products;
        },
        saleProducts(){
            return this.$store.getters.saleProducts;
        }
    }
}
</script>

# You can also use a spread operator

<script>
import {mapActions} from 'vuex';
import {mapGetters} from 'vuex';
export default {
    computed: {
        products(){
            return this.$store.state.products;
        },
        ...mapGetters([
            'saleProducts'
        ])
    },
    methods: {
        ...mapActions([
            'reducePrice'
        ])
    }
}
</script>

```

For detailed explanation on how things work, consult the [docs for vue-loader](http://vuejs.github.io/vue-loader).
