<template>
    <div>
        <ClientOnly>
            <slot name="before"></slot>
            <span ref="countUp"></span>
        </ClientOnly>
    </div>
</template>countUp

<script>
    export default {
        name: "CountUp",
        data() {
            return {
                counter: null,
            }
        },
        props: {
            startVal: {
                type: Number,
                default: 0
            },
            endVal: {
                type: Number,
                required: true
            },
            decimalPlaces: {
                type: Number,
                default: 0
            },
            duration: {
                type: Number,
                default: 2
            },
            delay: {
                type: Number,
                default: 0
            },
        },
        mounted() {
            this.init()
        },
        beforeDestroy() {
            this.counter.reset();
            this.counter = null
        },
        methods: {
            init() {
                import('countup.js').then(module => {
                    this.$nextTick(() => {
                        this.counter = new module.CountUp(this.$refs.countUp, this.endVal, {
                            startVal: this.startVal,
                            decimalPlaces: this.decimalPlaces,
                            duration: this.duration
                        })

                        setTimeout(() => {
                            this.counter.start()
                        }, this.delay)
                    })
                })
            }
        }
    }
</script>

<style scoped>

</style>
