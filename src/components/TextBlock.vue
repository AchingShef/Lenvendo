<template>
    <div class="text-block">
        <span class="close" v-on:click="destroy">x</span>
        <p class="text" v-once>{{ text }}</p>
    </div>
</template>

<script>
export default {
    data() {
        return {
            text: this.genText()
        };
    },
    methods: {
        genText() {
            return Math.random().toString(36);
        },
        destroy() {
            this.$emit("destroy-text-block")
        }
    }
};
</script>

<style lang="less" scoped>
    .text-block {
        width: 300px;
        height: 200px;
        display: block;
        margin-left: auto;
        margin-right: auto;
        margin-top: 5px;
        margin-bottom: 5px;
        background-color: #f5f5f5;
        border: 1px solid #cccccc;
        border-radius: 3px;

        .close {
            display: block;
            float: right;
            padding:2px 5px;
            background:#cccccc;
            cursor: pointer;
        }
    }
</style>

