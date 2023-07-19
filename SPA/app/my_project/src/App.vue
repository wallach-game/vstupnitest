<template>
  <div id="app">
    <Modal></Modal>
    <Items>
    </Items>

    <Kosik></Kosik>
    <!-- <img src="./assets/logo.png"> -->
    <!-- <router-view/> -->
    <Form></Form>
  </div>
</template>

<script>
import Items from "./components/Items.vue";
import Kosik from "./components/Kosik.vue";
import Form from "./components/Form.vue";
import Modal from "./components/Modal.vue";

export default {
  name: 'App',
  components: {
    Items,
    Kosik,
    Form,
    Modal
  }
};
</script>

<style>
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
}


#app>* {
  margin-top: 1em;
}
</style>
