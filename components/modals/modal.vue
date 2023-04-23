<template>
  <div class="modal" v-if='showModal'>
    <div class="modal-window">
      <div class="header">
        <h1>Preview</h1>
        <span @click="closeModal">Close</span>
      </div>
      <div class="modal-content">
        <img :src="this.imageUrl">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  data() {
    return {
      showModal: false,
      imageUrl: ''
    }
  },
  created() {
    this.$nuxt.$on('showModal', (url) => {
      this.showModal = true;
      this.imageUrl = url;
    });
  },
  methods: {
    closeModal() {
      this.showModal = false;
    },
  }
}
</script>
<style scoped>
.modal {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 9999;
  transition: opacity 0.3s ease, visibility 0s linear 0.3s;
}

.modal-window {
  max-width: 600px;
  width: 80%;
  background-color: #415a77;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  animation: modal-anim 0.3s ease-out;
}

@keyframes modal-anim {
  0% {
    transform: scale(0.8);
    opacity: 0;
  }
  100% {
    transform: scale(1);
    opacity: 1;
  }
}

.modal .header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  background-color: #1b263b;
  border-radius: 10px 10px 0 0;
}

.modal .header h1 {
  margin: 0;
}

.modal .header span {
  cursor: pointer;
}

.modal .modal-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
}

.modal .modal-content img {
  max-width: 100%;
  max-height: 100%;
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
}
</style>
