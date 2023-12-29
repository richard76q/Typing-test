<template>
    <div class="wrapper">
        <div class="input-word">
            <WordItem :words="wordsMod" :moveDown="moveDown"/>
            <!-- <MyButton @click="correctAnswer">обновить</MyButton> -->
        </div>
        <!-- <button @click="checkInput">da</button> -->
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
        },
        moveDown: {
            type: Number,
            required: false
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
        },
        checkInput() {
            const word = document.getElementsByClassName("input-word");
            // const heightWord = word.offsetHeight 
            console.log(word[0].offsetHeight)
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
    width: 1000px;
}

.input-word {
    max-height: 145px;
    height: 145px;
    padding: 5px 10px 70px 10px; 
    border: 8px solid #000;
    border-top: 10px solid #000;
    border-bottom: 0;
    overflow: hidden;

}
</style>