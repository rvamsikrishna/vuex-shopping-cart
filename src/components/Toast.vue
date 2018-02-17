<template>
    <div class="alert" v-show="isActive">
        {{text}}
    </div>
</template>

<script>
    export default{
        props:["show", "text"],
        data() {
            return {
                isActive: !!this.show,
                activeTimeout: {}
            };
        },
        mounted() {
            this.setTimeout();
        },
        watch: {
            show(newVal) {
                this.isActive = !!newVal;
            },
            isActive(newVal) {
                if(this.show !== !!newVal){
                    this.$emit("hide-toast", newVal);
                }
                this.setTimeout();
            }
        },
        methods: {
            setTimeout() {
                clearTimeout(this.activeTimeout);
                if(this.isActive) {
                    this.activeTimeout = setTimeout(() => {
                        this.isActive = false
                    }, 2000)
              }
            }
         }
    }
</script>


<style scoped>
    .alert{
        width: 30%;
        background-color: rgba(0, 0, 0, 0.7);
        text-align: center;
        font-weight: bold;
        color: white;
        position: fixed;
        bottom: 0;
        left: 50%;
        transform: translateX(-50%);
    }
</style>
