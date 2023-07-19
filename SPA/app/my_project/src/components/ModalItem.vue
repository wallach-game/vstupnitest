<template>
  <div class="modalItem">
    <span>{{ itemName }}</span>
    <span>{{ pocet }}</span>
    <span>{{ cena }}</span>
  </div>
</template>

<script>



export default {
  data() {
    return {
      itemName, 
      pocet, 
      cena
      }
  },
  methods: {
  }
}
</script>

<style scoped>
.modalItem {
}
</style>