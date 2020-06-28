<template>
  <div v-if="item" class="row">
      <div class="col-sm-6">
        <img :src="item.photo" alt="photo">
      </div>
    <div class="col-sm-6">
      <h4>{{item.title}}</h4>
      <h4>{{item.description}}</h4>
      <div class="cart-footer">
      <span>${{item.price}}</span>
        <button @click="addToCart(item)" class="btn btn-primary">Add</button>
      </div>
    </div>
  </div>
  <h3 v-else>Nothing</h3>
</template>
<script>
    import axios from "axios"

    export default {
        data() {
            return {
                item: null
            }
        },
        mounted(){
          this.fetchItem()
        },
        methods: {
            fetchItem() {
                var self = this
                axios.get('http://localhost:3000/item/' + this.$route.params.id).then(response => {
                  self.item = response.data
                })
            },
            addToCart(item){
                this.$store.commit('addToCart', item)
            }
        }
    }
</script>
<style>

</style>
