<template>
  <div class="carousel">
    <img v-show="img == 1" src="../assets/image-product-1.jpg" alt="" />
    <img v-show="img == 2" src="../assets/image-product-2.jpg" alt="" />
    <img v-show="img == 3" src="../assets/image-product-3.jpg" alt="" />
    <img v-show="img == 4" src="../assets/image-product-4.jpg" alt="" />

    <div v-on:click="goToPrevious" class="arrow-btn previous">
      <img src="../assets/icon-previous.svg" alt="previous" />
    </div>

    <div v-on:click="goToNextImage" class="arrow-btn next">
      <img src="../assets/icon-next.svg" alt="next" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      img: 1,
    };
  },
  methods: {
    goToNextImage() {
      //   console.log(this.img);
      if (this.img < 4) {
        this.img += 1;
      } else {
        console.log("This is last one :/");
      }
    },
    goToPrevious() {
      if (this.img > 1) {
        this.img -= 1;
      } else {
        console.log("This is first image of this sneakers");
      }
    },
  },
};
</script>

<style lang="scss">
.carousel {
  width: 100%;
  height: 75vw;
  position: relative;

  img {
    width: 100%;
    height: 100%;
    /* object-fit: contain; */
  }

  .arrow-btn {
    // padding: 1rem;
    // width: 36px;
    // height: 36px;
    height: 30px;
    width: 30px;
    border-radius: 50%;
    border: none;
    outline: none;
    background: var(--white);
    position: absolute;
    // text-align: center;
    display: grid;
    place-items: center;
    // display: flex;
    // align-items: center;
    // justify-content: center;
    img {
      height: 13px;
      width: 9px;
    }
  }

  .next {
    top: 0;
    bottom: 0;
    right: 5%;
    margin: auto;
  }

  .previous {
    top: 0;
    bottom: 0;
    left: 5%;
    margin: auto;
  }
}
</style>