<template>
  <div class="images">
    <img
      @click="showDesktopCarousel"
      v-show="imageId == 'thumbnail-1'"
      class="big-image"
      src="../assets/image-product-1.jpg"
      alt="bigImage"
    />
    <img
      @click="showDesktopCarousel"
      v-show="imageId == 'thumbnail-2'"
      class="big-image"
      src="../assets/image-product-2.jpg"
      alt="bigImage"
    />
    <img
      @click="showDesktopCarousel"
      v-show="imageId == 'thumbnail-3'"
      class="big-image"
      src="../assets/image-product-3.jpg"
      alt="bigImage"
    />
    <img
      @click="showDesktopCarousel"
      v-show="imageId == 'thumbnail-4'"
      class="big-image"
      src="../assets/image-product-4.jpg"
      alt="bigImage"
    />

    <div class="images-list">
      <div id="thumbnail-1" class="img">
        <img
          @click="chooseImage"
          class="thumbnail"
          src="../assets/image-product-1-thumbnail.jpg"
          alt="thumbnail-1"
        />
      </div>
      <div id="thumbnail-2" class="img">
        <img
          @click="chooseImage"
          class="thumbnail"
          src="../assets/image-product-2-thumbnail.jpg"
          alt="thumbnail-2"
        />
      </div>
      <div id="thumbnail-3" class="img">
        <img
          @click="chooseImage"
          class="thumbnail"
          src="../assets/image-product-3-thumbnail.jpg"
          alt="thumbnail-3"
        />
      </div>
      <div id="thumbnail-4" class="img">
        <img
          @click="chooseImage"
          class="thumbnail"
          src="../assets/image-product-4-thumbnail.jpg"
          alt="thumbnail-4"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      imageId: "thumbnail-1",
    };
  },
  methods: {
    setClass(images) {
      images.forEach((e) => {
        if (e.classList.contains("selected-image") && e.id != this.imageId) {
          e.classList.remove("selected-image");
        } else if (e.id == this.imageId) {
          e.classList.add("selected-image");
        }
      });
    },
    chooseImage(e) {
      this.imageId = e.path[1].id;

      let images = document.querySelectorAll(".img");
      this.setClass(images);
    },
    showDesktopCarousel() {
      this.$emit("changeDesktopCarouselStatus", true);
    },
  },
  mounted() {
    document.getElementById("thumbnail-1").classList.add("selected-image");
  },
};
</script>

<style lang="scss">
.images {
  width: 100%;
  padding: 4rem 2.5rem;
  // padding: 5rem 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  .big-image {
    width: 380px;
    height: 350px;
    border-radius: 10px;
    cursor: pointer;
  }

  .images-list {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    margin: 2.4rem 0;

    .img {
      width: 70px;
      height: 70px;
      display: flex;
      justify-content: center;
      align-items: center;
      border-radius: 10px;
      // overflow: hidden;
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

.selected-image {
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