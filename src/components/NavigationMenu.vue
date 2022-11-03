<template>
  <!-- Desktop Header -->
  <div v-if="!showMobile" class="header-container desktop">
    <img class="desktop-logo" src="../assets/Group-1198.svg">
    <ul class="navigation">
      <li
          v-for="(item, index) in items"
          :key="index"
          v-text="item.title"
          class="navigation-item"
        >
      </li>
    </ul>
  </div>

  <!-- Mobile header -->
  <div v-if="showMobile && !isMobileMenuShowing" class="header-container">

    <img class="mobile-logo" src="../assets/Group-1198.svg">

    <img
      class="menu-icon"
      src="../assets/Group-1154.svg"
      @click="toggleMobileMenu"
    >
  </div>

  <!-- Mobile menu -->
  <div v-if="showMobile && isMobileMenuShowing" class="mobile-menu">
    <div class="mobile-menu-title">
      <span>MENU</span>
      <img
        class="close-menu-icon"
        src="../assets/Group-1156.svg"
        @click="toggleMobileMenu"
      >
    </div>
    <ul>
      <li
          v-for="(item, index) in items"
          :key="index"
          v-text="item.title"
        >
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'NavigationMenu',
  props: {
    showMobile: Boolean,
  },
  data() {
    return {
      isMobileMenuShowing: true,
      items: [
        { title: 'Main Page' },
        { title: 'Page Two' },
        { title: 'Page Three' },
        { title: 'About Us' },
        { title: 'Our Work' },
        { title: 'Contact' },
      ],
    }
  },
  methods: {
    toggleMobileMenu() {
      this.isMobileMenuShowing = !this.isMobileMenuShowing
    },
  }
}
</script>

<style scoped>
.header-container {
  background-color: #000000;
  color: #FFFFFF;
  height: 56px;
  padding: 0px 25px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.desktop-logo {
  height: 72px;
  position: absolute;
  top: 20px;
  left: 47px;
}

.desktop {
  justify-content: center;
}

.navigation {
  color: #FFFFFF;
  font-weight: 800;
  font-size: 18px;
  display: flex;
}

.navigation-item {
  margin-right: 50px;
}

.mobile-logo {
  height: 40px;
}

.mobile-menu {
  font-weight: 800;
  font-size: 38px;
  line-height: 68px;
}

.mobile-menu-title {
  background-color: #000000;
  color: #FFFFFF;
  height: 56px;
  padding: 0px 25px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.close-menu-icon {
  position: absolute;
  right: 0;
  padding-right: 25px;
}

ul {
  list-style: none;
  padding-left: 0;
  color: #000000;
}

</style>
