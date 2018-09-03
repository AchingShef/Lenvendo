<template>
    <div class="main">
        <upper-panel v-on:add-text-block="onAddTextBlock"/>
        <template v-for="item in textBlocks">
            <text-block
                :prop-guid="item.guid"
                v-if="item.isSimple"
                v-bind:key="item.guid"
                v-on:destroy-text-block="onDestoyTextBlock"
                v-on:select-text-block="onSelecteTextBox"
            />
            <complex-text-block
                :prop-guid="item.guid"
                :prop-color="item.color"
                v-else
                v-bind:key="item.guid"
                v-on:destroy-text-block="onDestoyTextBlock"
                v-on:select-text-block="onSelecteTextBox"
                v-on:change-color="onChangeColor"
            />
        </template>
    </div>
</template>

<script>
    import UpperPanel from "./UpperPanel";
    import TextBlock from "./TextBlock";
    import ComplexTextBlock from "./ComplexTextBlock";

    export default {
        data() {
            return {
                textBlocks: [

                ]
            };
        },
        methods: {
            onAddTextBlock(isSimple) {
                let textBlock = {
                    isSimple: isSimple,
                    guid: this.genGuid(),
                    selected: false
                };

                if (!isSimple) {
                    textBlock.color = null;   
                }

                this.textBlocks.push(textBlock);
            },
            getElementByGuid(guid) {
                for (let i = 0; i < this.textBlocks.length; i += 1) {
                    if (this.textBlocks[i].guid === guid) {
                        return this.textBlocks[i];
                    }
                }
            },
            onDestoyTextBlock(guid) {
                for (let i = 0; i < this.textBlocks.length; i += 1) {
                    if (this.textBlocks[i].guid === guid) {
                        this.textBlocks.splice(i, 1);

                        break;
                    }
                }
            },
            onSelecteTextBox(selected, guid) {
                this.getElementByGuid(guid).selected = selected;
            },
            onChangeColor(guid, color) {
                this.getElementByGuid(guid).color = color;
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
            "text-block": TextBlock,
            "complex-text-block": ComplexTextBlock
        }
    };
</script>


<style lang="less" scoped>
    .main {
        height: 100%;
    }
</style>
