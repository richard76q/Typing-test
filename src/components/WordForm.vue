<template>
    <div class="wrapper">
        <div class="input-word">
            <!-- <WordItem :words="wordsMod"/> -->
            <WordItem :words="wordsMod"/>
            <!-- <MyButton @click="correctAnswer">обновить</MyButton> -->
        </div>
    </div>
</template>

<script>
// import MyButton from './UI/MyButton.vue';
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
        },
        update: {
            type: Number,
            // default: 0,
            required: true
        }
    },
    data() {
        return {
            wordsMod: [],
        };
    },
    components: {
    WordItem,
    // MyButton
},

    methods: {
        correctAnswer() {
            const new_arr = [];

            for (let i = 0; i < this.words.length; i++) {
                if (i >= this.completed.length) {
                    new_arr.push([this.words[i]])
                    continue;
                }
                new_arr.push([this.words[i], this.completed[i]]);
            }

            this.wordsMod = new_arr;
            // console.log(this.wordsMod);
        }
    },
    watch: {
        update() {
            this.correctAnswer();
        }
    }
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