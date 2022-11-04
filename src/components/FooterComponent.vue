<template>
  <div class="footer-container" :class="showMobile ? 'footer-container-mobile' : 'footer-container-desktop'">
    <div>© The standard Copywrite 2020</div>
    <img :class="showMobile ? 'mobile-logo' : 'desktop-logo'" src="../assets/Group-1198.svg">
  </div>
</template>

<script>

export default {
  name: 'FooterComponent',
  props: {
    showMobile: Boolean,
  },
}
</script>

<style scoped>

.footer-container {
  /* position: absolute; */
  bottom: 0;
  background-color: #000000;
  width: calc(100% - 144px);
  color: #FFFFFF;
  font-size: 16px;
  height: 48px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 72px;
}

.footer-container-mobile {
  width: calc(100% - 48px);
  font-size: 12px;
  height: 40px;
  padding: 0 24px;
}


.desktop-logo {
  height: 32px;
}

.mobile-logo {
  height: 24px;
  width: 24px;
}
</style>