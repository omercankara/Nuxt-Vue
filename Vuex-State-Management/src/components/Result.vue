<template>
        <div>
                <p class="counter-container">Sayaç : {{ double }}</p>
                <p class="counter-container">Tıklama sayısı {{ stringC }}</p>
        </div>
</template>
<script>
import { mapGetters } from "vuex";
export default {
        computed: {
             ...mapGetters({
                double:'getDoubleCounter',
                stringC:'stringCounter'
             })
               
        },
};
</script>
<style scoped>
.counter-container {
        border: 1px solid #aa7f08;
        padding: 10px 5px;
        background-color: #fbbd08;
        font-size: 20px;
        color: #000;
}
</style>
