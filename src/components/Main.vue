<template>
    <div class="main">
        <upper-panel v-on:add-text-block="onAddTextBlock"/>
        <template v-for="item in textBlocks">
            <text-block 
                v-if="item.isSimple"
                v-bind:key="item.guid"
                v-on:destroy-text-block="onDestoyTextBlock(item)"/>
        </template>
    </div>
</template>

<script>
    import UpperPanel from "./UpperPanel";
    import TextBlock from "./TextBlock";

    export default {
        data() {
            return {
                textBlocks: [

                ]
            };
        },
        methods: {
            onAddTextBlock(isSimple) {
                if (isSimple) {
                    this.textBlocks.push({
                        isSimple: isSimple,
                        guid: this.genGuid()
                    })
                }
            },
            onDestoyTextBlock(item) {
                for (let i = 0; i < this.textBlocks.length; i += 1) {
                    if (this.textBlocks[i] === item) {
                        this.textBlocks.splice(i, 1);
                    }
                }
            },
            genGuid() {
                function s4() {
                    return Math.floor((1 + Math.random()) * 0x10000).toString(16).substring(1);
                }

                return s4() + s4() + '-' + s4() + '-' + s4() + '-' + s4() + '-' + s4() + s4() + s4();
            },
        },
        components: {
            "upper-panel": UpperPanel,
            "text-block": TextBlock
        }
    };
</script>


<style lang="less" scoped>
    .main {
        height: 100%;
    }
</style>
