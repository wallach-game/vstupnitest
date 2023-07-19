<template>
    <div class="modal-wrapper" v-bind:class="open ? '' : 'closed'">
        <div class="modal" v-bind:class="open ? '' : 'closed'">
            <div class="buttonWrapper"><span class="closebtn" v-on:click="changeModalState()">❌</span>
            </div>
                <div>
                </div>
                <br>
                <div>
                    <span>v CZK</span>
                    <br><br>
                    <span>Celkem s DPH {{ sdph }}</span>
                    <br>
                    <span>Celkem bez DPH {{ bezdph }}</span>
                    <br>
                    <span>DPH {{ dph }}</span>
                    <br>
                    <br>
                    <span>v Eur</span>
                    <br>
                    <br>
                    <span>Celkem s DPH {{ (sdph / hodnotaEuro).toFixed(2) }}</span>
                    <br>
                    <span>Celkem bez DPH {{ (bezdph / hodnotaEuro).toFixed(2) }}</span>
                    <br>
                    <span>DPH {{ (dph / hodnotaEuro).toFixed(2) }}</span>
                </div>
                <br>
                <div>
                    <span>Jmeno: {{ jmeno }}</span><br>
                    <span>Prijmeni: {{ prijmeni }}</span><br>
                    <span>Tel: {{ telefon }}</span><br>
                    <span>Email: {{ email }}</span><br>
                    <span>Psc: {{ psc }}</span><br>
                    <span>Ulice: {{ ulice }}</span><br>
                    <span>Mesto: {{ mesto }}</span><br>
                </div>
            </div>
        </div>
</template>

<script>
import ModalItem from './ModalItem.vue'
import Vue from 'vue';

export default {
    name: 'Modal',


    components: {
        ModalItem
    },

    data() {
        return {
            open: false,
            sdph: 0,
            dph: 0,
            bezdph: 0,
            hodnotaEuro: 0,
            jmeno: '',
            prijmeni: '',
            telefon: '',
            email: '',
            psc: '',
            ulice: '',
            mesto: '',

        }
    },

    methods: {
        changeModalState() {
            console.log("closing");
            this.open = !this.open;
        },

        addItemToModal(itemData) {
            var ComponentClass = Vue.extend(ModalItem)
            var instance = new ComponentClass()

            instance.itemName = itemData.itemName;
            instance.pocet = itemData.value;
            instance.cena = itemData.price;
            instance.$mount();
            instance.$parent = this;
            this.$children.push(instance);
            // console.log(instance);
            // console.log(this.$el.childNodes[0].childNodes);
            this.$el.childNodes[0].childNodes[2].appendChild(instance.$el);
        },

        async loadKurzy(dnes, modal) {
            const url = 'https://corsproxy.io/?' + encodeURIComponent(`https://www.cnb.cz/cs/financni-trhy/devizovy-trh/kurzy-devizoveho-trhu/kurzy-devizoveho-trhu/denni_kurz.txt?date=${dnes}`);
            const response = await fetch(url);
            const movies = await response.text();
            let radky = movies.split("\n");
            let eura = radky[7].split("|");
            eura = eura[4];
            console.log(eura);
            eura = eura.replace(",", ".");
            console.log(parseFloat(eura));
            modal.hodnotaEuro = parseFloat(eura);
        }
    }
    , mounted() {
        // this.$on("evnt", console("picoooo"));
        var modal = this;
        window.addEventListener("rekapitulaceEvent", function (evt) {
            modal.jmeno = evt.detail.jmeno;
            modal.prijmeni = evt.detail.prijmeni;
            modal.telefon = evt.detail.telefon;
            modal.email = evt.detail.email;
            modal.psc = evt.detail.psc;
            modal.ulice = evt.detail.ulice;
            modal.mesto = evt.detail.mesto;
            modal.changeModalState();
        }, false);

        window.addEventListener("rekapitulaceDataReturnEvent", function (evt) {
            modal.$el.childNodes[0].childNodes[2].innerHTML = "";
            console.log(evt.detail);
            modal.sdph = evt.detail.sdph;
            modal.dph = evt.detail.dph;
            modal.bezdph = evt.detail.bezdph;

            console.log(modal);

            for (let i = 0; i < evt.detail.data.length; i++) {
                const element = evt.detail.data[i];
                modal.addItemToModal(element);
            }
        }, false);


        let dnes = new Date().toLocaleDateString('en-GB');

        this.loadKurzy(dnes, this);

    }
}
</script>

<style scoped>
.modal-wrapper {
    position: absolute;
    z-index: 2;
    /* background-color: blue; */
    width: 100vw;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}


.modal {
    background-color: #dddddde3;
    border-radius: 1em;
    width: 50vw;
    height: 50vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: start;
    margin: 0;
    overflow: scroll;;
}

.buttonWrapper {
    margin-top: 1em;
    width: calc(100% - 1.9em);
    height: min-content;
    display: flex;
    justify-content: flex-end;
}

.closebtn {}

.closed {
    display: none !important;
}

span {
    margin-top: 0.5em;
    margin-bottom: 0.5em;
}
</style>
