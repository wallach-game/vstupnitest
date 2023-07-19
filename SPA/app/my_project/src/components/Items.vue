<template>
    <div class="items">
        <Item itemName="vec 1" price="10" value="1" dph="15"></Item>
        <Item itemName="vec 2" price="10" value="5" dph="15"></Item>
        <Item itemName="vec 3" price="10" value="1" dph="15"></Item>
        <Item itemName="vec 4" price="10" value="1" dph="15"></Item>
        <Item itemName="vec 5" price="10" value="1" dph="15"></Item>
        <Item itemName="vec 6" price="10" value="1" dph="5"></Item>
        <Item itemName="vec 7" price="10" value="1" dph="15"></Item>
        <Item itemName="vec 8" price="10" value="1" dph="15"></Item>
    </div>
</template>

<script>
import Item from "./Item.vue"
export default {
    

    name: 'Items',

    components: {
        Item
    },

    data() {
        return {
            text: 'test'
        }
    }
,
}
</script>

<style scoped>
.items {
    width: 10em;
    height: min-content;
    width: min-content;
    padding: 1em;


    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    gap: 1em;
}
</style>
