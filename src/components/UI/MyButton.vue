<template>
    <button class="button" :style="{'background-color': color}">
        <slot></slot>
    </button>
</template>

<script>
    export default {
        props: {
            color: {
                type: String
            }
        }
    }
</script>

<style scoped>
.button {
    margin-left: 10px;
    padding: 5px 10px;
    /* text-align: center; */
    /* background-color: #FFCBDB; */
    border: none;
    font-size: 32px;
    line-height: 30px;
}
</style>