<template>
  <NavigationMenu :showMobile="showMobile"/>
  <!-- <ContactForm /> -->
</template>

<script>
import NavigationMenu from './components/NavigationMenu.vue'
//import ContactForm from './components/ContactForm.vue'

export default {
  name: 'App',
  components: {
    NavigationMenu,
    ///ContactForm
  },
  data() {
      return {
          windowWidth: window.innerWidth
      }
  },
  mounted() {
      window.onresize = () => {
          this.windowWidth = window.innerWidth
      }
  },
  computed: {
    showMobile() {
      return this.windowWidth < 1200
    }
  }
}
</script>

<style>
#app {
  font-family: 'Montserrat', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
