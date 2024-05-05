# zadacha4

Первым шагом установим Vuex через npm:

npm install vuex --save



Создайте файл store.js, в котором будет находиться ваше хранилище Vuex:

import Vue from 'vue';
import Vuex from 'vuex';

Vue.use(Vuex);

export default new Vuex.Store({
  state: {
    count: 0
  },
  mutations: {
    increment(state) {
      state.count++;
    },
    decrement(state) {
      state.count--;
    }
  },
  actions: {
    increment(context) {
      context.commit('increment');
    },
    decrement(context) {
      context.commit('decrement');
    }
  },
  getters: {
    getCount: state => {
      return state.count;
    }
  }
});



Импортируйте ваше хранилище Vuex в файл main.js и добавьте его к экземпляру Vue:

import Vue from 'vue';
import App from './App.vue';
import store from './store';

new Vue({
  el: '#app',
  store,
  render: h => h(App)
});



Теперь добавьте кнопки в ваш компонент App.vue, которые будут увеличивать и уменьшать счетчик в хранилище Vuex:

<template>
  <div>
    <h1>{{ count }}</h1>
    <button @click="increment">Increment</button>
    <button @click="decrement">Decrement</button>
  </div>
</template>

<script>
export default {
  computed: {
    count() {
      return this.$store.getters.getCount;
    }
  },
  methods: {
    increment() {
      this.$store.dispatch('increment');
    },
    decrement() {
      this.$store.dispatch('decrement');
    }
  }
};
</script>
