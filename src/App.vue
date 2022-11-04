<template>
  <NavigationMenu :showMobile="showMobile"/>
  <CarouselShow :showMobile="showMobile"/>
  <!-- <ContactForm /> -->
</template>

<script>
import NavigationMenu from './components/NavigationMenu.vue'
import CarouselShow from './components/CarouselShow.vue'
// import ContactForm from './components/ContactForm.vue'

export default {
  name: 'App',
  components: {
    NavigationMenu,
    CarouselShow,
    // ContactForm
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
  color: blue;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
