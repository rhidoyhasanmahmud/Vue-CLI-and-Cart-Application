<template>
  <div class="col-sm-9">
    <div v-for="(item, index) in items" class="card" style="width: 13rem;">
      <img :src="item.photo" class="card-img-top"
           alt="Alter Image">
      <div class="card-body">
        <h5 class="card-title">{{item.title}}</h5>
        <p class="card-text">${{item.price}}</p>
        <a @click="addToCart(item)" class="btn btn-primary">Add</a>
      </div>
    </div>
  </div>
</template>
<script>
    export default {
        props: ['items'],
        methods: {
            addToCart(item){
                this.$emit('newItemAdded', item)
            }
        }
    }
</script>
<style>

</style>
