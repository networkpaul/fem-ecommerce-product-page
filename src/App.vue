<template>
  <div>
    <HeaderComponent
              :items="cartItems"
              :total-price="totalPrice"
              :empty="isEmpty"
    />
    <main class="main-content">
    <PictureViewer />
    <DescriptionComponent
              :company="'Sneaker Company'"
              :title="'Fall Limited Edition Sneakers'"
              :text="'These low-profile sneakers are your perfect casual wear companion. Featuring a durable rubber outer sole, they’ll withstand everything the weather can offer.'"
              :current-price="'$125.00'"
              :original-price="'$250.00'"
              :rebate="'50%'"
              @cart-infos="getCart"
    />
    </main>
  </div>
  
</template>

<script>
import HeaderComponent from "./components/HeaderComponent.vue";
import PictureViewer from "./components/PictureViewer.vue";
import DescriptionComponent from "./components/DescriptionComponent.vue";
export default {
  components: { HeaderComponent, DescriptionComponent, PictureViewer },
  data() {
    return {
      cartItems: null,
      totalPrice: null,
      isEmpty: true
    }
  },
  methods: {
    getCart(itemsNumber, totalPrice, empty) {
      this.cartItems = itemsNumber
      this.totalPrice = totalPrice
      this.isEmpty = empty
    }
  }
}
</script>

<style lang="scss">

@import url('https://fonts.googleapis.com/css2?family=Kumbh+Sans:wght@100;200;300;400;500;600;700;800;900&family=Plus+Jakarta+Sans:wght@500;700&display=swap');

body {
  font-family: Kumbh Sans;
}

.main-content {
  display: flex;
  justify-content: space-around;
  padding-block: 5%;
}

</style>
