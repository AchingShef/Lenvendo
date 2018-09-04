<template>
    <div class="text-block" @click="select" ref="container">
        <span class="close" @click.stop="$emit('destroy-text-block', guid)">x</span>
        <span class="name" v-once>{{ name }}</span>
        <p class="text" v-once>{{ text }}</p>
        <span class="selected" @click="markerClick" v-if="selected">&#10004;</span>
    </div>
</template>

<script>
export default {
    props: ["prop-guid", "prop-name"],
    data() {
        return {
            name: this.$props.propName,
            text: this.genText(),
            selected: false,
            guid: this.$props.propGuid
        };
    },
    methods: {
        genText() {
            return Math.random().toString(36);
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
    @import url("./style.less");
</style>

