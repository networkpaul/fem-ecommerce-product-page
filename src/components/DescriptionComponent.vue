<template>
  <div class="description">
    <p class="description__company">{{ company }}</p>
    <h1 class="description__title">{{ title }}</h1>
    <p class="description__text">{{ text }}</p>
    <div class="description__prices">
      <span class="description__currentPrice">{{ currentPrice }}</span>
      <span class="description__rebate">{{ rebate }}</span>
      <span class="description__originalPrice">{{ originalPrice }}</span>
    </div>
    <AddToCart @cart-infos="getCart"/>
  </div>
</template>

<script>

import AddToCart from "./AddToCart.vue";

export default {
  name: 'DescriptionComponent',
  components: {AddToCart},
  props: ['company', 'title', 'text', 'currentPrice', 'originalPrice', 'rebate'],
  data() {
    return {
      cartInfo: null,
      totalPrice: null,
      isEmpty: true
    }
  },
  methods: {
    getCart(cartItems, totalPrice, empty) {
      this.cartInfo = cartItems
      this.totalPrice = totalPrice
      this.isEmpty = empty
      this.$emit('cartInfos', this.cartInfo, this.totalPrice, this.isEmpty)
    }
  }
}
</script>

<style lang="scss" scoped>
.description {
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 30px;
  width: 40%;
  overflow-x: hidden;

  .description__company {
    text-transform: uppercase;
    font-size: 13px;
    line-height: 16px;
    font-weight: 700;
    letter-spacing: 2px;
    color: #FF7E1B;
  }

  .description__title {
    font-size: 44px;
    line-height: 48px;
    font-weight: 700;
    color: #1D2026;
  }

  .description__text {
    font-size: 16px;
    line-height: 26px;
    color: #69707D;
  }

  .description__prices {
    display: flex;
    flex-wrap: wrap;
    column-gap: 20px;

    .description__currentPrice {
      font-size: 28px;
      line-height: 34px;
      font-weight: 700;
      color: #1D2026;
    }

    .description__rebate {
      padding-inline: 0.5rem;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 16px;
      line-height: 20px;
      font-weight: 700;
      color: #FF7E1B;
      border-radius: 6px;
      background-color: #FFEEE2;
    }

    .description__originalPrice {
      text-decoration: line-through;
      font-size: 16px;
      line-height: 26px;
      font-weight: 700;
      color: #B6BCC8;
      width: 100%;
      
      @media (max-width: 768px) {
        text-align: right;
      }
    }

    @media (max-width: 768px) {
      margin-inline: auto;
      flex-wrap: nowrap;
      width: 100%;
    }
  }

  @media (max-width: 768px) {
    padding-inline: 2rem;
    width: 100%;
  }
}
</style>