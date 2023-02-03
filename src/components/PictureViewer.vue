<template>
  <div class="pictureViewer">
    <div class="pictureViewer__main">
      <img v-if="selected === 1" src="/images/image-product-1.jpg" alt="">
      <img v-if="selected === 2" src="/images/image-product-2.jpg" alt="">
      <img v-if="selected === 3" src="/images/image-product-3.jpg" alt="">
      <img v-if="selected === 4" src="/images/image-product-4.jpg" alt="">
    </div>
    <div class="pictureViewer__alts">
      <img class="pictureViewer__altsImage" :class="{ 'pictureViewer__altsImage--selected': selected === 1 }" src="/images/image-product-1-thumbnail.jpg" alt="" @click="selectOne">
      <img class="pictureViewer__altsImage" :class="{ 'pictureViewer__altsImage--selected': selected === 2 }" src="/images/image-product-2-thumbnail.jpg" alt="" @click="selectTwo">
      <img class="pictureViewer__altsImage" :class="{ 'pictureViewer__altsImage--selected': selected === 3 }" src="/images/image-product-3-thumbnail.jpg" alt="" @click="selectThree">
      <img class="pictureViewer__altsImage" :class="{ 'pictureViewer__altsImage--selected': selected === 4 }" src="/images/image-product-4-thumbnail.jpg" alt="" @click="selectFour">
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selected: 1
    }
  },
  methods: {
    selectOne() {
      this.selected = 1
    },
    selectTwo() {
      this.selected = 2
    },
    selectThree() {
      this.selected = 3
    },
    selectFour() {
      this.selected = 4
    }
  }
}
</script>

<style lang="scss" scoped>
.pictureViewer {
  display: flex;
  flex-direction: column;
  width: 40%;
  gap: 30px;

  .pictureViewer__main {
    img {
      border-radius: 15px;
    }
  }

  .pictureViewer__alts {
    display: flex;
    justify-content: space-between;

    .pictureViewer__altsImage {
      width: 20%;
      border-radius: 15px;

      &.pictureViewer__altsImage--selected {
        opacity: 0.5;
        outline: 2px solid #FF7E1B;
      }
    }
  }
}
</style>