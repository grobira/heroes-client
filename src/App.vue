<template>
  <div id="app">
    <header>
        <img src="./assets/hero-icon.png"/>
    </header>
    <Hero/>
  </div>
</template>

<script>
import Hero from './components/Hero.vue'
import Vue from 'vue'
import BootstrapVue from 'bootstrap-vue'
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

Vue.use(BootstrapVue);

export default {
  name: 'app',
  components: {
    Hero
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 600px;;
}

header {
    background-color: #35441c;
    height: 60px;
    left: 15%;
}


img {
    width: 50px;
    height: 60px;
    position: fixed;
    left: 11%;
}
</style>
