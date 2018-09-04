<template>
    <div class="main">
        <upper-panel v-on:add-text-block="onAddTextBlock"/>
        <template v-for="item in textBlocks">
            <text-block
                :prop-guid="item.guid"
                prop-name="simple"
                v-if="item.isSimple"
                v-bind:key="item.guid"
                v-on:destroy-text-block="onDestoyTextBlock"
                v-on:select-text-block="onSelectTextBox"
            />
            <complex-text-block
                :prop-guid="item.guid"
                :prop-color="item.color"
                prop-name="complex"
                v-else
                v-bind:key="item.guid"
                v-on:destroy-text-block="prepareToDestroy"
                v-on:select-text-block="onSelectTextBox"
                v-on:change-color="onChangeColor"
            />
        </template>
        <div class="wrapper"></div>
        <lower-panel 
            :prop-count="count.all"
            :prop-selected="count.selected"
            :prop-green="count.green"
            :prop-red="count.red"
        />
        <modal v-if="showModal" @cancel="showModal = false" @ok="destroyComplexTextBlock"/>
    </div>
</template>

<script>
    import UpperPanel from "./UpperPanel";
    import LowerPanel from "./LowerPanel";
    import TextBlock from "./TextBlock/";
    import ComplexTextBlock from "./ComplexTextBlock/";
    import Modal from "./Modal/";

    export default {
        data() {
            return {
                textBlocks: [

                ],
                showModal: false,
                destroyGuid: null,
                count: {
                    all: 0,
                    selected: 0,
                    green: 0,
                    red: 0
                }
            };
        },
        methods: {
            destroyComplexTextBlock() {
                this.showModal = false;

                this.onDestoyTextBlock(this.destroyGuid);

                this.destroyGuid = null;
            },
            prepareToDestroy(guid) {
                this.destroyGuid = guid;
                this.showModal = true;
            },
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
            onSelectTextBox(selected, guid) {
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
            "complex-text-block": ComplexTextBlock,
            "lower-panel": LowerPanel,
            "modal": Modal
        },
        watch: {
            textBlocks: {
                handler() {
                    let selected = 0,
                        green = 0,
                        red = 0;

                    this.textBlocks.forEach(item => {
                        if (item.selected) {
                            selected += 1;

                            if (item.color) {
                                item.color === "green" ? green += 1 : red += 1;
                            }
                        }
                    });

                    this.count.all = this.textBlocks.length;
                    this.count.selected = selected;
                    this.count.green = green;
                    this.count.red = red;
                },
                deep: true
            }
        }
    };
</script>


<style lang="less" scoped>
    .main {
        height: 100%;
    }

    .wrapper {
        height: 50px;
        clear: both;
    }
</style>
