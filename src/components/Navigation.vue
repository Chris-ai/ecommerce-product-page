<template>
  <nav class="container">
    <div class="wrapper">
      <div class="left-col">
        <div
          id="menu-mobile-icon"
          class="nav-image state-controller"
          v-on:click="toggleMobileMenu"
        >
          <img
            style="width: 12px; height: 12px"
            src="../assets/icon-menu.svg"
            alt="menu"
          />
        </div>
        <div class="logo">
          <img src="../assets/logo.svg" alt="logo" />
        </div>

        <div class="links">
          <a href="/">Collections</a>
          <a href="/">Men</a>
          <a href="/">Women</a>
          <a href="/">About</a>
          <a href="/">Contact</a>
        </div>
      </div>

      <div class="right-col">
        <div @click="showCartBtn" class="nav-image state-controller">
          <img src="../assets/icon-cart.svg" alt="cart" />
          <div v-show="counter != 0" class="counter">{{ counter }}</div>
        </div>
        <div
          id="avatar"
          class="nav-image state-controller"
        >
          <img src="../assets/image-avatar.png" alt="avatar_" />
        </div>
      </div>
    </div>

    <div v-show="showMobileMenu" class="mobile-menu">
      <div class="menu">
        <div class="close-image">
          <img
            class="state-controller"
            v-on:click="toggleMobileMenu"
            src="../assets/icon-close.svg"
            alt="closeMenu"
          />
        </div>

        <ul class="menu-list">
          <li>Collections</li>
          <li>Men</li>
          <li>Women</li>
          <li>About</li>
          <li>Contact</li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  props: ["counter"],
  data() {
    return {
      showMobileMenu: false,
      showCart: false,
    };
  },
  methods: {
    toggleMobileMenu() {
      this.showMobileMenu = !this.showMobileMenu;
    },
    showCartBtn() {
      this.showCart = !this.showCart;
      this.$emit('showCart', this.showCart)
    },
  },
};
</script>

<style lang="scss">
.wrapper {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 70px;
  width: 100%;
  max-width: 1200px;

  .left-col,
  .right-col {
    display: flex;
    align-items: center;
    height: 100%;
    padding: 0 1rem;
    transition: 0.3s ease all;
  }

  .links {
    align-items: center;
    height: 100%;
    display: none;
    margin-left: 2.2rem;

    a {
      margin: 0 0.4rem;
      text-decoration: none;
      color: var(--grayish-blue);
      height: 100%;
      //   text-align: center;
      display: flex;
      align-items: center;
      transition: 0.3s ease all;
      &:hover,
      &:focus {
        // border-bottom: 4px solid var(--orange);
        box-shadow: inset 0 -5px 0 var(--orange);
        color: var(--very-dark-blue);
      }
    }
  }

  .nav-image {
    width: 25px;
    height: 25px;
    margin: 0 0.5rem;
    padding: 0.25rem;
    position: relative;
    display: flex;
    // flex-direction: ;
    align-items: center;
    justify-content: center;

    .counter {
      position: absolute;
      top: 0;
      right: 0;
      width: 60%;
      height: 20%;
      background: var(--orange);
      color: var(--white);
      font-size: 10px;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 0.35rem;
      border-radius: 50em;
      // text-align: center;
    }

    img {
      width: 100%;
      height: 100%;
    }
  }

  .logo {
    img {
      transition: 0.3s ease all;
      height: 15px;
    }
  }
  @media (min-width: 800px) {
    border-bottom: 2px solid var(--pale-orange);
    height: 15vh;

    .links {
      display: flex;
    }

    #menu-mobile-icon {
      display: none;
    }

    .nav-image {
      width: 35px;
      height: 35px;

      img:hover {
        color: black;
      }
      .counter {
        font-size: 12px;
        padding: 0.4rem;
      }
    }
  }

  @media (min-width: 950px) {
    .links {
      a {
        margin: 0 1rem;
      }
    }

    .logo {
      img {
        height: 25px;
      }
    }
  }
}

.mobile-menu {
  position: absolute;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100vw;
  z-index: 1;
  background: rgba($color: black, $alpha: 0.75);
  animation: 0.2s showUp ease-in-out;

  .menu {
    display: flex;
    flex-direction: column;
    height: 100%;
    width: 60%;
    background: var(--white);
    padding: 2rem;
    animation: 0.5s slideInFromLeft ease-in-out;

    .close-image {
      width: 100%;
      padding-bottom: 3rem;
    }

    .menu-list {
      list-style: none;

      li {
        font-weight: 700;
        padding: 0.6rem 0;
      }
    }
  }
}

.state-controller {
  cursor: pointer;
}

#avatar {
  padding: 0;
  border: 2px solid transparent;
  border-radius: 50em;
  transition: 0.2s ease all;

  &:hover,
  &:focus {
    border: 2px solid var(--orange);
  }

  @media (min-width: 780px) {
    width: 50px;
    height: 50px;
  }
}
</style>