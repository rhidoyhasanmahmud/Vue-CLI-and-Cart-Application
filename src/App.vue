<template>
  <div id="app">

<!--    <router-link :to="{path: '/'}">Home</router-link>-->
<!--    <router-link :to="{path: '/test/1'}">Test 1</router-link>-->
<!--    <router-link :to="{path: '/test/2'}">Test 2</router-link>-->
<!--    <router-link :to="{path: '/test/3'}">Test 3</router-link>-->
<!--    <router-view></router-view>-->

    <navbar @search="search"></navbar>
    <div class="container">
      <div class="row">
        <router-view></router-view>

<!--        <inventory @newItemAdded="addCartItem" :items="items"></inventory>-->

        <cart :items="cart" @itemRemoved="removeItem"></cart>
      </div>
    </div>
  </div>
</template>

<script>
    import Navbar from "./components/Navbar";
    import Cart from "./components/Cart";
    import Inventory from "./components/views/Inventory";
    import data from "./data";

    export default {
        components: {
            Navbar,
            Cart,
            Inventory
        },
        data(){
            return {
                items: [],
                cart: [
                  //   {
                  //   id: 1,
                  //   title: 'test',
                  //   price: 10.30,
                  //   photo: "http://dummyimage.com/240x245.png/5fa2dd/ffffff"
                  // }
                ]
            }
        },
        mounted() {
           this.items = data
        },
        methods: {
            search(keyword){
              this.items = data.filter(item=>{
                  return item.title.toLowerCase().indexOf(keyword.toLowerCase()) !== -1
              })
            },
            addCartItem(item){
                this.cart.push(item)
            },
            removeItem(index){
                this.cart.splice(index,1)
            }
        }
    }
</script>

<style>
  .container {
    padding-top: 10px;
  }
</style>
