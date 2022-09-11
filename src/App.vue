<template>
  <div id="app">
    <header>
      <Navigation @showCart="toggleCartState" v-bind:counter="amount" />
    </header>
    <section>
      <div class="container">
        <div class="wrap-content">
          <DesktopImages
            @changeDesktopCarouselStatus="changeDesktopCarouselState"
            class="column"
            v-show="!mobile"
          />
          <MobileCarousel v-show="mobile" />
          <ShoeInfo @addToCart="toggleCounterAmount" class="column" />
          <Cart
            v-show="showCart"
            v-bind:counter="amount"
            @cartItemsAmountSet0="deleteItems"
          />
        </div>
      </div>
    </section>

    <div v-show="showDesktopCarousel" class="desktop-carousel">
      <DesktopCarousel
        @desktopCarouselState="changeDesktopCarouselState"
        class="column"
        v-show="!mobile"
      />
      <!-- <DesktopImages class="column" v-show="!mobile" /> -->
    </div>
  </div>
</template>

<script>
import Navigation from "@/components/Navigation";
import MobileCarousel from "@/components/MobileCarousel";
import ShoeInfo from "@/components/ShoeInfo";
import DesktopImages from "@/components/DesktopImages";
import DesktopCarousel from "@/components/DesktopCarousel";
import Cart from "@/components/Cart";

export default {
  name: "App",
  components: {
    Navigation,
    MobileCarousel,
    ShoeInfo,
    DesktopImages,
    Cart,
    DesktopCarousel,
  },
  data() {
    return {
      mobile: true,
      showCart: false,
      amount: 0,
      showDesktopCarousel: false,
    };
  },
  methods: {
    checkCurrentWidth() {
      let width = document.body.clientWidth;
      if (width > 800) {
        this.mobile = false;
      } else {
        this.mobile = true;
      }
    },
    toggleCartState(event) {
      this.showCart = event;
    },
    toggleCounterAmount(event) {
      this.amount = event;
    },
    deleteItems(event) {
      this.amount = event;
    },
    changeDesktopCarouselState() {
      console.log("clicked")
      this.showDesktopCarousel = !this.showDesktopCarousel;
    },
  },
  created() {
    this.checkCurrentWidth();
  },
  mounted() {
    window.addEventListener("resize", this.checkCurrentWidth);
  },
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;

  --orange: hsl(26, 100%, 55%);
  --pale-orange: hsl(25, 100%, 94%);

  --very-dark-blue: hsl(220, 13%, 13%);
  --dark-grayish-blue: hsl(219, 9%, 45%);
  --grayish-blue: hsl(220, 14%, 75%);
  --light-grayish-blue: hsl(223, 64%, 98%);
  --white: hsl(0, 0%, 100%);
  --black: hsl(0, 0%, 0%);
  font-family: "Kumbh Sans", sans-serif;
  // border: 1px solid greenyellow;
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  // border: 1px solid red;
  height: 100vh;
  width: 100vw;
}

.container {
  width: 100%;
  display: flex;
  justify-content: center;
}

.wrap-content {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  max-width: 1200px;

  @media (min-width: 800px) {
    flex-direction: row;
  }
}

.column {
  display: flex;
  flex-direction: column;
  flex: 1;
}

.desktop-carousel {
  width: 100vw;
  height: 100vh;
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  margin: auto;
  // display: grid;
  // place-items: center;
  z-index: 10;
  background: rgba($color: black, $alpha: 0.7);
}

@keyframes slideInFromLeft {
  from {
    transform: translateX(-1000px);
  }

  to {
    transform: translateX(0);
  }
}

@keyframes showUp {
  from {
    opacity: 0;
  }

  to {
    opacity: 1;
  }
}

@keyframes showFromTop {
  from {
    transform: scaleY(0);
  }

  to {
    transform: scaleY(1);
  }
}
</style>