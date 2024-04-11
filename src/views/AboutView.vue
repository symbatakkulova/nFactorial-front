<script>
import axios from "axios";
const host = process.env.VUE_APP_SERVER_HOST;
const port = process.env.VUE_APP_SERVER_PORT;

export default {
  props:["id"],
  data(){
    return{
      info:""
    }
  },
  methods:{
    async getInfo(){
      const url = `http://${host}:${port}/${this.id}`;
      console.log(url);
      try {
        const result = await axios.get(url);
        const a = result.data.find(e=>e.id===this.id*1);
        console.log(result);
        console.log(this.id)
        this.info = result.data;
      } catch (err) {
        console.log(err)
      }
    }
  },
  mounted(){
    this.getInfo()
  }
}
</script>

<template>
  <div class="about">
    <div class="container">
      <div class="title">
        <h1>{{info.title}}</h1>
      </div>
    </div>
  </div>
</template>
