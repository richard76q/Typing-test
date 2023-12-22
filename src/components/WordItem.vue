<template>
    <div class="container__word" :style="{'margin-top': marginTop}">
        <span class="word" v-for="word in words" :key="word">{{ word }}</span>
    </div>
</template>

<script>
    export default {
        props: {
            words: {
                type: Array,
                default: () => [],
                required: true
            }
        },
        data() {
            return {
                marginTop: '-0px'
            }
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