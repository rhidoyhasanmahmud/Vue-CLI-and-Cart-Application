<template>
  <div v-if="!loading" class="col-sm-9">
    <div v-for="(item, index) in items" class="card" style="width: 13rem;">
      <router-link tag="div" :to="{path: '/item/' + item.id}">
        <img :src="item.photo" class="card-img-top"
             alt="Alter Image">
        <div class="card-body">
          <h5 class="card-title">{{item.title}}</h5>
        </div>
      </router-link>
      <div class="card-footer">
          <p class="card-text">${{item.price}}</p>
          <a @click="addToCart(item)" class="btn btn-primary">Add</a>
      </div>
    </div>
  </div>
  <h1 v-else>Loading...</h1>
</template>
<script>
  import axios from 'axios'
    export default {
        // props: ['items'],
        data() {
          return {
              loading: true,
              // items: ''
          }
        },
        computed: {
          items() {
              return this.$store.getters.getInventory
          }
        },
        mounted() {
            this.fetchInventory()
        },
        methods: {
            addToCart(item){
                // this.$emit('newItemAdded', item)
                // this.$store.commit('addToCart', item) // call mutation
                this.$store.dispatch('addToCart', item) // call action
            },
            fetchInventory(){
                var self = this;
                axios.get('http://localhost:3000/items').then(response => {
                    // console.log(response);
                    // this.items = response.data;
                    self.$store.commit('setInventory', response.data)
                    self.loading = false
                })
            }
        }
    }
</script>
<style>

</style>
