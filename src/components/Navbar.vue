<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <router-link class="navbar-brand" :to="{path: '/'}">Super Store</router-link>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent"
            aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>

    <div class="collapse navbar-collapse" id="navbarSupportedContent">

      <form @submit.prevent="search" class="form-inline my-2 my-lg-0">
        <input v-model="keyword" class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
        <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
      </form>
    </div>
  </nav>
</template>
<script>
  import axios from 'axios'
    export default {
        data() {
            return {
                keyword: ''
            }
        },
        methods: {
            search() {
                var self = this
                // this.$emit('search', this.keyword)
                axios.get('http://localhost:3000/search/' + this.keyword).then(response => {
                    // console.log(response.data)
                    self.$store.commit('setInventory', response.data)
                })
            }
        }
    }
</script>
<style>

</style>
