<template>
  <div class="bigImg">
    <img :src="image" class="img-item" @click="showModal"/>
  </div>
</template>

<script>
export default {
  name: 'BigImg',
  props: {
    image: {
      type: String,
      default: () => ''
    }
  },

  methods: {
    showModal() {
      this.$emit('rm', true)
    }
  }
}
</script>
<style scoped>
.bigImg {
  display: flex;
  justify-content: center;
}

.img-item {
  max-height: 350px;
  cursor: pointer;
}

</style>
