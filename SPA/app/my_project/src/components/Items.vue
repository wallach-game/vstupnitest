<template>
    <div>
        {{ text }}
        <Item></Item>
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
}
</script>

<style scoped>
div {
    border: 1px red solid;
    width: 10em;
    height: 10em;
    display: flex;
    justify-content: center;
    align-items: center;
}
</style>
