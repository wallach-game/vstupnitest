<template>
  <div>
    <!-- <img v-bind:src='img' alt=""> -->
    {{ msg }}
  </div>
</template>

<script>
export default {
  name: 'Item',
  data () {
    return {
      msg: 'helppp',
      // img: 'https://upload.wikimedia.org/wikipedia/commons/thumb/b/b6/Image_created_with_a_mobile_phone.png/1024px-Image_created_with_a_mobile_phone.png'
    }
  }
}
</script>

<style scoped>



</style>