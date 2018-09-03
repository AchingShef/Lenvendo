<template>
    <div class="main">
        <upper-panel v-on:add-text-block="onAddTextBlock"/>
    </div>
</template>

<script>
    import UpperPanel from "./UpperPanel";

    export default {
        data() {
            return {
                
            };
        },
        methods: {
            onAddTextBlock(isSimple) {
                
            }
        },
        components: {
            "upper-panel": UpperPanel
        }
    };
</script>


<style lang="less" scoped>
    .main {
        height: 100%;
    }
</style>
