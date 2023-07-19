<template>
    <div class="kosik">
        <KosikItems></KosikItems>
        <div class="total">
            <span>Celkem s dph: {{ celkemsdph }}</span>
            <span>Celkem bez dph: {{ celkembezdph }}</span>
            <span>Celkem dph: {{ celkemdph }}</span>
        </div>
    </div>
</template>

<script>
import KosikItems from './KosikItems'

export default {
    data() {
        return {
            celkemsdph: 0,
            celkembezdph: 0,
            celkemdph: 0
        }
    },
    components: {
        KosikItems
    },
    name: 'Kosik',
    methods: {
    },
}
</script>

<style scoped>
.kosik {
}

.total {
    display: flex;
    flex-direction: column;
}
</style>
