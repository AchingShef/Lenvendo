<template>
    <div class="upper-panel">
        <button class="btn" v-on:click="addTextBlock(true)">Add text block</button>
        <button class="btn" v-on:click="addTextBlock(false)">Add complex text block</button>
    </div>    
</template>

<script>
export default {
    data() {
        return {

        }
    },
    methods: {
        addTextBlock(isSimple) {
            this.$emit("add-text-block", isSimple);
        }
    }
};
</script>


<style lang="less" scoped>
    .upper-panel {
        width: 100%;
        height: 50px;
        background: #2196F3;
        border-radius: 16px;
        padding: 10px 15px;
        box-sizing: border-box;
        text-align: right;
        margin-bottom: 5px;

        .btn {
            color: #333333;
            background-color: #ffffff;
            padding: 5px 10px;
            border: none;
            border-radius: 3px;
            text-align: center;
            text-decoration: none;
            display: inline-block;
            cursor: pointer;
        }
    }
</style>
