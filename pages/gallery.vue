<template>
  <div class="gallery">
    <BigImg :image="img" @rm="runModal($event)"/>
    <ThumbnailBar :images="items" @selectedImg="showImg($event)"/>
    <Modal v-show="showModal" :image="img" @closeModel="runModal($event)"/>
  </div>
</template>

<script>
import ThumbnailBar from '../components/gallery/ThumbnailBar.vue'
import BigImg from "~/components/gallery/BigImg.vue";
import Modal from "~/components/modals/modal.vue";

export default {
  name: 'GalleryPage',
  components: {BigImg, ThumbnailBar, Modal},
  data() {
    return {
      items: [
        'https://cdn.pixabay.com/photo/2018/12/15/00/05/winter-3876098_960_720.jpg',
        'https://cdn.pixabay.com/photo/2023/03/25/19/12/butterfly-7876680_960_720.jpg',
        'https://cdn.pixabay.com/photo/2017/10/02/21/56/dog-2810484_960_720.jpg',
        'https://cdn.pixabay.com/photo/2019/10/05/19/40/pumpkins-4528653_960_720.jpg',
        'https://cdn.pixabay.com/photo/2023/01/16/18/52/cupcake-7723091_960_720.jpg',
        'https://cdn.pixabay.com/photo/2017/01/11/11/33/cake-1971552_960_720.jpg',
        'https://cdn.pixabay.com/photo/2022/10/22/19/11/acorns-7539907_960_720.jpg',
        'https://cdn.pixabay.com/photo/2018/01/11/21/27/carnival-3076952_960_720.jpg'
      ],

      img: 'https://cdn.pixabay.com/photo/2018/12/15/00/05/winter-3876098_960_720.jpg',
      showModal: false
    }
  },

  methods: {
    showImg(url) {
      this.img = url
    },
    runModal(e) {
      this.showModal = e
    }
  }
}
</script>
<style scoped>
.gallery {
  background-color: #415a77;
}
</style>
