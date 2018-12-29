<template>
    <div class="carousel">
        <slot></slot>
        <button class="button carousel-nav carousel-prev" @click.prevent="prev">Précédent</button>
        <button class="button carousel-nav carousel-next" @click.prevent="next">Suivant</button>
        <div class="carousel-pagination">
            <button v-for="n in slides_count" @click="goto(n-1)" :class="{active: n-1 === index}"></button>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Carousel",
        data: function () {
            return {
                index: 0,
                slides: [],
                direction: 'right'
            }
        },
        computed: {
            slides_count() {
                return this.slides.length
            }
        },
        watch: {
            slides (slides){
                if(this.index >= this.slides_count){
                    this.index = this.slides_count - 1
                }
            }
        },
        methods: {
            next() {
                this.index++
                this.direction = 'right';
                if (this.index >= this.slides_count) {
                    this.index = 0
                }
            },
            prev() {
                this.index--
                this.direction = 'left';
                if (this.index < 0) {
                    this.index = this.slides_count - 1
                }
            },
            goto(n) {
                this.direction = n > this.index ? 'right' : 'left';
                this.index = n
            }
        },
        mounted: function () {
            this.slides = this.$children
        },
    }
</script>

<style scoped>

    .carousel {
        position: relative;
        overflow: hidden;
    }

    .carousel-nav {
        position: absolute;
        top: 50%;
        left: 10px;
    }

    .carousel-next {
        right: 10%;
        left: auto;
    }

    .carousel-pagination {
        position: absolute;
        bottom: 10px;
        left: 0;
        right: 0;
        text-align: center;
    }

    .carousel-pagination button {
        display: inline-block;
        width: 10px;
        height: 10px;
        background-color: #000;
        opacity: 0.8;
        border-radius: 10px;
        margin: 0 2px;
    }

    .carousel-pagination button.active {
        background-color: #fff;
    }


</style>