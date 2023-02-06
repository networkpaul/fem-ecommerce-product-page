<template>
  <div class="addToCart">
    <div class="addToCart__counter">
      <button class="addToCart__minus" @click="removeItem"></button>
      <span class="addToCart__number">{{ items }}</span>
      <button class="addToCart__plus" @click="addItem"></button>
    </div>
    <button class="addToCart__button" :class="{ 'addToCart__button--disabled': items === 0 }" :disabled="items === 0" @click.once="addToCart">
      Add to cart
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: 0,
      totalPrice: null,
      isEmpty: true,
    }
  },
  methods: {
    removeItem() {
      if (this.items > 0) {
        this.items--
      }
    },
    addItem() {
      if (this.items >= 0) {
        this.items++
      }
    },
    addToCart() {
      this.totalPrice = 125 * this.items
      this.isEmpty = !this.isEmpty
      this.$emit('cartInfos', this.items, this.totalPrice, this.isEmpty)
      this.items = 0
    }
  }
}
</script>

<style lang="scss" scoped>
.addToCart {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;

  @media (max-width: 768px) {
    margin-inline: auto;
    flex-direction: column;
    gap: 20px;
  }
}

.addToCart__counter {
  padding-block: 1.5rem;
  padding-inline: 1.5rem;
  width: 35%;
  min-width: 125px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #F6F8FD;
  border-radius: 10px;

  @media (max-width: 768px) {
    justify-content: space-between;
    width: 100%;
  }
}

.addToCart__minus {
  display: block;
  width: 12px;
  height: 4px;
  background-color: #FF7E1B;
  mask: url("/images/icon-minus.svg");

  &:hover {
    background-color: #FFAB6A;
  }
}

.addToCart__plus {
  display: block;
  width: 12px;
  height: 12px;
  background-color: #FF7E1B;
  mask: url("/images/icon-plus.svg");

  &:hover {
    background-color: #FFAB6A;
  }
}

.addToCart__number {

  display: flex;
  align-items: center;
  font-size: 16px;
  line-height: 20px;
  font-weight: 700;

}

.addToCart__button {
  display: flex;
  gap: 20px;
  padding-block: 1.5rem;
  padding-inline: 5rem;
  border-radius: 10px;
  color: #FFFFFF;
  font-size: 16px;
  line-height: 20px;
  font-weight: 700;
  background-color: #FF7E1B;

  &:hover {
    background-color: #FFAB6A;
  }

  &:before {
    content: '';
    display: block;
    background-color: #FFFFFF;
    width: 22px;
    height: 20px;
    mask: url("/images/icon-cart.svg");
  }

  &.addToCart__button--disabled:hover {
    cursor: not-allowed;
  }
}
</style>