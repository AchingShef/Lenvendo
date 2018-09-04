<template>
    <div class="lower-panel">
        <div class="panel-container">
            <div class="count">
                Blocks count: {{propCount}}
            </div>
            <div class="selected">
                Selected blocks: {{propSelected}}
            </div>
            <div class="selected">
                Selected green: {{propGreen}}
            </div>
            <div class="selected">
                Selected red: {{propRed}}
            </div>
        </div>
    </div>    
</template>

<script>
export default {
    props: ["prop-count", "prop-selected", "prop-green", "prop-red"],
    data() {
        return {

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
        padding: 15px 15px;
        display: table;

        .panel-container {
            display: table-row;

            div {
                color: #ffffff;
                display: table-cell;
            }
        }
    }
</style>
