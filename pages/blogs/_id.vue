<template>
  <div class="container mt-5">
    <div class="card">
      <div class="card-body">
        <h1>{{articulo.title}}</h1>
        <p class="small">{{articulo.nombreAutor}}</p>
        <p>{{articulo.body}}</p>
        <nuxt-link to="/blogs" class="btn btn-primary">Atras</nuxt-link>
      </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  name: "",
  data: () => ({

  }),
  // async created(){
  //   try {
  //     const res = await axios.get(`https://jsonplaceholder.typicode.com/posts/${this.$route.params.id}`)
  //     // console.log(res.data);
  //     this.articulo = res.data;
  //
  //     const resAutor = await axios.get(`https://jsonplaceholder.typicode.com/users/${res.data.userId}`)
  //     this.articulo.nombreAutor = resAutor.data.name;
  //   } catch (e) {
  //     console.log(e);
  //   }
  // },
  async asyncData({isDev, route, store, env, params, query, req, res, redirect, error}){
    try {
      const res = await axios.get(`https://jsonplaceholder.typicode.com/posts/${params.id}`)
      // console.log(res.data);
      const articulo = res.data;

      const resAutor = await axios.get(`https://jsonplaceholder.typicode.com/users/${res.data.userId}`)
      articulo.nombreAutor = resAutor.data.name;

      return {articulo};
    } catch (e) {
      console.log(e);
      return {error: e}
    }
  },
}
</script>
<style lang="scss" scoped>
</style>
