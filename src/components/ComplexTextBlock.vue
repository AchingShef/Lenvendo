<script>

import TextBlock from "./TextBlock";

export default {
    extends: TextBlock,
    data() {
        return {
            name: "complex",
            delay: 700,
            clicks: 0,
            timer: null,
            color: this.$props.color
        };
    },
    methods: {
        select() {
            this.clicks += 1;

            if (this.clicks === 1) {
                this.timer = setTimeout(() => {
                    this.selected = !this.selected;

                    this.$emit("select-text-block", this.selected, this.guid);

                    this.clicks = 0
                }, this.delay);
            } else{
                clearTimeout(this.timer);

                this.clicks = 0;
                
                if (this.color !== "green") {
                    this.$refs.container.classList.add("green");
                    this.$refs.container.classList.remove("red");
                    this.color = "green";
                } else {
                    this.$refs.container.classList.remove("green");
                    this.$refs.container.classList.add("red");
                    this.color = "red";
                }

                this.$emit("change-color", this.guid, this.color);
            }     
        }
    }
}
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

    .red {
        background-color: #BB525E;
    }

    .green {
        background-color: #A4D26C;
    }
</style>

