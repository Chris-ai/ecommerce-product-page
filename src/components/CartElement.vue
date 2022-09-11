<template>
  <div class="cart-element">
    <div v-show="amount != 0" class="element">
      <img
        src="../assets/image-product-1-thumbnail.jpg"
        alt="cart-element-icon"
      />
      <div class="prduct-info">
        <p>Fall Limited Edition Sneakers</p>
        <p>
          $125.00 x {{ amount }} <b>${{ totalPrice * amount }}.00</b>
        </p>
      </div>
      <img
        @click="deleteCartElements"
        class="icon"
        src="../assets/icon-delete.svg"
        alt="delete"
      />
    </div>
    <div class="empty-cart" v-show="amount === 0">Your cart is empty</div>
    <button v-show="amount != 0" class="checkout-btn">Checkout</button>
  </div>
</template>

<script>
export default {
  props: ["amount"],
  data() {
    return {
      // amount: 3,
      totalPrice: 125.0,
    };
  },
  methods: {
    deleteCartElements() {
      // console.log('delete items')
      this.$emit("removeItems", 0);
    },
  },
};
</script>

<style lang="scss">
.cart-element {
  display: flex;
  flex-direction: column;
  .element {
    display: flex;
    justify-content: space-between;
    align-items: center;
    p {
      color: var(--dark-grayish-blue);
      line-height: 1.5;
      font-size: 15px;
    }

    img {
      width: 50px;
      height: 50px;
      border-radius: 8px;
    }

    .icon {
      height: 20px;
      width: 20px;
      object-fit: contain;
      cursor: pointer;
    }
    @media (max-width: 800px) {
      p {
        font-size: 12px;
      }
    }
  }

  .checkout-btn {
    bottom: 20px;
    margin: auto;
    width: 100%;
    margin: 1.8rem 0;
    padding: 1.2rem 0;
    color: var(--white);
    background: var(--orange);
    outline: none;
    border: none;
    border-radius: 0.8rem;
    cursor: pointer;
    transition: 0.3s ease all;
    letter-spacing: 0.5px;
    display: flex;
    justify-content: center;
    font-weight: 700;

    &:hover {
      opacity: 0.7;
    }
  }

  .empty-cart {
    height: 100%;
    width: 100%;
    display: grid;
    place-items: center;
    font-size: 18px;
    color: var(--grayish-blue);
    font-weight: 700;
    padding: 50px 0;
  }
}
</style>