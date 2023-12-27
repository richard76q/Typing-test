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
                marginTop: '-0px'
            }
        },
        methods: {
            giveClass(list) {
                const ntype = list[1];
                if (ntype === undefined) {
                    // console.log('none')
                    return
                } else if (ntype === 1) {
                    return "comp-green"
                } else if (ntype === 0) {
                    return "comp-red"
                } else {
                    console.log("error")
                }
            },
        }
    }
</script>

<style scoped>
.container__word {
    /* box-sizing: border-box; */
    /* margin-top: -40px;    */
    word-break: break-all;
    user-select: none;
}

.word {
    display: inline-block;
    font-size: 2.2em;
    line-height: 1.2em;
    font-weight: 600;
    /* margin: 0px 2px; */
    padding: 3px 5px;
    color: #61c9ff;
}

.comp-green {
    color: green;
}

.comp-red {
    color: red;
}
</style>