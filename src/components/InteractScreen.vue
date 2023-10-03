<template>
    <h1>Interact Screen Heer ...</h1>
    <card-flip v-for="(card,index) in cardContext" :key="index" :imgBackFaceUrl="`images/${card}.png`">
    </card-flip>
</template>
<script>
import CardFlip from './Card.vue';
export default {
    components:{CardFlip},
    props: {
        cardContext: {
            type: Array,
            default: function() {
                return [];
            }
        }
    }
}
</script>