<template>
    <div v-on:click.capture.stop="select">
        <text-block
            ref="text-box" 
            :prop-name="this.$props.propName" 
            :prop-guid="this.$props.propGuid"
            v-on:destroy-text-block="destroy">
        </text-block>
    </div>
</template>



<script>

import TextBlock from "../TextBlock/";
// import Modal from "../Modal/";

export default {
    props: ["prop-guid", "prop-name", "prop-color"],
    components: {
        "text-block": TextBlock,
        // "modal": Modal
    },
    data() {
        return {
            selected: false,
            delay: 700,
            clicks: 0,
            timer: null,
            color: this.$props.propColor
        };
    },
    methods: {
        select() {
            this.clicks += 1;

            if (this.clicks === 1) {
                this.timer = setTimeout(() => {
                    this.selected = !this.selected;

                    this.$refs["text-box"].select();

                    this.clicks = 0
                }, this.delay);
            } else{
                clearTimeout(this.timer);

                this.clicks = 0;
                
                if (this.color !== "green") {
                    this.$refs["text-box"].$refs.container.classList.add("green");
                    this.$refs["text-box"].$refs.container.classList.remove("red");
                    this.color = "green";
                } else {
                    this.$refs["text-box"].$refs.container.classList.remove("green");
                    this.$refs["text-box"].$refs.container.classList.add("red");
                    this.color = "red";
                }

                this.$emit("change-color", this.guid, this.color);
            }     
        },
        destroy (guid) {
            console.log("Удаляем")
        }
    }
}
</script>

<style lang="less" scoped>
    @import url("../TextBlock/style.less");

    .text-block.red {
        background-color: #BB525E;
    }

    .text-block.green {
        background-color: #A4D26C;
    }
</style>

