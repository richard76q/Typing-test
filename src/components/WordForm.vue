<template>
    <div class="wrapper">
        <div class="input-word">
            <WordItem :words="words" />
        </div>
    </div>
</template>

<script>
import WordItem from './WordItem.vue';

    export default {
    props: {
        words: {
            type: Array,
            default: () => [],
            required: true
        },
        completed: {
            type: Array,
            default: () => [],
            required: true
        }
    },
    data() {
        return {
        };
    },
    methods: {
        checkWords() {
            const Node = document.getElementsByClassName('container__word');
            console.log(Node);
        }
    },
    components: { WordItem }
}
</script>

<style scoped>

.wrapper {
    width: 800px;
}

.input-word {
    max-width: 1000px;
    max-height: 120px;
    /* width: 800px;
    height: 40px; */
    padding: 5px 10px 40px 10px; 
    /* background-color: #000; */
    border: 4px solid #000;
    overflow: hidden;

}
</style>