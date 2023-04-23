<template>
  <div class="modal" v-if='showModal'>
    <div class="modal-window">
      <div class="header">
        <h1>Preview</h1>
        <span @click="closeModal">Close</span>
      </div>
      <div class="modal-content">
        <div class="picture-thumbnails">
          <img
            v-for="(picture, index) in pictures"
            :key="index"
            :src="picture"
            @click="setCurrentPicture(index)"
            alt="Thumbnail Picture"
          />
        </div>
        <div class="picture-preview">
          <div class="preview-content">
            <img :src="currentPicture" alt="Preview Picture"/>
            <button class="previous-button" @click="showPreviousPicture">Previous</button>
            <button class="next-button" @click="showNextPicture">Next</button>
          </div>
          <button class="close-button" @click="closeModal">Close</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "complexmodal",
  data() {
    return {
      pictures: [],
      showModal: false,
      currentPictureIndex: 0,
    };
  },
  computed: {
    currentPicture() {
      return this.pictures[this.currentPictureIndex];
    },
  },
  created() {
    this.$nuxt.$on('showComplexModal', (pictures, currentPictureIndex) => {
      this.showModal = true;
      this.pictures = pictures;
      this.currentPictureIndex = currentPictureIndex;
    });
  },
  methods: {
    setCurrentPicture(index) {
      this.currentPictureIndex = index;
    },
    showPreviousPicture() {
      if (this.currentPictureIndex > 0) {
        this.currentPictureIndex--;
      } else {
        this.currentPictureIndex = this.pictures.length - 1;
      }
    },
    showNextPicture() {
      if (this.currentPictureIndex < this.pictures.length - 1) {
        this.currentPictureIndex++;
      } else {
        this.currentPictureIndex = 0;
      }
    },
    closeModal() {
      this.showModal = false;
    },
  },
}
</script>

<style scoped>

</style>
