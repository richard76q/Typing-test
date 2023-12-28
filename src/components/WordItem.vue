<template>
    <div class="container__word" :style="{'margin-top': marginTop}">
        <span class="word" v-for="word in words" :key="word[0]" :class="giveClass(word)">{{ word[0] }}</span>
    </div>
</template>

<script>
    export default {
        props: {
            words: {
                type: Array,
                // default: () => [[1, 2]],
                required: true
            }
        },
        data() {
            return {
                marginTop: '0px'
            }
        },
        methods: {
            giveClass(list) {
                const ntype = list[1];
                if (ntype === undefined) {
                    return
                } else if (ntype === 2) {
                    return "word-mistake"
                } else if (ntype === 1) {
                    this.checkWord1();
                    return "comp-green"
                } else if (ntype === 0) {
                    return "comp-red"
                } else {
                    console.log("error")
                }
            },
            
            checkWord1() {
                const node = document.querySelector(".container__word");
                console.log(node.height);
                return node
            }
        }
    }
</script>

<style scoped>
.container__word {
    word-break: break-all;
    user-select: none;
}

.word {
    display: inline-block;
    font-size: 2.6em;
    line-height: 1.2em;
    font-weight: 600;
    /* margin: 0px 2px; */
    padding: 4px 7px;
    color: #61c9ff;
    /* color: #000; */
}

.comp-green {
    color: green;
}

.comp-red {
    color: red;
}

.word-mistake {
    background-color: #FFCBDB;
}
</style>