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
          <button class="previous-button" @click="showPreviousPicture">&lt</button>
          <img :src="currentPicture" alt="Preview Picture"/>
          <button class="next-button" @click="showNextPicture">&gt</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "complexModal",
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
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  transition: opacity 0.3s ease, visibility 0.3s ease;
}

.modal-window {
  position: relative;
  background-color: #415a77;
  width: 90%;
  max-width: 900px;
  max-height: 90%;
  overflow-y: auto;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
  animation: modalFadeIn 0.3s forwards;
}

@keyframes modalFadeIn {
  from {
    opacity: 0;
    transform: translateY(-50%);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 20px;
  background-color: #1b263b;
  border-top-left-radius: 5px;
  border-top-right-radius: 5px;
}

.header h1 {
  margin: 0;
  font-size: 1.5rem;
}

.modal-content {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
}

.picture-thumbnails {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 10px;
  padding: 20px;
}

.picture-thumbnails img {
  width: 100px;
  height: 100px;
  cursor: pointer;
}

.picture-thumbnails img:hover {
  border: 1px solid #ffc300;
}

.picture-preview {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 20px;
  overflow: hidden;
  width: 70vw;
  height: auto;
}

.previous-button,
.next-button {
  background-color: transparent;
  border: none;
  color: white;
  font-size: 20px;
  width: 30px;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.previous-button {
  position: absolute;
  left: 0;
}

.next-button {
  position: absolute;
  right: 0;
}

button:hover {
  color: #ffc300;
}

.picture-preview img {
  max-width: 100%;
  max-height: 300px;
  border-radius: 5px;
  object-fit: contain;
  transition: transform 0.3s ease;
}

</style>
