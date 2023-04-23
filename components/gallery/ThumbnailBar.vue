<template>
  <div class="thumbnail-bar">
    <img :src="item" v-for="(item, index) in images" :key="index" class="image" @click="sendImage(item)">
  </div>
</template>

<script>
export default {
  name: 'ThumbnailBar',
  props: {
    images: {
      type: Array,
      default: () => []
    }
  },

  methods: {
    sendImage(url) {
      this.$emit('selectedImg', url)
    }
  }
}
</script>
<style scoped>
.thumbnail-bar {
  margin-top: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.image {
  width: 150px;
  height: 150px;
  padding: 10px 5px;
  cursor: pointer;
}

.image:hover {
  border: 1px solid #ffc300;
}
</style>
