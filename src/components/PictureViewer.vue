<template>
  <div class="pictureViewer">
    <div class="pictureViewer__main" @click="showPlayer = !showPlayer">
      <img v-if="selected === 1" src="/images/image-product-1.jpg" alt="">
      <img v-if="selected === 2" src="/images/image-product-2.jpg" alt="">
      <img v-if="selected === 3" src="/images/image-product-3.jpg" alt="">
      <img v-if="selected === 4" src="/images/image-product-4.jpg" alt="">
    </div>
    <div class="pictureViewer__arrows--mobile">
      <span class="pictureViewer__arrows--left" @click="selectPrevious"></span>
      <span class="pictureViewer__arrows--right" @click="selectNext"></span>
    </div>
    <div class="pictureViewer__alts">
      <img class="pictureViewer__altsImage" :class="{ 'pictureViewer__altsImage--selected': selected === 1 }"
           src="/images/image-product-1-thumbnail.jpg" alt="" @click="selectOne">
      <img class="pictureViewer__altsImage" :class="{ 'pictureViewer__altsImage--selected': selected === 2 }"
           src="/images/image-product-2-thumbnail.jpg" alt="" @click="selectTwo">
      <img class="pictureViewer__altsImage" :class="{ 'pictureViewer__altsImage--selected': selected === 3 }"
           src="/images/image-product-3-thumbnail.jpg" alt="" @click="selectThree">
      <img class="pictureViewer__altsImage" :class="{ 'pictureViewer__altsImage--selected': selected === 4 }"
           src="/images/image-product-4-thumbnail.jpg" alt="" @click="selectFour">
    </div>
  </div>
  <div v-if="showPlayer" class="pictureViewer__main--player">
    <span class="pictureViewer__close" @click="showPlayer = false"></span>
    <div class="pictureViewer__main">
      <img v-if="selected === 1" src="/images/image-product-1.jpg" alt="">
      <img v-if="selected === 2" src="/images/image-product-2.jpg" alt="">
      <img v-if="selected === 3" src="/images/image-product-3.jpg" alt="">
      <img v-if="selected === 4" src="/images/image-product-4.jpg" alt="">
    </div>
    <div class="pictureViewer__arrows">
      <span class="pictureViewer__arrows--left" @click="selectPrevious"></span>
      <span class="pictureViewer__arrows--right" @click="selectNext"></span>
    </div>
    <div class="pictureViewer__alts">
      <img class="pictureViewer__altsImage" :class="{ 'pictureViewer__altsImage--selected': selected === 1 }"
           src="/images/image-product-1-thumbnail.jpg" alt="" @click="selectOne">
      <img class="pictureViewer__altsImage" :class="{ 'pictureViewer__altsImage--selected': selected === 2 }"
           src="/images/image-product-2-thumbnail.jpg" alt="" @click="selectTwo">
      <img class="pictureViewer__altsImage" :class="{ 'pictureViewer__altsImage--selected': selected === 3 }"
           src="/images/image-product-3-thumbnail.jpg" alt="" @click="selectThree">
      <img class="pictureViewer__altsImage" :class="{ 'pictureViewer__altsImage--selected': selected === 4 }"
           src="/images/image-product-4-thumbnail.jpg" alt="" @click="selectFour">
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selected: 1,
      showPlayer: false
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
    },
    selectPrevious() {
      if (this.selected >= 2) {
        this.selected--
      }
    },
    selectNext() {
      if (this.selected <= 3) {
        this.selected++
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.pictureViewer {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 40%;
  gap: 30px;

  .pictureViewer__arrows--mobile {
    display: none;

    @media (max-width: 768px) {
      position: absolute;
      display: flex;
      top: 50%;
      width: 100%;
      height: fit-content;
      gap: 350px;

      .pictureViewer__arrows--left,
      .pictureViewer__arrows--right {
        display: flex;
        justify-content: center;
        align-items: center;
        width: 100%;
        height: 100%;

        &:hover {
          cursor: pointer;
        }
      }

      .pictureViewer__arrows--left:before {
        position: absolute;
        z-index: 6;
        content: '';
        display: block;
        width: 12px;
        height: 18px;
        background-color: #1D2026;
        mask: url("/images/icon-previous.svg");
      }

      .pictureViewer__arrows--right:before {
        position: absolute;
        z-index: 6;
        content: '';
        display: block;
        width: 12px;
        height: 18px;
        background-color: #1D2026;
        mask: url("/images/icon-next.svg");

        &:hover {
          background-color: #FF7E1B;
        }
      }

      .pictureViewer__arrows--left:after,
      .pictureViewer__arrows--right:after {
        position: absolute;
        z-index: 5;
        content: '';
        display: block;
        width: 56px;
        height: 56px;
        border-radius: 50%;
        background-color: #FFFFFF;
      }

    }

    @media (max-width: 480px) {
      gap: 250px;
    }
    
    @media (max-width: 320px) {
      gap: 150px;
    }
  }

  .pictureViewer__main {
    overflow-x: hidden;
    img {
      border-radius: 15px;

      @media (max-width: 768px) {
        border-radius: 0;
      }
    }

    &:hover {
      cursor: pointer;
    }
  }

  .pictureViewer__alts {
    display: flex;
    justify-content: space-between;

    .pictureViewer__altsImage {
      width: 20%;
      border-radius: 15px;
      transition: opacity ease-in-out 150ms;

      &:hover {
        cursor: pointer;
        opacity: 0.7;
      }

      &.pictureViewer__altsImage--selected {
        outline: 3px solid #FF7E1B;
      }
    }

    @media (max-width: 768px) {
      display: none;
    }
  }

  @media (max-width: 768px) {
    position: relative;
    width: 100%;
    overflow-x: hidden;
  }
}

.pictureViewer__main--player {
  position: absolute;
  padding-top: 6rem;
  padding-bottom: 12rem;
  top: 0;
  z-index: 999;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-inline: auto;
  gap: 30px;
  width: 100vw;
  background-color: rgba(10, 10, 10, 0.7);

  .pictureViewer__close {
    margin-left: 30rem;
    background-color: #FFFFFF;
    width: 14px;
    height: 15px;
    mask: url("/images/icon-close.svg");
    transition: background-color ease-in-out 150ms;

    &:hover {
      background-color: #FF7E1B;
      cursor: pointer;
    }
  }

  .pictureViewer__main {
    width: 50%;
    max-width: 500px;

    img {
      margin-inline: auto;
      border-radius: 15px;
    }
  }

  .pictureViewer__arrows {
    margin-bottom: 5rem;
    position: absolute;
    display: flex;
    gap: 500px;
    width: 100%;
    max-width: 500px;

    .pictureViewer__arrows--left,
    .pictureViewer__arrows--right {
      display: flex;
      justify-content: center;
      align-items: center;
      width: 100%;
      height: 100%;

      &:hover {
        cursor: pointer;
      }
    }

    .pictureViewer__arrows--left:before {
      position: absolute;
      z-index: 6;
      content: '';
      display: block;
      width: 12px;
      height: 18px;
      background-color: #1D2026;
      mask: url("/images/icon-previous.svg");
    }

    .pictureViewer__arrows--right:before {
      position: absolute;
      z-index: 6;
      content: '';
      display: block;
      width: 12px;
      height: 18px;
      background-color: #1D2026;
      mask: url("/images/icon-next.svg");

      &:hover {
        background-color: #FF7E1B;
      }
    }

    .pictureViewer__arrows--left:after,
    .pictureViewer__arrows--right:after {
      position: absolute;
      z-index: 5;
      content: '';
      display: block;
      width: 56px;
      height: 56px;
      border-radius: 50%;
      background-color: #FFFFFF;
    }
  }

  .pictureViewer__alts {
    display: flex;
    justify-content: space-between;
    width: 50%;
    max-width: 500px;

    .pictureViewer__altsImage {
      width: 20%;
      border-radius: 15px;
      transition: opacity ease-in-out 150ms;

      &:hover {
        cursor: pointer;
        opacity: 0.7;
      }

      &.pictureViewer__altsImage--selected {
        outline: 3px solid #FF7E1B;
      }
    }
  }
}
</style>