<template>
  <!-- <NavigationMenu /> -->
  <ContactForm />
</template>

<script>
import axios from 'axios'
import VueAxios from 'vue-axios'
// import NavigationMenu from './components/NavigationMenu.vue'
import ContactForm from './components/ContactForm.vue'

export default {
  name: 'App',
  components: {
    // NavigationMenu,
    ContactForm
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
