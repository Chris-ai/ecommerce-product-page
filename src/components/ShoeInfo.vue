<template>
  <!-- <h1>helo</h1> -->
  <div class="info">
    <h5>SNEAKER COMPANY</h5>
    <h2>
      Fall Limited Edition <br />
      Sneakers
    </h2>
    <p>
      These low-profile sneakers are your perfect casual wear companion.
      Featuring a durable rubber outer sole, they’ll withstand everything the
      weather can offer.
    </p>

    <div class="prices">
      <div class="price">
        <p>{{ price }}</p>
      </div>
      <div>
        <p class="original-price">{{ originalPrice }}</p>
      </div>
    </div>

    <div class="row-column">
      <div class="counter">
        <input type="number" v-model="counter" min="0" />
        <div v-on:click="plusCounter" class="plus">
          <img src="../assets/icon-plus.svg" alt="plus" />
        </div>
        <div v-on:click="minusCounter" class="minus">
          <img src="../assets/icon-minus.svg" alt="minus" />
        </div>
      </div>

      <button @click="addToCart" class="add-to-cart-btn">
        <img src="../assets/icon-btn-cart.svg" alt="cartBtn" />
        <span>Add to cart</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      price: "$125.00",
      salePercet: "50%",
      originalPrice: "$250.00",
      counter: 0,
    };
  },
  methods: {
    plusCounter() {
      this.counter++;
    },
    minusCounter() {
      if (this.counter > 0) {
        this.counter--;
      }
    },
    addToCart(){
      this.$emit("addToCart", this.counter)
    }
  },
};
</script>

<style lang="scss">
.info {
  width: 100%;
  max-width: 510px;
  padding: 1.2rem;
  //   max-width: 30px;

  h5 {
    font-size: 12px;
    text-transform: uppercase;
    letter-spacing: 1px;
    color: var(--orange);
    margin: 0.6rem 0;
  }

  h2 {
    color: var(--very-dark-blue);
    margin: 0.8rem 0;
  }

  p {
    color: var(--dark-grayish-blue);
    text-justify: justify;
    font-size: 15px;
    line-height: 1.5;
  }

  .prices {
    display: flex;
    flex-direction: row;
    margin: 1.2rem 0;
    justify-content: space-between;

    .price {
      position: relative;
      p {
        font-size: 26px;
        font-weight: 700;
        color: var(--very-dark-blue);
      }
    }

    .price::after {
      position: absolute;
      display: grid;
      place-items: center;
      content: "50%";
      height: 60%;
      // min-width: 10px;
      border-radius: 6px;
      background: var(--pale-orange);
      color: var(--orange);
      font-weight: 700;
      font-size: 12px;
      padding: 0 0.5rem;
      top: 0;
      bottom: 0;
      margin: auto;
      right: -50px;
    }

    .original-price {
      text-decoration: line-through;
      font-weight: 700;
      font-size: 14px;
      color: var(--grayish-blue);
    }
  }

  .counter {
    width: 100%;
    position: relative;
    input {
      width: 100%;
      padding: 1.2rem 0;
      text-align: center;
      outline: none;
      border: none;
      background: #f6f6f6;
      border-radius: 1rem;
      font-weight: 700;
      font-size: 1rem;
    }
    /* Chrome, Safari, Edge, Opera */
    input::-webkit-outer-spin-button,
    input::-webkit-inner-spin-button {
      -webkit-appearance: none;
      margin: 0;
    }

    /* Firefox */
    input[type="number"] {
      -moz-appearance: textfield;
    }
    .plus,
    .minus {
      display: flex;
      align-items: center;
      cursor: pointer;
    }

    .minus {
      position: absolute;
      top: 0;
      left: 25px;
      bottom: 0;
      margin: auto;
    }

    .plus {
      position: absolute;
      top: 0;
      right: 25px;
      bottom: 0;
      margin: auto;
    }
  }

  .add-to-cart-btn {
    width: 100%;
    margin: 1.2rem 0;
    padding: 1.2rem 0;
    color: var(--white);
    background: var(--orange);
    outline: none;
    border: none;
    border-radius: 0.8rem;
    cursor: pointer;
    box-shadow: 0px 15px 25px 2px rgba(252, 167, 64, 0.267);
    transition: 0.3s ease all;
    // font-size: 18px;
    letter-spacing: 0.5px;
    display: flex;
    justify-content: center;
    font-weight: 700;
    span {
      margin-left: 1rem;
    }
    img {
      fill: white;
      height: 16px;
      width: 16px;
    }

    &:hover {
      opacity: 0.7;
    }
  }

  .row-column {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  @media (min-width: 800px) {
    // height: 100%;
    // align-content: ;
    // padding: 0;
    h2 {
      font-size: 38px;
    }
    .prices {
      flex-direction: column;
      .price {
        width: max-content;
      }
    }

    .row-column {
      flex-direction: row;
      justify-content: space-between;

      .counter {
        width: 70%;
        margin-right: 0.4rem;
      }

      .add-to-cart-btn {
        margin-left: 1rem;
      }
    }
  }
}
</style>