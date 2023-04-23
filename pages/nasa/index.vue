<template>
  <div class="center">
    <h1>Nasa - {{ currentCollectionName }}</h1>
    <input v-model="query" placeholder="Search...">
    <button @click="$event=>find()">Search</button>
    <div class="images">
      <template v-for="value in dataArray">
        <template v-for="(link, index) in value.links">
          <img class="image" v-if="index === 0" :data-index="index" :src="link.href" alt="Image from Nasa" @click="showModal(link.href)"/>
        </template>
      </template>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "index",

  created() {
    this.fetchData("sun");
  },

  data() {
    return {
      dataArray: [],
      query: "",
      currentCollectionName: ""
    }
  },

  methods: {
    find() {
      this.fetchData(this.query);
    },
    async fetchData(query) {
      await axios.get('https://images-api.nasa.gov/search?q=' + query)
        .then(response => {
          let images = response.data.collection.items;
          console.log(images);
          this.dataArray = images;
          this.currentCollectionName = query;
          this.query = "";

        })
        .catch(error => {
          console.log(error);
        })
    },
    showModal(imageUrl) {
      console.log(imageUrl);
      this.$nuxt.$emit('showModal', imageUrl);
    },
  }
}
</script>

<style scoped>
.images {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  justify-content: center;
}

img {
  width: 100px;
  height: 100px;
  object-fit: cover;
  padding: 5px;
  cursor: pointer;
}

.center {
  display: flex;
  flex-direction: column;
  align-items: center;
}

input {
  padding: 10px;
  width: 300px;
  font-size: 16px;
  background-color: #1b263b;
  border-radius: 4px;
  margin-bottom: 10px;
  outline: none;
  border: 1px solid #1b263b;
}

input:hover {
  border-color: #ffc300;
}

input:focus {
  border-color: #38b000;
}

button {
  padding: 10px 20px;
  font-size: 16px;
  background-color: #1b263b;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #ffc300;
}

.image:hover {
  border: 1px solid #ffc300;
}

</style>
