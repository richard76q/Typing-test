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
                required: true
            },
            moveDown: {
            type: Number,
            required: false
        },
        },
        data() {
            return {
                marginTop: '',
                marginValue: 0,
            }
        },
        methods: {
            giveClass(list) {
                const ntype = list[1];
                if (ntype === undefined) {
                    return
                } else if (ntype === 1) {
                    return "comp-green"
                } else if (ntype === 0) {
                    return "comp-red"
                } else if (ntype === 3) {
                    this.checkWord1();
                    return "word-next"
                } else if (ntype === 2) {
                    return "word-mistake"
                } else {
                    console.log("error")
                }
            },
            
            checkWord1() {
                const node = document.getElementsByClassName("word-next");
                console.log(node)
            },

            marginMoveDown() {
                this.marginValue += 60;
                return '-' + String(this.marginValue) + 'px'
            }
        },
        watch: {
            moveDown() {
                this.marginTop = this.marginMoveDown();
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
    border-bottom: 2px solid #fff;
    /* color: #000; */
}

.comp-green {
    color: #22bb22;
}

.comp-red {
    color: #E00;
}

.word-mistake {
    background-color: #FFCBDB;
    border-bottom: 2px solid #E00;
}

.word-next {
    background-color: #f4f4f4;
    border-bottom: 2px solid #61c9ff;
}
</style>