<template>
  <div class="images-desktop">
    <div @click="closeDesktopCarousel" class="close">
      <img src="../assets/orange-icon-close.svg" alt="" />
    </div>

    <img
      v-show="imageId == 1"
      class="desktop-big-image"
      src="../assets/image-product-1.jpg"
      alt="bigImage"
    />
    <img
      v-show="imageId == 2"
      class="desktop-big-image"
      src="../assets/image-product-2.jpg"
      alt="bigImage"
    />
    <img
      v-show="imageId == 3"
      class="desktop-big-image"
      src="../assets/image-product-3.jpg"
      alt="bigImage"
    />
    <img
      v-show="imageId == 4"
      class="desktop-big-image"
      src="../assets/image-product-4.jpg"
      alt="bigImage"
    />

    <div class="desktop-images-list">
      <img
        @click="chooseImage"
        id="1"
        class="desktop-thumbnail"
        src="../assets/image-product-1-thumbnail.jpg"
        alt=""
      />
      <img
        @click="chooseImage"
        id="2"
        class="desktop-thumbnail"
        src="../assets/image-product-2-thumbnail.jpg"
        alt=""
      />
      <img
        @click="chooseImage"
        id="3"
        class="desktop-thumbnail"
        src="../assets/image-product-3-thumbnail.jpg"
        alt=""
      />
      <img
        @click="chooseImage"
        id="4"
        class="desktop-thumbnail"
        src="../assets/image-product-4-thumbnail.jpg"
        alt=""
      />
    </div>

    <div @click="goToNextImage" class="next-btn">
      <img src="../assets/icon-next.svg" alt="" />
    </div>
    <div @click="goToPrevious" class="previous-btn">
      <img src="../assets/icon-previous.svg" alt="" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      imageId: 1,
    };
  },
  methods: {
    setClass(images) {
      images.forEach((e) => {
        if (
          e.classList.contains("desktop-selected-image") &&
          e.id != this.imageId
        ) {
          e.classList.remove("desktop-selected-image");
        } else if (e.id == this.imageId) {
          e.classList.add("desktop-selected-image");
        }
      });
    },
    chooseImage(e) {
      console.log(e.path[0].id);
      this.imageId = e.path[0].id;

      let images = document.querySelectorAll(".desktop-thumbnail");
      this.setClass(images);
    },
    goToNextImage() {
      if (this.imageId < 4) {
        this.imageId++;
        let images = document.querySelectorAll(".desktop-thumbnail");
        this.setClass(images);
      } else {
        console.log("This is last one :/");
      }
    },
    goToPrevious() {
      if (this.imageId > 1) {
        this.imageId--;
        let images = document.querySelectorAll(".desktop-thumbnail");
        this.setClass(images);
      } else {
        console.log("This is first image of this sneakers");
      }
    },
    closeDesktopCarousel() {
      this.$emit("desktopCarouselState", false);
    },
  },
  mounted() {
    document.getElementById("1").classList.add("desktop-selected-image");
  },
};
</script>

<style lang="scss">
.images-desktop {
  width: 100%;
  padding: 0;
  // padding: 5rem 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  position: relative;

  .desktop-big-image {
    width: 480px;
    height: 480px;
    border-radius: 12px;
    cursor: pointer;
  }

  .desktop-images-list {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    margin: 2.4rem 0;
    img {
      width: 80px;
      height: 80px;
      margin: 0 1rem;
      border-radius: 10px;
      cursor: pointer;

      &:hover {
        opacity: 0.5;
        outline: 3px solid var(--orange);
      }
    }
  }
}

.desktop-selected-image {
  opacity: 0.5;
  outline: 3px solid var(--orange);
}

.close {
  width: 480px;
  text-align: right;
  margin: 3.5rem 0 0.5rem 0;
  img {
    height: 20px;
    width: 20px;
    cursor: pointer;
  }
}

.next-btn {
  position: absolute;
  top: 0;
  bottom: 0;
  right: 380px;
  margin: auto;
  background: var(--white);
  height: 50px;
  width: 50px;
  border-radius: 50em;
  display: grid;
  place-items: center;
  cursor: pointer;
}

.previous-btn {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 380px;
  margin: auto;
  background: var(--white);
  height: 50px;
  width: 50px;
  border-radius: 50em;
  display: grid;
  place-items: center;
  cursor: pointer;
}
</style>