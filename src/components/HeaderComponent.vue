<template>
  <div class="header">
    <div v-if="showMobile" class="header__mobile">
      <span class="header__mobile--close" @click="showMobile = false"></span>
      <ul class="header__categories header__categories--mobile">
        <li v-for="categorie in categories">
          <a class="header__categorie header__categorie--mobile" href="#">{{ categorie.categorie }}</a>
        </li>
      </ul>
    </div>
    <div class="header__left">
      <button class="header__hamburger" @click="showMobile = !showMobile"></button>
      <div class="header__logo">
        <a href="#">
          <img class="header__image" src="/images/logo.svg" alt="Sneakers Logo">
        </a>
      </div>
      <ul class="header__categories">
        <li v-for="categorie in categories">
          <a class="header__categorie" href="#">{{ categorie.categorie }}</a>
        </li>
      </ul>
    </div>
    <div class="header__right">
      <button class="header__cart" @click="openCart"></button>
      <span v-if="!isEmpty" class="header__cart--items">{{ items }}</span>
      <button class="header__avatar">
        <img class="header__image" src="/images/image-avatar.png" alt="">
      </button>
    </div>
    <div class="cart" :class="{ 'cart--opened': isOpen, 'cart--empty': isEmpty }">
      <span class="cart__title">Cart</span>
      <span class="cart__noItems" v-if="isEmpty">Your cart is empty</span>
      <div class="cart__top">
        <div class="cart__thumb">
          <img class="header__image" src="/images/image-product-1-thumbnail.jpg" alt="">
        </div>
        <div class="cart__description">
          <span class="cart__descriptionTitle">Fall Limited Edition Sneakers</span>
          <span class="cart__descriptionPrice">$125.00</span>
          <span class="cart__descriptionTimes">x {{ items }}</span>
          <span class="cart__descriptionTotal">${{ totalPrice }}</span>
        </div>
        <button class="cart__delete" @click="removeCartItems"></button>
      </div>
      <button v-if="!isEmpty" class="cart__checkout">Checkout</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HeaderComponent',
  data() {
    return {
      categories: [
        {categorie: 'Collections'},
        {categorie: 'Men'},
        {categorie: 'Women'},
        {categorie: 'About'},
        {categorie: 'Contact'}
      ],
      isOpen: false,
      isEmpty: true,
      showMobile: false,
    }
  },
  methods: {
    openCart() {
      this.isOpen = !this.isOpen
    },
    removeCartItems() {
      this.isEmpty = !this.isEmpty
    }
  },
  props: ['items', 'totalPrice', 'empty'],
  updated() {
    this.isEmpty = this.empty
  }
}
</script>

<style lang="scss">

