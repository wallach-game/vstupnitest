<template>
  <div id="app">
    <Items>
    </Items>
    <!-- <img src="./assets/logo.png"> -->
    <!-- <router-view/> -->

  </div>
</template>

<script>
import Items from "./components/Items.vue";
import Item from "./components/Item.vue"

export default {
  name: 'App',
  components: {
    "Items" : Items,
    "Item" : Item
  }
};
</script>

<style>
#app {
  /* font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px; */

  display: flex;
  justify-content: center;
}
</style>
