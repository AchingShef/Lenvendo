<template>
    <div class="text-block" v-on:click="select" ref="container">
        <span class="close" v-on:click.stop="destroy">x</span>
        <span class="name" v-once>{{ name }}</span>
        <p class="text" v-once>{{ text }}</p>
        <span class="selected" v-on:click="markerClick" v-if="selected">V</span>
    </div>
</template>

<script>
export default {
    props: ["prop-guid"],
    data() {
        return {
            name: "simple",
            text: this.genText(),
            selected: false,
            guid: this.$props.propGuid,
            delay: 700,
            clicks: 0,
            timer: null
        };
    },
    methods: {
        genText() {
            return Math.random().toString(36);
        },
        destroy(e) {
            this.$emit("destroy-text-block", this.guid);
        },
        select() {
            this.selected = !this.selected;

            this.$emit("select-text-block", this.selected, this.guid);
        },
        markerClick(e) {
            e.stopPropagation();
        }
    }
};
</script>

<style lang="less" scoped>
    .text-block {
        width: 200px;
        min-height: 200px;
        display: inline-block;
        margin: 5px;
        background-color: #f5f5f5;
        border: 1px solid #cccccc;
        border-radius: 3px;
        padding-bottom: 25px;
        float: left;
        position: relative;

        .close {
            display: block;
            float: right;
            padding:2px 5px;
            background:#cccccc;
            cursor: pointer;
        }

        .selected {
            position: absolute;
            right: 0px;
            bottom: 0px;
            height: 25px;
            width: 25px;
            border-radius: 50%;
            background-color: #000000;
            font-size: 25px;
            color: #ffffff;
        }
    }
</style>

