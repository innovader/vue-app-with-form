<template>
  <div :class="showMobile ? 'slide-one-mobile' : 'slide-one'">
    <div :class="showMobile ? 'image-text-mobile' : 'image-text'">
      <div :class="showMobile? 'heading-mobile' : 'heading'">S.und Co</div>
      <div :class="showMobile ? 'decorative-line-mobile' : 'decorative-line'"></div>
      <p :class="showMobile ? 'description-mobile' : 'description'">
        To take a trivial example, which of us ever undertakes laborious physical exercise, except to obtain some advantage from it?
      </p>
    </div>
  </div>
</template>

<script>

export default {
  name: 'CarouselShow',
  props: {
    showMobile: Boolean,
  },
}
</script>

<style>
.slide-one {
  width: 100%;
  height: calc(100vh - 64px);
  background-image: url('../assets/1858113@2x.png');
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
}

.image-text{
  color: white;
  width: 576px;
  height: 375px;
  position: relative;
  left: 252px;
  padding-top: 384px;
  
}

.heading {
  font-size: 100px;
  font-weight: 800;
}

.decorative-line {
  width: 96px;
  height: 16px;
  background-color: #b4ff00;
}

.description {
  font-size: 30px;
  font-weight: 800;
}

.slide-one-mobile {
  width: 100%;
  height: 356px;
  background-image: url('../assets/1858113.png');
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
} 

.image-text-mobile{
  color: white;
  padding: 73px 24px 0 24px;
}

.heading-mobile {
  font-size: 38px;
  font-weight: 800;
}

.decorative-line-mobile {
  width: 48px;
  height: 8px;
  background-color: #b4ff00;
}

.description-mobile {
  font-size: 18px;
  font-weight: 800;
  margin-top: 42px;
}
</style>