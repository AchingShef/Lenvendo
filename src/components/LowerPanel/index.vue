<template>
    <div class="lower-panel">
        <div class="panel-container">
            
        </div>
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
    .lower-panel {
        width: 100%;
        height: 50px;
        position: fixed;
        bottom: 0;
        background: #2196F3;
        box-sizing: border-box;
        border-radius: 16px;
        z-index: 10000;
        width: 100%;
    }
</style>
