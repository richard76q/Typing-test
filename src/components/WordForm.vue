<template>
    <div class="wrapper">
        <div class="input-word">
            <!-- <WordItem :words="wordsMod" :updateWordheight="updateWordHeight" :id="id"/> -->
            <WordItem :words="wordsMod" :id="id"/>
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
        },
        update: {
            type: Number,
            // default: 0,
            required: true
        },
        // updateWordHeight: {
        //     type: Number,
        //     required: false
        // },
        id: {
            type: Number,
            required: false
        }
    },
    data() {
        return {
            wordsMod: [],
            wordId: [],
        };
    },
    components: {
    WordItem,
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
    },
    watch: {
        update() {
            this.correctAnswer();
        }
    },
    // created() {
    //     this.updateWordheight += 1;
    //     console.log(this.updateWordHeight)
    // }
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