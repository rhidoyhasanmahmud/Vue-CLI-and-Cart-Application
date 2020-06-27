<template>
  <div class="col-sm-3">
    <ul class="list-group">
      <li class="list-group-item">
        <span class="item-name">Name</span>
        <span class="item-price float-right">Price</span>
      </li>
      <hr>
      <li v-for="(item, index) in items" :key="index" class="list-group-item">
        <span class="item-name">{{item.title}}</span>
        <button class="btn btn-sm btn-danger" @click="removeItem(index)">X</button>
        <span class="item-price float-right">${{item.price}}</span>
      </li>
      <hr>
      <li class="list-group-item">
        <span class="item-name">Total</span>
        <span class="item-price float-right">${{totalPrice}}</span>
      </li>
    </ul>
  </div>
</template>
<script>
    export default {
        props: ['items'],
        computed: {
            totalPrice(){
                var total = 0;
                this.items.forEach(item=>{
                    console.log(item.price);
                    total += parseFloat(item.price)
                });
                return total
            }
        },
        methods: {
            removeItem(index){
            this.$emit('itemRemoved', index)
            }
        }
    }
</script>
<style>

</style>
