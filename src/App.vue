<template>
  <NavigationMenu :showMobile="showMobile"/>
  <CarouselShow :showMobile="showMobile" />
  <MainContent :showMobile="showMobile" />
  <MapAndContact :showMobile="showMobile" />
  <FooterComponent :showMobile="showMobile" />
</template>

<script>
import NavigationMenu from './components/NavigationMenu.vue'
import CarouselShow from './components/CarouselShow.vue'
import MainContent from './components/MainContent.vue'
import MapAndContact from './components/MapAndContact.vue'
import FooterComponent from './components/FooterComponent.vue'

export default {
  name: 'App',
  components: {
    NavigationMenu,
    CarouselShow,
    MainContent,
    MapAndContact,
    FooterComponent
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
  color: #000000;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
