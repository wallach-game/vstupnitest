<template>
    <div class="kosikItems">
    </div>
</template>
<script>
import KosikItem from './KosikItem.vue'
import Vue from 'vue'

export default {
    data() {
        return {
            idGen: 0,
            items: []
        };
    },
    mounted() {
        var kosikItems = this;
        // this.$on("evnt", console("picoooo"));
        window.addEventListener("addToCardEvent", function (evt) {
            kosikItems.addItemToCard(evt.detail);
        }, false);

        window.addEventListener("rekapitulaceEvent", function (evt) {
            var evt = new CustomEvent("rekapitulaceDataReturnEvent", { detail: { data: kosikItems.$children , sdph: kosikItems.$parent.celkemsdph , bezdph:kosikItems.$parent.celkembezdph, dph: kosikItems.$parent.celkemdph} });
            window.dispatchEvent(evt);
        }, false);
    },
    name: 'KosikItems',

    components: {
        KosikItem
    },
    methods: {
        addItemToCard(itemData) {
            var ComponentClass = Vue.extend(KosikItem)
            var instance = new ComponentClass()
            instance.$mount();
            instance.itemName = itemData.itemName;
            instance.value = itemData.value;
            instance.price = itemData.price;
            instance.$parent = this;
            this.idGen += 1;
            instance.id = this.idGen;
            this.$children.push(instance);
            this.$el.appendChild(instance.$el);
            this.calcItemsTotal();
        }
        ,
        calcItemsTotal() {
            let celkemsdph = 0;
            let celkembezdph = 0;
            let celkemdph = 0;
            for (let i = 0; i < this.$children.length; i++) {
                const element = this.$children[i];
                celkemsdph += element.calcItemTotal().sdph;
                celkembezdph += element.calcItemTotal().bezdph;
                celkemdph += element.calcItemTotal().dph;
            }
            this.$parent.celkemsdph = celkemsdph;
            this.$parent.celkembezdph = celkembezdph;
            this.$parent.celkemdph = celkemdph;
        }

        ,
        removeItem(id) {
            for (let i = 0; i < this.$children.length; i++) {
                const element = this.$children[i];
                if (element.id === id) {
                    //this.$children.reduce(element);
                    this.$children.splice(i, 1);
                }
            }
        },
    },
}
</script>

<style scoped>
.kosikItems {}
</style>
