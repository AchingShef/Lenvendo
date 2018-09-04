<script>

import TextBlock from "../TextBlock/";


export default {
    props: ["prop-guid", "prop-name", "prop-color"],
    extends: TextBlock,
    data() {
        return {
            delay: 700,
            clicks: 0,
            timer: null,
            color: this.$props.propColor
        };
    },
    methods: {
        select(e) {
            this.clicks += 1;

            if (this.clicks === 1) {
                this.timer = setTimeout(() => {
                    this.selected = !this.selected;

                    this.$emit("select-text-block", this.selected, this.guid);

                    this.clicks = 0
                }, this.delay);
            } else {
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
    @import url("../TextBlock/style.less");

    .text-block.red {
        background-color: #BB525E;
    }

    .text-block.green {
        background-color: #A4D26C;
    }
</style>

