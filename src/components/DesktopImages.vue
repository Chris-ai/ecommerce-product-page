<template>
  <div class="images">
    <img
      v-show="imageId == 1"
      class="big-image"
      src="../assets/image-product-1.jpg"
      alt="bigImage"
    />
    <img
      v-show="imageId == 2"
      class="big-image"
      src="../assets/image-product-2.jpg"
      alt="bigImage"
    />
    <img
      v-show="imageId == 3"
      class="big-image"
      src="../assets/image-product-3.jpg"
      alt="bigImage"
    />
    <img
      v-show="imageId == 4"
      class="big-image"
      src="../assets/image-product-4.jpg"
      alt="bigImage"
    />

    <div class="images-list">
      <img
        @click="chooseImage"
        id="1"
        class="thumbnail"
        src="../assets/image-product-1-thumbnail.jpg"
        alt=""
      />
      <img
        @click="chooseImage"
        id="2"
        class="thumbnail"
        src="../assets/image-product-2-thumbnail.jpg"
        alt=""
      />
      <img
        @click="chooseImage"
        id="3"
        class="thumbnail"
        src="../assets/image-product-3-thumbnail.jpg"
        alt=""
      />
      <img
        @click="chooseImage"
        id="4"
        class="thumbnail"
        src="../assets/image-product-4-thumbnail.jpg"
        alt=""
      />
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
        if (e.classList.contains("selected-image") && e.id != this.imageId) {
          e.classList.remove("selected-image");
        } else if (e.id == this.imageId) {
          e.classList.add("selected-image");
        }
      });
    },
    chooseImage(e) {
      // console.log(e.path[0].id);
      this.imageId = e.path[0].id;

      let images = document.querySelectorAll(".thumbnail");
      this.setClass(images);
    },
  },
  mounted() {
    document.getElementById('1').classList.add('selected-image')

    document.querySelector('.big-image').addEventListener("click", () => {
      this.$emit("changeDesktopCarouselStatus", true);
    })
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
    img {
      width: 70px;
      height: 70px;
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

.selected-image {
  opacity: 0.5;
  outline: 3px solid var(--orange);
}
</style>