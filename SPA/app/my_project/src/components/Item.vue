<template>
  <div class="item">
    <p>{{ itemName }}</p>
    <img v-bind:src='img' alt="">
    <input type="number" name="" id="" min="1" v-model="value">
    <span>cena vč DPH {{ price }} czk</span>
    <span>cena bez DPH {{ price - (price*(dph*0.01)) }} czk</span>
    <span>dph: {{ dph }}%</span>
    <button @click="addToCard()">
      <span class="material-symbols-outlined">
        add_shopping_cart
      </span>
    </button>
  </div>
</template>

<script>



export default {
  props: ['itemName', 'price', 'value', 'dph'],


  data() {
    return {
      img: 'https://upload.wikimedia.org/wikipedia/commons/thumb/b/b6/Image_created_with_a_mobile_phone.png/1024px-Image_created_with_a_mobile_phone.png'
    }
  },
  methods: {
    addToCard() {
      // var addToCardEvent = new CustomEvent("addToCard", { detail: {itemName: this.itemName, value: this.value, price: this.price} });
      // window.dispatchEvent(addToCardEvent);
      // this.$root.$children[0].$children[1].$emit("evnt");
      // this.$root.$emit("evnt");
      console.log(this.itemName) ; 
      var evt = new CustomEvent("addToCardEvent", { detail: {itemName: this.itemName, value: this.value, price: this.price, dph: this.dph}});
      window.dispatchEvent(evt);
    }
  }
}
</script>

<style scoped>
.item {
  height: min-content;
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 10em;
  background-color: #00000042;
  border-radius: 0.75em;
}

div> :not(:first-child) {
  margin-top: 1em;
}

img {
  height: 5em;
}

button {
  margin-bottom: 1em;
}

input[type=number] {
  width: 3em;
}

input[type=number]::-webkit-inner-spin-button,
input[type=number]::-webkit-outer-spin-button {
  opacity: 1;
}
</style>