<template>
    <div class="form">
        <span>Jmeno: </span>
        <input type="text" v-on:change="idValidInputUnicode(jmeno, /^[a-zA-Z0-9]+$/, 'vJmeno')" v-model="jmeno"
            v-bind:class="(vJmeno) ? '' : 'spatnyVstup'">
        <span>Primeni: </span>
        <input type="text" v-on:change="idValidInputUnicode(prijmeni, /^[a-zA-Z0-9]+$/, 'vPrijmeni')" v-model="prijmeni"
            v-bind:class="(vPrijmeni) ? '' : 'spatnyVstup'">
        <span>tel: </span>
        <div><select name="" id=""  v-model="predvolba">
                <option value="+420">+420 🇨🇿</option>
            </select>
            <input type="text" name="" id="" v-on:change="isValidInput(phoneNumber, /^(?![+]420)\d{9}$/, 'vPhoneNumber')"
                v-model="phoneNumber" v-bind:class="vPhoneNumber ? '' : 'spatnyVstup'">
        </div>
        <span>email: </span>
        <input type="text" v-model="email" v-on:change="isValidInput(email, /[a-z0-9]+@[a-z]+\.[a-z]{2,3}$/, 'vEmail')"
            v-bind:class="(vEmail) ? '' : 'spatnyVstup'">
        <span>psc: </span>
        <input type="text" v-on:change="isValidInput(psc, /^[1-7]\d{2}(?:\s?\d{2})?$/, 'vPsc')" v-model="psc"
            v-bind:class="(vPsc) ? '' : 'spatnyVstup'">
        <span>Ulice: </span>
        <input type="text" v-on:change="idValidInputUnicode(ulice, /^(?=.*\d)[\da-zA-Z\s\-.,]+$/, 'vUlice')" v-model="ulice"
            v-bind:class="(vUlice) ? '' : 'spatnyVstup'">
        <span>Mesto: </span>
        <input type="text" v-on:change="idValidInputUnicode(mesto, /^[a-zA-Z0-9]+$/, 'vMesto')" v-model="mesto"
            v-bind:class="(vMesto) ? '' : 'spatnyVstup'">
        <span>Odeslat</span>
        <input type="submit" value="Rekapitulace" v-on:click="rekapitulace()">
    </div>
</template>

<script>
export default {
    name: 'Form',

    components: {
    },

    data() {
        return {
            psc: '',
            vPsc: false,
            phoneNumber: '',
            vPhoneNumber: false,
            email: '',
            vEmail: false,
            ulice,
            vUlice,
            jmeno,
            vJmeno,
            prijmeni,
            vPrijmeni,
            mesto,
            vMesto,
            predvolba:  '+420'
        }
    }
    ,
    mounted() {
        this.isPsc = false;

        
    },
    methods: {
        isValidInput(input, redex, key) {
            console.log({ input, redex, key });
            this[key] = redex.test(input);
            console.log(redex.test(input));
            this.$forceUpdate();
        }
        ,
        idValidInputUnicode(input, redex, key) {
            console.log(input);
            //prevert UNI na ASCII
            let uni = ['ě', 'š', 'č', 'ř', 'ž', 'ý', 'á', 'í', 'é', 'ů', 'ú'];
            let ascii = ['e', 's', 'c', 'r', 'z', 'y', 'a', 'i', 'e', 'u', 'u'];
            let convert = input.toLowerCase();
            convert = convert.split('');
            //cyklus
            for (let i = 0; i < convert.length; i++) {
                for (let j = 0; j < uni.length; j++) {
                    if (convert[i] == uni[j]) {

                        convert[i] = ascii[j];

                    }
                }
            }


            let out = "";
            for (let i = 0; i < convert.length; i++) {
                out += convert[i];
            }

            // console.log(out);

            //redex kontrola
            // let redex = /^(?=.*\d)[\da-zA-Z\s\-.,]+$/; redex pro ulici 
            redex.test(out)
            // console.log(redex.test(out));
            this[key] = redex.test(out);
            console.log(redex.test(out));
            this.$forceUpdate();
        },
        rekapitulace() {
            let telefon = this.predvolba + this.phoneNumber;
            console.log(telefon);
            if (this.vEmail && this.vJmeno && this.vMesto && this.vPhoneNumber && this.vPrijmeni && this.vPsc && this.vUlice) {
                var evt = new CustomEvent("rekapitulaceEvent", { detail: { jmeno: this.jmeno, prijmeni: this.prijmeni, telefon: telefon, email: this.email, psc: this.psc, ulice: this.ulice, mesto: this.mesto } });
                window.dispatchEvent(evt);
            }
            else {
                alert("chybný vstup");
            }
        }
    }
}
</script>

<style scoped>
.form {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    row-gap: 0.5em;
    width: 20em;
}

.form>input {
    width: 15em;
    margin-left: 4em;
}

.form>div {
    width: 15em;
    margin-left: 3em;
}

.form>div>select {
    width: 4em;
    margin-left: 0.5em;
}

.form>div>input {
    width: 10em;
    margin-left: 0.5em;
}

.form>input[type=submit] {
    width: 15.5em;
}

.spatnyVstup {
    border: 1px solid red;
}
</style>
