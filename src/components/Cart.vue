<template>
  <div class="cart">
    <div class="title">
      <h4>Cart</h4>
    </div>

    <div class="content">
      <CartElement v-bind:amount="this.counter" @removeItems="cartItemsTo0" />
    </div>
  </div>
</template>

<script>
import CartElement from "@/components/CartElement";

export default {
  components: { CartElement },
  props: ["counter"],
  methods: {
    cartItemsTo0(event){
      this.$emit("cartItemsAmountSet0", event)
    }
  },
};
</script>

<style lang="scss">
.cart {
  position: absolute;
  top: -25px;
  //   left: 0;
  right: -100px;
  margin: auto;
  width: 95vw;
  height: 40vh;
  max-width: 350px;
  max-height: 250px;
  background: var(--white);
  border-radius: 10px;
  -webkit-box-shadow: 0px 55px 100px -26px rgba(195, 195, 195, 1);
  -moz-box-shadow: 0px 55px 100px -26px rgba(195, 195, 195, 1);
  box-shadow: 0px 55px 100px -26px rgba(195, 195, 195, 1);
  transition: 0.3s ease all;
  animation: 0.3s showFromTop ease-in-out;

  .title {
    width: 100%;
    padding: 1.2rem;
    border-bottom: 1px solid var(--pale-orange);
    animation: 0.7s showUp ease-in-out;
  }

  .content {
    width: 100%;
    padding: 1.2rem;
    animation: 0.7s showUp ease-in-out;
  }

  //   @media(min-width: 580px){
  //     right: 0;
  //   }

  @media (max-width: 1200px) {
    right: 0;
  }
  @media (max-width: 800px) {
    top: 20px;
    left: 0;
    right: 0;
  }
}
</style>