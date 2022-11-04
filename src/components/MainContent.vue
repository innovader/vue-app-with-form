<template>
  <div class="main-content-container">

    <div :class="showMobile ? 'first-row mobile-row' : 'first-row'">
      <img v-if="showMobile" class="first-image-mobile" src="../assets/6cfa2f3aca711cdcdb097435682f9555-510x638.png">
      <img v-if="!showMobile" class="first-image" src="../assets/6cfa2f3aca711cdcdb097435682f9555-510x638@2x.png">
      <div :class="showMobile ? 'text-container-mobile' : 'text-container'">
        <div :class="showMobile ? 'above-heading-mobile' : 'above-heading'">Since the 1500s</div>
        <div :class="showMobile? 'heading-mobile' : 'heading'">The standard</div>
        <p :class="showMobile ? 'description-mobile' : 'description'">
          Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt.
        </p>
      </div>
    </div>

    <div :class="showMobile ? 'second-row mobile-row' : 'second-row'">
      <img v-if="showMobile" class="second-image-mobile" src="../assets/pop-art-love-cushion-46x46cm-848344.png">
      <div :class="showMobile ? 'text-container-mobile' : 'text-container'" class="second-text-container">
        <div :class="showMobile ? 'above-heading-mobile' : 'above-heading'">Since the 1500s</div>
        <div :class="showMobile? 'heading-mobile' : 'heading'">The standard</div>
        <p :class="showMobile ? 'description-mobile' : 'description'">
          Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
        </p>
      </div>
      <img v-if="!showMobile" class="second-image" src="../assets/pop-art-love-cushion-46x46cm-848344@2x.png">
    </div>

  </div>
</template>

<script>

export default {
  name: 'MainContent',
  props: {
    showMobile: Boolean,
  },
}
</script>

<style scoped>
.main-content-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  padding-bottom: 129px;
}

.first-row {
  width: 1200px;
  display: flex;
  justify-content: space-between;
  padding-top: 144px;
}

.first-image {
  width: 696px;
}

.text-container {
  width: 456px;
}

.above-heading {
  font-size: 16px;
  font-weight: bold;
  color: #CFCFCF;
  padding-top: 24px;
  padding-bottom: 8px;
}

.heading {
  font-size: 32px;
  font-weight: 800;
}

.description {
  font-size: 18px;
}

.second-row {
  width: 1200px;
  display: flex;
  justify-content: space-between;
  padding-top: 96px;
  padding-bottom: 87px;
}

.second-text-container {
  margin-left: 240px;
}

.second-image {
  width: 424px;
}

.mobile-row {
  width: 312px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  padding-top: 32px;
  padding-bottom: 0;
}

.first-image-mobile {
  width: 312px;
}

.above-heading-mobile {
  font-size: 11px;
  font-weight: bold;
  color: #CFCFCF;
  padding-top: 32px;
}

.heading-mobile {
  font-size: 28px;
  font-weight: 800;
}

.description-mobile {
  font-size: 18px;
}
.second-image-mobile {
  width: 289px;
}

.text-container-mobile{
  margin-left: 0;
}
</style>
