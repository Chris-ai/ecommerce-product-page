<template>
  <div class="images-desktop">
    <div class="desktop-big-image-wrapper">
      <img
        v-show="imageId == 'desktop-thumbnail-1'"
        class="desktop-big-image"
        src="../assets/image-product-1.jpg"
        alt="desktopBigImage"
      />
      <img
        v-show="imageId == 'desktop-thumbnail-2'"
        class="desktop-big-image"
        src="../assets/image-product-2.jpg"
        alt="desktopBigImage"
      />
      <img
        v-show="imageId == 'desktop-thumbnail-3'"
        class="desktop-big-image"
        src="../assets/image-product-3.jpg"
        alt="desktopBigImage"
      />
      <img
        v-show="imageId == 'desktop-thumbnail-4'"
        class="desktop-big-image"
        src="../assets/image-product-4.jpg"
        alt="desktopBigImage"
      />

      <div @click="closeDesktopCarousel" class="close-desktop-carousel">
        <img src="../assets/orange-icon-close.svg" alt="closeDesktopCarousel" />
      </div>

      <div @click="nextItem" class="change-img-btn right">
        <img src="../assets/icon-next.svg" alt="nextItem" />
      </div>

      <div @click="previousItem" class="change-img-btn left">
        <img src="../assets/icon-previous.svg" alt="previousItem" />
      </div>
    </div>

    <div class="images-desktop-list">
      <div id="desktop-thumbnail-1" class="desktop-img">
        <img
          @click="chooseImage"
          class="thumbnail"
          src="../assets/image-product-1-thumbnail.jpg"
          alt="desktop-thumbnail-1"
        />
      </div>
      <div id="desktop-thumbnail-2" class="desktop-img">
        <img
          @click="chooseImage"
          class="thumbnail"
          src="../assets/image-product-2-thumbnail.jpg"
          alt="desktop-thumbnail-2"
        />
      </div>
      <div id="desktop-thumbnail-3" class="desktop-img">
        <img
          @click="chooseImage"
          class="thumbnail"
          src="../assets/image-product-3-thumbnail.jpg"
          alt="desktop-thumbnail-3"
        />
      </div>
      <div id="desktop-thumbnail-4" class="desktop-img">
        <img
          @click="chooseImage"
          class="thumbnail"
          src="../assets/image-product-4-thumbnail.jpg"
          alt="desktop-thumbnail-4"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      imageId: "desktop-thumbnail-1",
      imageIdNumber: 1,
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
      this.imageId = e.path[1].id;
      this.imageIdNumber = this.imageId.slice(-1);
      console.log(e);

      let images = document.querySelectorAll(".desktop-img");
      this.setClass(images);
    },

    nextItem() {
      if (this.imageIdNumber < 4) {
        this.imageIdNumber++;
        this.imageId = `desktop-thumbnail-${this.imageIdNumber}`;
        this.setClass(document.querySelectorAll(".desktop-img"));
      } else {
        console.log("This is the last one :/");
      }
    },
    previousItem() {
      if (this.imageIdNumber > 1) {
        this.imageIdNumber--;
        this.imageId = `desktop-thumbnail-${this.imageIdNumber}`;
        this.setClass(document.querySelectorAll(".desktop-img"));
      } else {
        console.log("You're at the start of the carousel :)");
      }
    },
    closeDesktopCarousel() {
      this.$emit("desktopCarouselState", false);
    },
  },
  mounted() {
    document
      .getElementById(this.imageId)
      .classList.add("desktop-selected-image");

    document
      .querySelector(".desktop-big-image")
      .addEventListener("click", () => {
        this.$emit("changeDesktopCarouselStatus", true);
      });
  },
};
</script>

<style lang="scss">
.images-desktop {
  width: 100%;
  padding: 4rem 2.5rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  .desktop-big-image {
    width: 380px;
    height: 350px;
    border-radius: 10px;
    cursor: pointer;
  }

  .images-desktop-list {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    margin: 2.4rem 0;

    .desktop-img {
      width: 70px;
      height: 70px;
      display: flex;
      justify-content: center;
      align-items: center;
      border-radius: 10px;
      margin: 0 1rem;

      img {
        width: 70px;
        height: 70px;
        border-radius: 10px;
        cursor: pointer;
      }

      &:hover {
        img {
          opacity: 0.5;
        }
      }
    }
  }
}

.desktop-big-image-wrapper {
  position: relative;
}

.close-desktop-carousel {
  position: absolute;
  top: -40px;
  right: 0;
  padding: 0 0.7rem;
  cursor: pointer;
  img {
    height: 150%;
    width: 150%;
  }
}
.change-img-btn {
  height: 50px;
  width: 50px;
  border-radius: 50em;
  background: var(--white);
  display: grid;
  place-items: center;
  position: absolute;
  top: 0;
  bottom: 0;
  margin: auto;
  cursor: pointer;
}

.left {
  left: -25px;
}

.right {
  right: -25px;
}
.desktop-selected-image {
  position: relative;
  &::after {
    border-radius: 10px;
    position: absolute;
    content: "";
    width: 100%;
    height: 100%;
    background: rgba($color: #fff, $alpha: 0.8);
    outline: 2px solid var(--orange);
    cursor: pointer;
  }
}
</style>