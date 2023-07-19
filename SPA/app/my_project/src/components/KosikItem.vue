<template>
  <div class="kosikItem">
    <span>{{ itemName }}</span>
    <span>{{ price }}</span>
    <span class="material-symbols-outlined" v-on:click="removeItem()">
      delete
    </span>
    <input type="number" name="" id="" v-model="value" min="1" v-on:click="callbackCallTotal()">
  </div>
</template>

<script>
export default {
  data() {
    return {
      itemName: 'jmeno',
      value: 1,
      price: 10,
      dph: 15,
      id: 0
    }
  }
  ,
  methods: {

    callbackCallTotal() {
      this.$parent.calcItemsTotal();
    }
    ,
    calcItemTotal() {
      return {sdph: this.value * this.price,bezdph: this.value * this.price - (this.price*(this.dph*0.01)), dph: this.value * this.price*(this.dph*0.01) };
    },
    removeItem() {
    this.$parent.removeItem(this.id);
    this.callbackCallTotal();
    this.$el.remove();
  }
  },
  
}
</script>

<style scoped>
input[type=number] {
  width: 3em;
}

input[type=number]::-webkit-inner-spin-button,
input[type=number]::-webkit-outer-spin-button {
  opacity: 1;
}

.kosikItem {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  width: 10em;
}
</style>