.header {
  margin-inline: auto;
  position: relative;
  padding: 1.5rem 4rem 3rem 4rem;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: space-between;
  row-gap: 2rem;
  width: 100%;
  max-width: 1260px;

  &:after {
    content: '';
    display: block;
    width: 100%;
    height: 1px;
    background-color: #E4E9F2;

    @media (max-width: 768px) {
      display: none;
    }
  }

  .header__mobile {
    padding: 2rem;
    position: absolute;
    z-index: 1000;
    background-color: #FFFFFF;
    width: 45%;
    min-width: 280px;
    height: 100vh;
    top: 0;
    left: 0;
    box-shadow: 300px 0 0 200px rgba(0,0,0,0.6);

    .header__mobile--close {
      margin-bottom: 3.5rem;
      background-color: #69707D;
      display: block;
      width: 14px;
      height: 15px;
      mask: url("/images/icon-close.svg");
    }

    .header__categories--mobile {
      display: flex;
      flex-direction: column;
      gap: 20px;

      .header__categorie--mobile {
        font-size: 18px;
        line-height: 26px;
        font-weight: 700;
      }
    }
  }

  .header__left {
    display: flex;
    justify-content: flex-start;
    align-items: center;
    gap: 50px;
    width: 60%;
    min-width: 250px;

    .header__hamburger {
      display: none;
      background-color: #69707D;
      width: 16px;
      height: 15px;
      mask: url("/images/icon-menu.svg");

      @media (max-width: 768px) {
        display: block;
      }
    }

    .header__logo {
      width: 20%;
      min-width: 135px;
    }

    .header__categories {
      display: flex;
      gap: 30px;
      font-size: 15px;
      line-height: 26px;
      font-weight: 400;
      color: #69707D;

      @media (max-width: 768px) {
        display: none;
      }

      .header__categorie {
        position: relative;
        display: flex;
        flex-direction: column;
      }

      .header__categorie:hover {
        color: #1D2026;

        &:after {
          position: absolute;
          bottom: -42px;
          content: '';
          display: block;
          width: 100%;
          height: 5px;
          background-color: #FF7E1B;
        }
      }
    }

    @media (max-width: 768px) {
      justify-content: flex-start;
      gap: 15px;
    }
  }

  .header__right {
    display: flex;
    justify-content: flex-end;
    align-items: center;
    gap: 30px;
    width: 20%;
    min-width: 90px;

    .header__cart {
      background-color: #69707D;
      width: 22px;
      height: 20px;
      mask: url("/images/icon-cart.svg");

      &:hover {
        background-color: #1D2026;
      }
    }

    .header__avatar {
      width: 20%;

      &:hover {
        outline: 2px solid #FF7E1B;
        border-radius: 100%;
      }
    }
  }

  .header__cart--items {
    position: absolute;
    top: 25px;
    right: 125px;
    z-index: 1;
    padding: 3px 10px;
    font-size: 10px;
    line-height: 14px;
    font-weight: 700;
    background-color: #FF7E1B;
    border-radius: 10px;
    color: #FFFFFF;
  }

  @media (max-width: 768px) {
    padding: 1.5rem 2rem 0 2rem;
    flex-wrap: nowrap;
  }
}

.header__image {
  width: 100%;
}

.cart {
  display: none;

  &.cart--opened {
    padding-block: 2rem;
    position: absolute;
    top: 85px;
    right: 30px;
    display: flex;
    flex-direction: column;
    background-color: #FFFFFF;
    box-shadow: 0 20px 50px -20px rgba(29, 32, 38, 0.503143);
    border-radius: 10px;
    width: 40%;

    @media (max-width: 768px) {
      top: 100px;
      left: 0;
      right: 0;
      width: 95%;
      margin-inline: 1rem;
      z-index: 999;
    }
  }

  &.cart--opened.cart--empty {
    .cart__top {
      visibility: hidden;
    }

    .cart__checkout {
      visibility: hidden;
    }

    .cart__noItems {
      position: absolute;
      left: 50%;
      top: 70%;
      transform: translate(-50%, -50%);
      font-size: 16px;
      line-height: 26px;
      font-weight: 700;
      color: #69707D;
    }
  }
}

.cart__title {
  position: relative;
  padding-inline: 2rem;
  padding-bottom: 2rem;
  font-size: 16px;
  line-height: 20px;
  font-weight: 700;
  color: #1D2026;

  &:after {
    position: absolute;
    margin-top: 2rem;
    content: '';
    display: block;
    left: 0;
    right: 0;
    width: 100%;
    height: 1px;
    background-color: #E4E9F2;
  }
}

.cart__top {
  padding-inline: 2rem;
  padding-top: 2rem;
  display: flex;
  align-items: center;
  justify-content: space-between;

  .cart__thumb {
    width: 15%;

    .header__image {
      border-radius: 6px;
    }
  }

  .cart__description {
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    column-gap: 10px;
    width: 70%;
    font-size: 16px;
    color: #69707D;

    .cart__descriptionTitle {
      width: 100%;
    }

    .cart__descriptionTotal {
      font-weight: 700;
      color: #1D2026;
    }
  }

  .cart__delete {
    background-color: #C3CAD9;
    display: block;
    width: 14px;
    height: 16px;
    mask: url("/images/icon-delete.svg");
    align-self: center;
    transition: background-color ease-in-out 150ms;

    &:hover {
      background-color: #1D2026;
    }
  }
}

.cart__checkout {
  margin-top: 2rem;
  margin-inline: 2rem;
  padding-block: 1.5rem;
  border-radius: 10px;
  color: #FFFFFF;
  font-size: 16px;
  line-height: 20px;
  font-weight: 700;
  background-color: #FF7E1B;
}
</style>