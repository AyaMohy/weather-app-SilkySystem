<template>
  <div class="full-width row g-header justify-center items-center">
    <div
      class="g-header__center col-12 row text-center q-ma-auto animation-slide-bottom"
    >
      <!-- <div class="col row text-center q-ma-auto"> -->
      <div class="col-12">
        <img
          :style="{ width: '100px', height: '100.64px' }"
          src="Group 1171274739.png"
        />
      </div>
      <div class="col-12 g-header__center--h1 q-pa-md">Weather Climate</div>
      <!-- </div> -->
    </div>
    <div class="g-header__left-img larg-screen-only">
      <img src="Group.png" />
    </div>
    <div class="g-header__right-img larg-screen-only">
      <!-- <img :src="imgRight" /> -->
    </div>
  </div>
</template>

<script>
export default {
  props: {
    imgRight: {
      type: String,
      default: "",
    },
  },
  components: {},
};
</script>

<style lang="scss" scoped>
.g-header {
  position: relative;
  height: 360px;
  background: linear-gradient(
    180deg,
    rgba(255, 255, 255, 0.3) 0%,
    rgba(57, 147, 73, 0.3) 100%
  );
  &__center {
    img {
      width: 100px;
      height: 75.64px;
    }
    &--h1 {
      font-style: normal;
      font-weight: 600;
      font-size: 32px;
      line-height: 24px;
    }
    @media (min-width: $breakpoint-sm-min) {
      font-size: 16px;
    }
  }
  &__right-img {
    img {
      position: absolute;
      right: 30px;
      width: 101px;
      height: 56.1px;
      bottom: -30px;
    }
  }
  &__left-img {
    img {
      position: absolute;
      left: 30px;
      width: 150px;
      height: 150px;
      bottom: -30px;
    }
  }
}

</style>
