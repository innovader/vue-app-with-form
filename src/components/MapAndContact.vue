<template>
  <div class="map-and-contact-container" :class="showMobile ? 'mobile-container' : ''">
    <img v-if="!showMobile" class="map-image" src="../assets/Image-2.png">
    <ContactForm :showMobile="showMobile" />
    <img v-if="showMobile" class="map-image-mobile" src="../assets/Image-2@2x.png">
  </div>
</template>

<script>
import ContactForm from './ContactForm.vue'

export default {
  name: 'MapAndContact',
  components: {
    ContactForm
  },
  props: {
    showMobile: Boolean,
  },
}
</script>

<style scoped>
.map-and-contact-container {
  display: flex;
}

.map-image {
  max-width: 45%;
}

.map-image-mobile {
  height: 360px;
}

.mobile-container {
  display: flex;
  flex-direction: column;
}
</style>