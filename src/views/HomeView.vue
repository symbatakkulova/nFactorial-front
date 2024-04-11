<script>
import axios from "axios";
const host = process.env.VUE_APP_SERVER_HOST;
const port = process.env.VUE_APP_SERVER_PORT;
const url = `http://${host}:${port}/`
export default {
  data() {
    return {
      list: []
    }

  },
  methods: {
    async getList() {
      try {
        const result = await axios.get(url);
        console.log(result);
        this.list = result.data;
      } catch (err) {
        console.log(err)
      }

    }


  },
  mounted() {

    this.getList()
  }
}
</script>
<template>
  <main>
    <div class="title">
      <h1>Tengri News</h1>
    </div>
    <div class="container">
      <div class="news">
        <div v-for="i in list" :key="i.id" class="new">
          <router-link :to="{ name: 'about', params: { id: i.id } }">
            <div class="new-title">{{ i.title }}</div>
            <div class="image">
              <img :src="i.img" alt="">
            </div>
            <div class="date">
              {{ i.date }}
            </div>
          </router-link>
        </div>
      </div>
    </div>
  </main>
</template>
<style lang="css" scoped>
* {
  margin: 0;
}

.title {
  margin: 0;
  padding: 1rem;
  background-color: green;
  color: white;
  text-align: center;
}

.container {
  width: 100%;
  height: 100%;
}

.news {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

.new {
  width: 20%;
  text-align: center;
  margin: 1rem;
  padding: 1rem;
  border: 1px solid black;

}

.image img {
  width: 100%;
  height: 20%;
}</style>